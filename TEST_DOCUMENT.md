# Software Test Plan & Test Cases Document
## "Learn English with AI" System

- **Document Version:** 1.0
- **Related Documents:** [FRD.md](./FRD.md), [TECHNICAL_DOCUMENT.md](./TECHNICAL_DOCUMENT.md)
- **System Under Test:** Decoupled Full-Stack Web Application (`Next.js App Router` + `FastAPI`)

---

## 1. Test Strategy & Scope

### 1.1 Objectives
Verify that the **"Learn English with AI"** platform satisfies its functional requirements (`FR-005`–`FR-074`), non-functional requirements (`NFR-001`–`NFR-006`), API contracts, ML pipeline accuracy/latency, and graceful degradation behavior across guest and authenticated user flows.

### 1.2 Scope
| Layer | Components Under Test |
| :--- | :--- |
| **Frontend (`frontend/`)** | Next.js 15+ (App Router), localization (`hy`, `ru`, `en`), `@dnd-kit` card reordering, `Local Storage` guest state (`lewa_guest_state_v1`), audio player timestamp sync, `MediaRecorder` WebSocket client |
| **Backend (`backend/`)** | FastAPI `/api/v1` REST endpoints, SSE streaming (`/ai/help`), WebSocket (`/ws/speaking/{session_id}`), JWT auth, Redis sliding-window rate limiter, SQLAlchemy 2.0 models |
| **ML & AI Pipeline** | Silero VAD, `faster-whisper` (STT), `wav2vec2` / WhisperX (GOP pronunciation scoring), TTS engine, LLM service |
| **Data & Storage** | PostgreSQL 16, Redis cache/rate-limit store, Cloudflare R2 object storage |

### 1.3 Test Levels
1. **Unit Testing:** Isolated testing of Pydantic schemas, services (daily plan, mistake analyzer), React hooks (`useAudioRecorder`, `useGuestProgress`), and utility functions.
2. **Integration Testing:** FastAPI endpoints against test PostgreSQL & Redis instances, database migrations (Alembic), and mocked external LLM/R2 providers.
3. **End-to-End (E2E) Testing:** Full browser flows covering guest onboarding, migration on sign-up, content consumption, audio playback sync, and AI interactions.
4. **ML & Audio Pipeline Testing:** Audio chunk streaming, VAD segmentation, STT transcription accuracy, GOP pronunciation scoring, and temporary audio cleanup.
5. **Non-Functional Testing:** Latency benchmarks (`<= 3s` speaking target), fault injection (`503 AI_UNAVAILABLE`), responsive layout, and WCAG AA accessibility.

---

## 2. Test Environment & Tooling

### 2.1 Recommended Testing Stack
- **Backend:** `pytest`, `pytest-asyncio`, `httpx` (AsyncClient), `pytest-mock`
- **Frontend:** `Vitest` + React Testing Library (unit/component), `Playwright` (E2E, WebSocket/media mocking, accessibility checks via `@axe-core/playwright`)
- **Performance / Load:** `k6` or `Locust` for REST/SSE/WebSocket concurrency and latency profiling

### 2.2 Environment Configuration
- **Database:** Dedicated PostgreSQL 16 test instance seeded from `backend/seeds/`.
- **Cache:** Dedicated Redis instance flushed between rate-limit test suites.
- **External Services:** Deterministic stubs/mocks for LLM (Gemini/OpenAI), TTS, and Cloudflare R2 (`boto3` mock) in CI; live staging environment for end-to-end ML latency validation.

---

## 3. Functional Test Cases

### 3.1 Authentication & Guest Migration (`FR-005`, `FR-006`, `FR-007`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-AUTH-01` | User Registration & Login | Unregistered email | 1. `POST /api/v1/auth/register` with valid email & password.<br>2. `POST /api/v1/auth/login`. | User created in `USERS`; returns short-lived `access_token` and sets `HttpOnly` `refresh_token` cookie. |
| `TC-AUTH-02` | Token Refresh | Valid `refresh_token` cookie | 1. `POST /api/v1/auth/refresh`. | Returns a new valid `access_token`; expired/invalid refresh tokens return `401 Unauthorized`. |
| `TC-AUTH-03` | Guest Progress Persistence | Unauthenticated browser session | 1. Complete a lesson and bookmark a word.<br>2. Inspect `Local Storage`. | `lewa_guest_state_v1` exists with `version: 1`, `completed_lessons`, `test_scores`, `bookmarked_words`, and `card_order`. |
| `TC-AUTH-04` | Idempotent Guest Migration | Guest has `lewa_guest_state_v1` populated | 1. Register/login.<br>2. Client sends payload to `POST /api/v1/auth/migrate-guest`.<br>3. Re-send the same payload a second time. | Records merge into `USER_PROGRESS`, `TEST_ATTEMPTS`, `VOCAB_BOOKMARKS`, and `USER_PREFERENCES`; second call skips duplicates without error; `lewa_guest_state_v1` is cleared on success. |

---

### 3.2 User Preferences, Localization & Dashboard (`FR-008`, `FR-010`–`FR-013`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-UI-01` | Multi-language Switching | App loaded | 1. Switch locale between `en`, `hy` (Armenian), and `ru` (Russian). | Routes update to `/[locale]/...`; UI labels render from `messages/{locale}.json` without missing keys. |
| `TC-UI-02` | Card Reordering Persistence | Authenticated user on main page | 1. Drag and drop a learning card using `@dnd-kit`.<br>2. Reload the page. | `PATCH /users/me/preferences` persists `card_layout_order`; order remains preserved after reload. |
| `TC-UI-03` | Level & Interests Update | Authenticated user | 1. Update `current_level` (`A0`–`B2`), `target_level`, and `interests` via `PATCH /users/me/preferences`. | `GET /users/me/preferences` returns updated values; content filtering reflects the updated level. |

---

### 3.3 Learning Content, Audio Sync & Tests (`FR-042`, `FR-043`, `FR-059`–`FR-062`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-CNT-01` | Content Filtering | Seeded lessons & vocabulary | 1. Query `GET /api/v1/grammar`, `/vocabulary`, `/listening`, `/reading`, `/songs`, `/exams` with `level`, `theme`, `pos` params. | Returns `200 OK` with items strictly matching the filter criteria. |
| `TC-CNT-02` | Reading Audio Timestamp Sync | Reading lesson with `timestamps` JSON | 1. Play audio in Reading view.<br>2. Advance playback to `start <= t <= end` of `segment_id: 2`. | `timeupdate` handler highlights `segment_id: 2` accurately in the UI. |
| `TC-CNT-03` | Songs Difficulty Masks | Song lesson with timestamps & masks | 1. Open Song in Level 1, Level 2, and Level 3 modes. | Lyrics display ~10% blanks (Level 1), ~25% blanks (Level 2), and ~45% blanks (Level 3). |
| `TC-CNT-04` | Test Submission (Guest vs Registered) | Valid test ID | 1. Submit answers to `POST /api/v1/tests/{id}/submit` as guest.<br>2. Submit as authenticated user. | Both receive graded score; authenticated submission stores `TEST_ATTEMPTS` and triggers AI summary. |

---

### 3.4 AI Help & Rate Limiting (`FR-016`, `FR-018`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-AI-01` | Context-Aware AI Help SSE | Valid lesson context | 1. `POST /api/v1/ai/help` with question and lesson context. | Response streams via `text/event-stream` (SSE) with contextually relevant explanation. |
| `TC-AI-02` | Guest Rate Limiting | Unauthenticated IP/session; Redis active | 1. Send 5 requests to `POST /api/v1/ai/help`.<br>2. Send a 6th request within the same day window. | First 5 requests succeed (`200 OK`); 6th request is rejected with `429 Too Many Requests`. |
| `TC-AI-03` | Authenticated Quota | Authenticated user | 1. Send > 5 requests to `POST /api/v1/ai/help` within registered quota. | Requests succeed beyond the guest limit up to the registered user quota. |

---

### 3.5 Writing & Personalized Tutor (`FR-047`, `FR-048`, `FR-063`–`FR-070`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-WRT-01` | Writing Prompt & Evaluation | Authenticated user | 1. Call `POST /api/v1/ai/writing/generate`.<br>2. Submit essay with intentional grammar errors to `POST /api/v1/ai/writing/evaluate`. | Returns structured grammar/vocabulary feedback and logs identified errors in `MISTAKES`. |
| `TC-TUT-01` | Daily Plan & Mistake Review | User has logged entries in `MISTAKES` | 1. Call `GET /api/v1/tutor/daily-plan`.<br>2. Complete review via `POST /api/v1/tutor/review`. | Daily plan includes targeted tasks; resolved mistakes update `MISTAKES.resolved = true`. |

---

### 3.6 Speaking & Pronunciation ML Pipeline (`FR-050`–`FR-054`)

| Test ID | Title | Preconditions | Steps | Expected Result |
| :--- | :--- | :--- | :--- | :--- |
| `TC-SPK-01` | Real-Time Voice Dialogue | Authenticated user; WebSocket connected to `/ws/speaking/{session_id}` | 1. Stream `webm/opus` speech chunks.<br>2. Pause speaking to trigger Silero VAD end-of-speech. | Backend transcribes via `faster-whisper`, generates LLM reply + TTS audio stream, and returns live transcript + audio to client. |
| `TC-SPK-02` | Pronunciation & Fluency Scoring | Sample English audio with known mispronunciations | 1. Stream audio through `/ws/speaking/{session_id}`. | `wav2vec2`/GOP scorer returns word/phoneme scores, speaking rate (WPM), and highlights mispronounced words; session saved in `SPEAKING_SESSIONS`. |
| `TC-SPK-03` | Model Startup Lifespan | FastAPI server startup | 1. Inspect startup logs and send 2 consecutive speaking requests. | `faster-whisper` and `wav2vec2` load once during FastAPI `lifespan` startup, not per request. |

---

## 4. Non-Functional & Edge-Case Test Scenarios

| Test ID | Category | Requirement | Test Scenario & Pass Criteria |
| :--- | :--- | :--- | :--- |
| `TC-NFR-01` | **Latency** | `NFR-001` | Measure time from end-of-speech (VAD trigger) to first TTS audio byte on `/ws/speaking/{session_id}`. Must meet the `<= 3s` target under normal load. |
| `TC-NFR-02` | **Audio Privacy** | `NFR-002` | Run a complete Speaking session and inspect `/tmp` and Cloudflare R2 buckets afterward. Temporary raw user audio buffers/files must be deleted immediately after session analysis. |
| `TC-NFR-03` | **Responsiveness** | `NFR-003` | Render all `[locale]` routes at desktop (`1440x900`) and mobile (`375x812`) viewports. No horizontal overflow, clipped controls, or overlapping cards. |
| `TC-NFR-04` | **Accessibility** | `NFR-005` | Run `axe-core` audit across main dashboard, Reading player, and AI Help drawer. Zero WCAG AA contrast, keyboard-focus, or ARIA violations. |
| `TC-NFR-05` | **Graceful Degradation** | `FR-072`–`FR-074`, `NFR-006` | Simulate LLM/STT/TTS timeout (`> 10s`). FastAPI must return `503 Service Unavailable` with error code `AI_UNAVAILABLE`; Next.js must preserve user input and display a **Retry** button; `/grammar`, `/vocabulary`, `/reading`, and `/listening` must remain 100% functional. |

---

## 5. Test Data & Exit Criteria

### 5.1 Test Data Management
- Seed data in `backend/seeds/` (JSON/YAML) must cover all CEFR levels (`A0`–`B2`), Armenian (`hy`) and Russian (`ru`) translations, reading `timestamps`, and song difficulty masks.
- Test audio fixtures (clean speech, noisy speech, accented/mispronounced speech, silence) should be stored in a dedicated test fixtures directory for repeatable Speaking pipeline runs.

### 5.2 Release Exit Criteria
- **100%** of `TC-AUTH`, `TC-CNT`, `TC-NFR-02` (Audio Privacy), and `TC-NFR-05` (Graceful Degradation) test cases pass.
- **0** critical or high-severity defects open.
- Speaking pipeline end-to-end latency meets `<= 3s` (`NFR-001`) in the target GPU deployment environment.
- No regressions in guest-to-registered data migration (`lewa_guest_state_v1`).
