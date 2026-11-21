# Functional Requirements Document (FRD)
## "Learn English with AI" System

- **Document Version:** 1.1
- **Document Status:** Updated Draft (Post-Review)
- **Basis:** Functional description provided by the project author and stakeholder clarifications
- **Supported Interface Languages:** Armenian (`hy`), Russian (`ru`), and English (`en`)

---

## 1. Purpose and General Description

The purpose of the system is to create an online English language learning platform that integrates structured educational materials, practical exercises, and artificial intelligence (AI) support.

The platform is designed to help users develop six core areas of English proficiency:
1. Grammar
2. Vocabulary
3. Listening
4. Reading
5. Writing
6. Speaking

Core educational materials will be prepared and curated by the project author, while AI models will be utilized for contextual assistance, task generation, automated evaluation, and personalized recommendations.

### AI Model Responsibilities by Module
- **Grammar:** Analyzing test results to provide an overall assessment of topic mastery and identifying weak areas.
- **Vocabulary:** Selecting and recommending new words for daily study plans for registered users.
- **Writing:** Generating level-appropriate questions, sentences, and prompts, as well as evaluating user responses and providing overall feedback.
- **Speaking:** Facilitating voice-based interaction and dialogue with registered users, and evaluating grammar and pronunciation.
- **Contextual Help:** Answering user questions within the context of the active learning section or exercise.

For registered users, the system functions as a personalized online tutor: generating daily study plans, recommending exercises, evaluating responses, identifying strengths and weaknesses, and scheduling reviews of past mistakes.

---

## 2. Goals

The system shall:
- Provide English learning materials for levels **A0** (Grammar and Vocabulary) and **A1, A2, B1, B2** (all core tracks).
- Ensure access to the six core learning tracks plus "Learning English through Songs" and "Tests and Exams".
- Allow users to assess their knowledge through topic tests and comprehensive level-based exams.
- Track and display the user's learning progress, strengths, and areas for improvement.
- Provide explanations, feedback, and personalized recommendations using AI.
- Generate a personalized daily study plan for registered users.
- Support interface localization (Armenian, Russian, English) and customizable main-page card ordering via drag-and-drop.

---

## 3. Stakeholders and User Types

### 3.1. Unregistered User (Guest)
An unregistered user may explore the platform, access open educational materials (Grammar, Vocabulary, Listening, Reading, Songs, and Tests), and complete tasks that do not require an account. Progress data for unregistered users is stored in the browser's `Local Storage` and migrated to their account upon registration.

### 3.2. Registered User
A registered user has full access to persistent learning history, profile preferences, the personalized AI tutor, daily study plans, mistake analysis, review sessions, and registration-only features such as the Speaking section.

### 3.3. Content Administrator (Project Author)
The person responsible for content prepares and organizes educational materials, topics, glossaries, audio/text sources, and test questions.
- **Phase 1 (MVP):** Content is managed via structured data files or database seed scripts.
- **Phase 2:** A dedicated Admin/CMS panel will be introduced for creating, editing, and publishing materials.

### 3.4. AI Services
External or self-hosted AI models that support learning paths by answering contextual questions, generating/adapting exercises, evaluating written and spoken responses, and analyzing user performance.

---

## 4. General System Structure and Access Matrix

### 4.1. Main Navigation
The system's main navigation shall provide access to:
- The six core learning tracks: **Grammar**, **Vocabulary**, **Listening**, **Reading**, **Writing**, **Speaking**
- **Learning English through Songs**
- **Tests and Exams**
- **My Learning Space** (for registered users)

### 4.2. "My Learning Space" Subsections (Registered Users)
To avoid confusion with the platform name, the registered user's personal area is titled **My Learning Space** and includes:
- **Learning Path:** Completed lessons, topics, tests, submitted answers, and learning statistics.
- **User Progress:** Progress metrics, achievements, mastered skills, and areas requiring further work.
- **Mistake Analysis:** A categorized log of errors made by the user with AI-assisted explanations.
- **Review System:** Spaced/targeted review of previously covered material and past mistakes with newly generated practice tasks.
- **Profile & Preferences:** Account settings, interface language, target proficiency level, and topics of interest.

### 4.3. Feature Access Matrix

| Feature / Module | Unregistered User | Registered User | Notes |
| :--- | :---: | :---: | :--- |
| Onboarding & Placement Test | Yes | Yes | Progress saved in `Local Storage` for guests |
| Grammar (Materials & Topic Tests) | Yes | Yes | AI post-test summary for registered users |
| Vocabulary (Glossaries & Games) | Yes | Yes | Unfamiliar word lists synced upon registration |
| Listening & Reading | Yes | Yes | Full access to A1–B2 materials |
| Learning English through Songs | Yes | Yes | Full access to lyrics, analysis, and gap-fill tasks |
| Tests and Exams (Comprehensive) | Yes | Yes | Results saved to account or `Local Storage` |
| Writing (Tasks & AI Evaluation) | Limited (Tasks only) | Full (with AI Evaluation) | AI evaluation requires registration |
| AI Help Button (Contextual Chat) | Limited / Rate-limited | Yes | Context-aware assistance |
| Speaking (Voice Dialogue with AI) | No | Yes | Registration required |
| My Learning Space & Daily Plan | No | Yes | Registration required |

---

## 5. Functional Requirements

Each requirement has a unique identifier and a target implementation phase:
- **Phase 1 (MVP):** Core platform functionality required for initial launch.
- **Phase 2:** Extended features planned after the initial release.

### 5.1. Onboarding Questions and Proficiency Level Assessment
- **FR-001 [Phase 1]:** During the first visit, the system shall present the user with onboarding questions regarding their English proficiency and familiarity with the platform.
- **FR-002 [Phase 1]:** The onboarding screen shall include a "Skip" button allowing the user to bypass the questions.
- **FR-003 [Phase 1]:** The system shall invite the user to take an initial proficiency placement test.
- **FR-004 [Phase 1]:** Based on the placement test results, the system shall estimate the user's current proficiency level (A0–B2) and recommend a starting level.

### 5.2. User Account, Profile, and Data Storage
- **FR-005 [Phase 1]:** The system shall support user registration, login, logout, and password recovery (via email/password or OAuth).
- **FR-006 [Phase 1]:** For unregistered users, completed lessons, test scores, unfamiliar vocabulary marks, and UI layout preferences shall be stored in browser `Local Storage`.
- **FR-007 [Phase 1]:** When an unregistered user registers or logs in, the system shall automatically migrate their existing `Local Storage` progress into their user account.
- **FR-008 [Phase 1]:** Registered users shall have a **Profile & Preferences** page to manage their display name, interface language, target proficiency level, and preferred conversation/writing topics (e.g., technology, travel, business).
- **FR-009 [Phase 1]:** Features such as the personalized AI tutor, daily study plan, AI writing evaluation, and the Speaking section shall be restricted to registered users.

### 5.3. Interface, Localization, and Navigation
- **FR-010 [Phase 1]:** The system shall include a persistent header providing navigation to all main learning sections, "Learning English through Songs", "Tests and Exams", and "My Learning Space" (when authenticated).
- **FR-011 [Phase 1]:** The main page shall display interactive cards for each learning section.
- **FR-012 [Phase 1]:** The system shall allow the user to switch the interface language between **Armenian (`hy`)**, **Russian (`ru`)**, and **English (`en`)**.
- **FR-013 [Phase 1]:** The user shall be able to customize the order of the section cards on the main page using **drag-and-drop**, with the custom order persisted in `Local Storage` (for guests) or the user profile (for registered users).
- **FR-014 [Phase 1]:** An AI "Help" button shall be accessible on every learning track page.

### 5.4. Contextual AI "Help" Button
- **FR-015 [Phase 1]:** Clicking the "Help" button shall open a chat drawer/modal for communicating with the AI assistant.
- **FR-016 [Phase 1]:** The AI assistant shall be **context-aware**, receiving metadata about the user's current section, proficiency level, and active topic or exercise.
- **FR-017 [Phase 1]:** The AI shall answer questions related to the active study material, providing clear explanations and examples.
- **FR-018 [Phase 1]:** Unregistered users shall be subject to a configurable rate limit on AI Help queries (or prompted to register after exceeding the limit).

### 5.5. Grammar
- **FR-019 [Phase 1]:** Grammar materials shall be categorized by proficiency levels: **A0, A1, A2, B1, and B2**.
- **FR-020 [Phase 1]:** Each grammar topic page shall present a general description, grammatical rules, usage contexts, and example sentences.
- **FR-021 [Phase 1]:** Each grammar topic shall include a topic-level practice test.
- **FR-022 [Phase 1]:** During the test, the system shall display questions and capture user responses.
- **FR-023 [Phase 1]:** Upon submission, the system shall highlight correct and incorrect answers, display the score and percentage, and provide explanations for why each answer is correct or incorrect.
- **FR-024 [Phase 1]:** For registered users, the AI shall analyze completed grammar test results and provide a summary of strengths and weaknesses.
- **FR-025 [Phase 1]:** The Grammar section shall include a dedicated subsection for **synonyms and word usage**, categorized by parts of speech, explaining semantic differences and usage conditions.
- **FR-026 [Phase 1]:** Grammar topic pages shall include a "Frequently Asked Questions" (FAQ) section.

### 5.6. Vocabulary
- **FR-027 [Phase 1]:** Vocabulary materials shall be presented as structured glossaries/dictionaries.
- **FR-028 [Phase 1]:** Glossaries shall be filterable by proficiency levels **A0, A1, A2, B1, and B2**, and grouped within each level by parts of speech (e.g., nouns, verbs, adjectives).
- **FR-029 [Phase 1]:** Thematic glossaries shall be provided (e.g., daily life, emotions, communication, work, animals, colors, travel, food, transport, hygiene).
- **FR-030 [Phase 1]:** Separate glossaries shall be provided for **phrasal verbs** and **idioms**.
- **FR-031 [Phase 1]:** Each word or expression shall display example sentences, audio pronunciation, and translations corresponding to the selected interface language (**Armenian** or **Russian**; when **English** interface is selected, English definitions/synonyms shall be shown, with an option to toggle HY/RU translation).
- **FR-032 [Phase 1]:** Users shall be able to bookmark/mark unfamiliar words and practice them later in dedicated review lists.
- **FR-033 [Phase 1]:** The AI shall select new words from available glossaries for registered users' daily study plans (`FR-076`), and newly learned words shall be reusable in Writing tasks.
- **FR-034 [Phase 1]:** The Vocabulary section shall include a vocabulary assessment test that displays word translations, pronunciation audio, and example sentences upon completion.
- **FR-035 [Phase 1]:** Basic vocabulary-learning games shall be provided (matching words with translations, true/false selection).
- **FR-036 [Phase 2]:** Advanced interactive vocabulary games (assembling words from individual letters, image-to-word matching) shall be added.

### 5.7. Listening
- **FR-037 [Phase 1]:** The Listening section shall provide audio materials for levels **A1, A2, B1, and B2** (note: A0 is covered via basic pronunciation in Grammar/Vocabulary).
- **FR-038 [Phase 1]:** Audio materials shall cover everyday situations, educational dialogues, and licensed/public-domain/TTS-generated clips.
- **FR-039 [Phase 1]:** Users shall be able to play/pause audio, adjust playback speed, and answer comprehension questions related to the audio.
- **FR-040 [Phase 1]:** Each listening material shall include a grammatical and vocabulary breakdown (verb tenses, key vocabulary, expressions) prepared by the content author or assisted by AI.

### 5.8. Reading
- **FR-041 [Phase 1]:** The Reading section shall provide texts categorized by levels **A1, A2, B1, and B2**.
- **FR-042 [Phase 1]:** Corresponding audio versions (pre-recorded or TTS with word/sentence timestamps) shall be available for each text.
- **FR-043 [Phase 1]:** While audio plays, the system shall visually highlight the currently spoken sentence or segment in real time.
- **FR-044 [Phase 1]:** Users shall be able to click any word in the text to view its translation (in the active interface language) and listen to its pronunciation.
- **FR-045 [Phase 1]:** The Reading section shall include a dedicated **Books** subsection featuring adapted/graded readers or public-domain books.

### 5.9. Writing
- **FR-046 [Phase 1]:** The Writing section shall provide tasks for levels **A1, A2, B1, and B2**:
  - **A1:** Translating simple sentences, constructing sentences from given words, writing short summaries of audio clips.
  - **A2:** Progressively more complex sentence construction and short descriptive responses.
  - **B1:** Written responses about daily routines, events, and user-selected topics.
  - **B2:** In-depth analytical questions, structured texts, and essays.
- **FR-047 [Phase 1]:** The AI shall generate level-appropriate writing prompts and tasks.
- **FR-048 [Phase 1]:** For registered users, the AI shall evaluate written submissions—assessing grammar, vocabulary, coherence, and overall quality—and provide actionable feedback.
- **FR-049 [Phase 1]:** For registered users, the AI shall tailor writing topics to the user's profile preferences (`FR-008`) and optionally prompt them to use words learned during the current day or week.

### 5.10. Speaking
- **FR-050 [Phase 1]:** The Speaking section shall be accessible exclusively to registered users.
- **FR-051 [Phase 1]:** The user shall be able to select a suggested topic, propose a custom topic, or use topics tailored to their profile preferences (`FR-008`) to start a conversation with the AI.
- **FR-052 [Phase 1]:** The user shall be able to record their speech via a microphone recording button (with clear visual recording indicators).
- **FR-053 [Phase 1]:** The AI shall respond via synthesized voice (TTS) to maintain a natural conversational flow.
- **FR-054 [Phase 1]:** After the conversation, the AI shall analyze the user's speech and provide feedback on grammar, pronunciation, strengths, and areas for improvement.

### 5.11. Tests and Exams
- **FR-055 [Phase 1]:** The "Tests and Exams" section shall serve as the central hub for **comprehensive and level-based exams** (A0–B2) rather than duplicating individual topic quizzes.
- **FR-056 [Phase 1]:** It shall include comprehensive Grammar exams (covering multiple verb tenses and parts of speech) and Vocabulary level-estimation exams.
- **FR-057 [Phase 2]:** Comprehensive exams for Listening, Reading, Writing, and Speaking shall be added.
- **FR-058 [Phase 2]:** Preparation mock tests for **IELTS** and **TOEFL** exams shall be added.

### 5.12. Learning English through Songs
- **FR-059 [Phase 1]:** The system shall include a "Learning English through Songs" section integrating Listening, Grammar, Vocabulary, and Writing.
- **FR-060 [Phase 1]:** Each song entry shall provide audio playback (via licensed/embedded player), a grammatical analysis of structures used in the lyrics, and a vocabulary/idiom breakdown.
- **FR-061 [Phase 1]:** Each song shall include fill-in-the-blank lyrics exercises with **three difficulty levels** determined by the percentage/number of missing words.
- **FR-062 [Phase 1]:** Users shall listen to the song and type the missing words, receiving immediate feedback on spelling and accuracy.

### 5.13. AI Personal Tutor and Daily Study Plan
- **FR-063 [Phase 1]:** For registered users, the AI shall generate an individualized daily study plan comprising tasks across multiple learning tracks.
- **FR-064 [Phase 1]:** The daily plan shall adapt to the user's current proficiency level, past performance, strengths/weaknesses, and profile preferences (`FR-008`).
- **FR-065 [Phase 1]:** The AI shall evaluate answers to daily plan tasks, provide feedback, and update the user's progress metrics.
- **FR-066 [Phase 1]:** The AI shall periodically schedule review tasks based on previously covered material and past mistakes, and generate targeted review tests.

### 5.14. Learning History and Progress ("My Learning Space")
- **FR-067 [Phase 1]:** **Learning Path** shall display completed lessons, topics, tests, submitted answers, and percentage-based statistics.
- **FR-068 [Phase 1]:** **User Progress** shall display overall progress, achievements, mastered skills, and weak areas.
- **FR-069 [Phase 1]:** **Mistake Analysis** shall list errors made across sections along with explanations.
- **FR-070 [Phase 1]:** **Review System** shall allow users to revisit past topics, complete new exercises generated from their mistakes, and receive AI reminders on challenging topics.

### 5.15. Content Management (Admin / CMS)
- **FR-071 [Phase 2]:** An Admin/CMS panel shall be provided for authorized content administrators to create, edit, categorize (A0–B2), and publish Grammar, Vocabulary, Listening, Reading, Song, and Exam content without code deployments.

### 5.16. Error Handling and Edge Cases
- **FR-072 [Phase 1]:** If an AI service is unavailable, times out, or returns an invalid response, the system shall display a user-friendly error message with a "Retry" option and preserve the user's unsaved input.
- **FR-073 [Phase 1]:** In the Speaking section, if microphone permissions are denied or no audio input is detected, the system shall display clear instructions on enabling microphone access and prevent empty submissions.
- **FR-074 [Phase 1]:** If audio playback fails to load in Listening, Reading, or Songs, the system shall display a fallback notification and allow retrying without losing exercise progress.

---

## 6. Proficiency Levels and Content Guidelines

- **A0 (Absolute Beginner):** Covers foundational grammar and basic vocabulary only.
- **A1 (Beginner):** Simple grammar, core vocabulary, short listening clips, basic reading texts, and guided sentence writing.
- **A2 (Elementary):** Increasing complexity across all six tracks.
- **B1 (Intermediate):** Conversational fluency, everyday/workplace topics, paragraph writing, and multi-part listening/reading.
- **B2 (Upper-Intermediate):** Complex grammar, idioms/phrasal verbs, essays, and in-depth speaking/listening materials.

---

## 7. Non-Functional Requirements (NFRs)

- **NFR-001 (Performance & Latency):**
  - Standard page transitions and static content loads shall complete within **2 seconds** on a standard broadband connection.
  - Text-based AI responses (Help chat, Writing evaluation) shall begin streaming or return within **5 seconds** (95th percentile).
  - Voice-based AI responses in Speaking shall complete within **3 seconds** after speech end detection.
- **NFR-002 (Security & Privacy):**
  - All client-server communication shall be encrypted using **HTTPS/TLS**.
  - User passwords shall be hashed using a modern algorithm (e.g., `bcrypt` or `Argon2`).
  - Voice recordings in the Speaking section shall be processed securely, and users shall be informed of retention policies (recordings deleted after analysis unless explicitly saved).
- **NFR-003 (Responsive Design & Mobile Compatibility):**
  - The web application shall be fully responsive across desktop (`>= 1024px`), tablet (`768px–1023px`), and mobile (`360px–767px`) viewports.
- **NFR-004 (Browser Compatibility):**
  - The platform shall support the latest two major versions of Google Chrome, Mozilla Firefox, Apple Safari, and Microsoft Edge, including Web Audio / MediaRecorder APIs for Speaking.
- **NFR-005 (Accessibility):**
  - The UI shall follow **WCAG 2.1 Level AA** guidelines where practical (keyboard navigation, sufficient color contrast, ARIA labels for audio controls and drag-and-drop cards).
- **NFR-006 (Reliability & Availability):**
  - Core non-AI learning sections (Grammar, Vocabulary, Reading, Listening) shall remain functional even if external AI services experience temporary downtime.

---

## 8. Main Use Cases

### UC-01: First Visit and Onboarding
- **Actor:** Unregistered User
- **Preconditions:** User has no existing session or `Local Storage` onboarding flag.
- **Main Flow:**
  1. User opens the platform.
  2. System presents initial onboarding questions.
  3. User answers the questions (or clicks "Skip").
  4. System invites the user to take the placement test.
  5. Upon completion, system displays the estimated level (A0–B2) and recommends a starting path, saving the state in `Local Storage`.
- **Alternative Flow:** If the user skips both onboarding and placement test, the system defaults to showing all levels starting from A0/A1.

### UC-02: Studying a Grammar Topic
- **Actor:** Unregistered or Registered User
- **Preconditions:** User navigates to the Grammar section.
- **Main Flow:**
  1. User selects a proficiency level (A0–B2) and a topic.
  2. User reads the rules, usage contexts, examples, and FAQ.
  3. User completes the topic test.
  4. System displays correct/incorrect indicators, percentage score, and answer explanations.
  5. *(Registered User)* AI generates a summary of strengths and weaknesses and updates Learning Path.

### UC-03: Using Contextual AI Help
- **Actor:** Unregistered or Registered User
- **Preconditions:** User is on any learning track page.
- **Main Flow:**
  1. User clicks the "Help" button.
  2. System opens the AI chat window pre-loaded with the current page/exercise context.
  3. User submits a question.
  4. AI responds with a contextual explanation.
- **Exception Flow:** If the AI service fails, system displays a retry prompt (`FR-072`). If an unregistered user hits the rate limit, system prompts them to register.

### UC-04: Vocabulary Study and Unfamiliar Word Review
- **Actor:** Unregistered or Registered User
- **Main Flow:**
  1. User opens Vocabulary and selects a level-based or thematic glossary.
  2. User views words, translations (in active interface language), examples, and listens to pronunciation.
  3. User marks unfamiliar words.
  4. User practices marked words via vocabulary games.

### UC-05: Listening and Reading with Synchronized Audio
- **Actor:** Unregistered or Registered User
- **Main Flow:**
  1. User opens Listening or Reading and selects an A1–B2 material.
  2. User plays the audio; in Reading, the system highlights the spoken text segment in real time.
  3. User clicks unfamiliar words in Reading to view translations and hear pronunciation.
  4. User answers comprehension questions and reviews the grammar/vocabulary breakdown.

### UC-06: Writing Task with AI Evaluation
- **Actor:** Registered User
- **Preconditions:** User is logged in.
- **Main Flow:**
  1. User opens Writing and selects their level (A1–B2) or accepts an AI-generated prompt tailored to their preferences.
  2. User writes and submits their response.
  3. AI evaluates grammar, vocabulary, and coherence, returning detailed feedback.
  4. System logs any mistakes into **Mistake Analysis**.

### UC-07: Oral Conversation with AI (Speaking)
- **Actor:** Registered User
- **Preconditions:** User is logged in and grants microphone permission.
- **Main Flow:**
  1. User opens Speaking and selects or enters a conversation topic.
  2. User presses the record button and speaks.
  3. AI processes the speech and responds via voice.
  4. After ending the session, AI provides feedback on pronunciation and grammar.
- **Exception Flow:** If microphone access is denied, system displays browser permission instructions (`FR-073`).

### UC-08: Learning English through Songs
- **Actor:** Unregistered or Registered User
- **Main Flow:**
  1. User opens "Learning English through Songs" and selects a song.
  2. User reviews the grammar and vocabulary breakdown.
  3. User selects one of three difficulty levels and plays the song.
  4. User fills in the missing lyrics and submits for immediate feedback.

### UC-09: Completing the Daily Study Plan and Reviewing Mistakes
- **Actor:** Registered User
- **Preconditions:** User is logged in.
- **Main Flow:**
  1. User opens **My Learning Space** and views today's AI-generated daily plan.
  2. User completes tasks across assigned tracks.
  3. AI evaluates responses and updates **User Progress** and **Learning Path**.
  4. User visits **Mistake Analysis** or **Review System** to practice past errors.

---

## 9. Preliminary Limitations and Technical Decisions to Finalize

1. **AI Provider Selection:** Specific LLM, Speech-to-Text (STT), and Text-to-Speech (TTS) providers, token/cost budgets, and rate-limiting thresholds.
2. **Authentication Mechanism:** Selection of auth providers (email/password, Google/Apple OAuth) and session token strategy.
3. **Content Licensing:** Verification of public-domain, TTS, or licensed API sources (e.g., YouTube IFrame API) for Reading books, Listening clips, and Song lyrics/audio.
4. **Daily Plan Algorithm:** Exact weighting and task count formulas for the spaced-repetition and daily plan generator.
5. **Placement Test Scoring:** Exact question count and rubric mapping test scores to levels A0–B2.
