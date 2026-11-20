Functional Requirements Document (FRD)
"Learn English with AI" System
•Document Version: 1.0
•Document Status: Preliminary Version
•Basis: Functional description provided by the user
•Supported Languages: Armenian and Russian interface support— a project requirement, the         details of which are yet to be specified
1. Purpose and General Description
The purpose of the system is to create an online English language learning platform that integrates educational materials, practical exercises, and support from artificial intelligence (AI).
The platform is designed to help users develop six core areas of English proficiency:
1.Grammar,
2.Vocabulary,
3.Listening,
4.Reading,
5.Writing,
6.Speaking.
Some of the educational materials will be prepared and compiled by the project author, while AI models will be utilized for certain tasks, explanations, assessments, and personalized recommendations.
AI models will be used for: For the Grammar component: after administering tests (to provide an overall assessment of topic mastery).
For the Vocabulary component: when creating daily study plans for registered users.
For the Writing component: when generating questions, sentences, and exercises, as well as when evaluating them and providing an overall assessment (using a model similar to the one applied in the Grammar component).
For the Speaking component: to facilitate voice-based interaction and practice with registered users, and to generate assessments of their existing skills (using models that evaluate Grammar and Pronunciation).
For registered users, the system should function as a
personalized online tutor: creating daily study plans, suggesting
exercises, evaluating responses, identifying strengths and weaknesses, and
recommending relevant learning materials.
2. Goals
The system shall:
•provide English learning materials for A0, A1, A2, B1, and B2 levels,
•ensure access to six core learning tracks,
•allow users to assess their knowledge through tests and assignments,
•track and display the user’s learning progress,
•provide explanations, feedback, and personalized recommendations with the help of AI,
•create a personalized daily study plan for registered users,
•allow for the customization of the interface language and layout.
3. Stakeholders and User Types
3.1. Unregistered User
An unregistered user may explore the platform, access available educational materials, and complete tasks for which registration is not required. Certain data regarding their progress must be stored in the browser's Local Storage.
3.2. Registered User
A registered user can save their learning history, access a personalized AI tutor, receive a daily plan, track their progress, analyze mistakes, and utilize features that require registration, including the Speaking section.
3.3. Person Responsible for System Content
The person responsible for content (the project author or an authorized individual) prepares and organizes the educational materials, topics, glossaries, and test questions. No specific requirements for a separate administrative panel are defined in the description.
3.4. AI Models
AI models support relevant learning paths by answering questions, creating or adapting tasks, checking the user's work, and providing analysis.
4. General structure of the system
The system's main navigation must provide access to the six learning tracks and the "Tests and Exams" section.
The "Learn English with AI" section, intended for registered users, must include the following subsections:
•Learning Path — completed lessons, topics, tests, answers, and learning statistics.
•User Progress — the user's progress and achievements, skills already well-mastered, and areas requiring further work.
•Mistake Analysis — a list of errors made by the user, along with an analysis of those errors.
•Review System — a review of previously covered material and past mistakes, featuring exercises and tests based on this content.
5. Functional Requirements
Requirement identifiers are used to uniquely designate each requirement. The phrasing "shall" describes the intended behavior of the system. Features that are noted in the initial description as potential or subject to discussion are marked as preliminary/subject to clarification.
5.1. Onboarding Questions and Proficiency Level Assessment
•FR-001. During the first visit, the system shall present the user with general questions regarding their English proficiency and their familiarity with the platform.
•FR-002. The screen containing these questions shall include a "Skip" button, allowing the user to bypass the questions.
•FR-003. The system shall invite the user to take an initial proficiency assessment test.
•FR-004. Based on the results of the initial test, the system shall determine the user's approximate current proficiency level and suggest an appropriate starting level.
•FR-005. Whether the completion of the onboarding questions and the assessment test is mandatory shall be defined during the design phase.
5.2. User Account and Data Storage
•FR-006. Certain learning data and completed stages for unregistered users must be stored in Local Storage.
•FR-007. The learning history and progress of registered users must be stored in such a way that they remain accessible during subsequent visits.
•FR-008. Features such as the personalized AI tutor, the individual daily plan, and the "Speaking" section must be available to registered users.
•FR-009. The specific methods for registration and login shall be defined during a separate phase of the project.
5.3. Interface and Navigation
•FR-010. The system shall include a common header providing access to the main educational sections and the "Tests and Exams" section.
•FR-011. The main page shall feature cards or other visible elements that allow the user to navigate to the corresponding section.
•FR-012. The system shall allow the interface language to be changed.
•FR-013. The user shall be able to customize the layout of interface elements by arranging buttons and sections in an order that suits them.
•FR-014. A relevant AI assistance button shall be available on the page for each educational track.
5.4. "Help Button" and AI Support
•FR-015. The user must be able to click the "Help button" and
open a separate communication window with the AI.
•FR-016. The AI must respond to questions related to the specific field of study.
•FR-017. For each field of study, a specialized AI model—or an AI service with appropriate configurations—shall be provided.
•FR-018. The AI's response should be aimed at clarifying the user's question
and facilitating a better grasp of the study material.
5.5. Grammar
•FR-019. Grammar materials must be categorized according to levels A0, A1, A2, B1, and B2.
•FR-020. Each topic page must present a general description of the topic, the rules, usage contexts, and examples.
•FR-021. Each grammar topic must include a test section to assess knowledge.
•FR-022. During the test, the system must display the questions and the user's responses.
•FR-023. The system must indicate which answers are correct and which are incorrect.
•FR-024. Upon completion of the test, the system must display the number or percentage of correct and incorrect answers.
•FR-025. The system must provide explanations for the answers, clarifying why a given answer is correct or incorrect.
•FR-026. The AI must be able to analyze test results and
provide a general conclusion regarding the user's strengths and weaknesses.
•FR-027. The grammar section should include a dedicated area for materials on synonyms and word usage, categorized by parts of speech.
•FR-028. Materials concerning synonyms must explain the semantic differences between words and the conditions for their use.
•FR-029. A "Frequently Asked Questions" (FAQ) section should be included on the pages dedicated to grammatical topics.
5.6. Vocabulary
•FR-030. Vocabulary materials must be presented in the form of glossaries/dictionaries.
•FR-031. It must be possible to view these glossaries according to language proficiency levels: A0,            A1, A2, B1, and B2.
•FR-032. Within level-based glossaries, words must be grouped by parts of speech—for example, nouns, verbs, and adjectives.
•FR-033. Thematic glossaries must also be provided—for example, covering topics such as daily life, emotions, communication, work, animals, colors, travel, food, transport, and hygiene.
•FR-034. Separate materials must be provided for phrasal verbs and idioms.
•FR-035. Example sentences must be displayed for words and expressions.
•FR-036. The AI must be able to suggest new words for the daily study plan, drawing from the available glossaries.
•FR-037. Newly learned words can be used in tasks within the Writing section.
•FR-038. A test to provide an approximate assessment of vocabulary proficiency level must be included.
•FR-039. Following the vocabulary test, the system must display the translations of the words and provide an option to listen to their pronunciation.
•FR-040. Example sentences and relevant images may be displayed for the words.
•FR-041. Users must be able to isolate or mark words that are unfamiliar to them and practice them later.
•FR-042. Vocabulary-learning games must be provided, including matching words with their translations, assembling words from individual letters, selecting the word that corresponds to an image, and determining whether an option is correct or incorrect.
5.7. Listening
•FR-043. The Listening section must include audio materials corresponding to levels A1, A2, B1, and B2.
•FR-044. The audio materials must cover various topics and types of sources—for example, everyday situations, cartoons, and excerpts from films.
•FR-045. The user must be able to listen to the material and answer questions related to it.
•FR-046. A grammatical and vocabulary analysis must be provided for the materials.
•FR-047. The analysis must present the verb tenses, vocabulary, expressions, and other linguistic elements used.
•FR-048. The analysis of the materials may be prepared by the person responsible for the content or with the assistance of AI.
5.8. Reading
•FR-049. The Reading section must contain texts corresponding to A1, A2, B1, and B2 proficiency levels.
•FR-050. Corresponding audio versions must be available for the texts.
•FR-051. While the audio is playing, the system must visually highlight the portion of the text currently being spoken.
•FR-052. Users must be able to click on a word in the text to view its translation.
•FR-053. It must be possible to listen to the pronunciation of a word.
•FR-054. The Reading section must include a separate subsection dedicated to books.
5.9. Writing
•FR-055. The Writing section must contain written tasks appropriate to the user's proficiency level.
•FR-056. At the A1 level, tasks should include translating simple sentences, constructing sentences from given words, and providing written accounts of what has been heard.
•FR-057. At the A2 level, similar types of tasks should be included, with a gradually increasing level of complexity.
•FR-058. At the B1 level, the scope should expand to include written responses regarding the user's daily routine, events, and preferred topics.
•FR-059. At the B2 level, the content should involve more in-depth questions, texts, and essays.
•FR-060. The AI must be capable of generating questions, sentences, and other written tasks that are appropriate to the user's proficiency level.
•FR-061. The AI must evaluate the user's written responses, assessing their grammar, vocabulary, and the overall quality of their writing.
•FR-062. For registered users, the AI must be able to
tailor task topics to the user's preferences.
•FR-063. The AI can suggest writing a text or an essay
using words learned during the current day or week.
5.10. Speaking
•FR-064. The "Speaking" section must be accessible to registered users.
•FR-065. The user must be able to record their speech using a recording button.
•FR-066. The user must be able to select or initiate a conversation topic and speak with the AI.
•FR-067. The AI must be able to respond via voice, facilitating the flow of the dialogue.
•FR-068. The AI must analyze the user's grammar and pronunciation.
•FR-069. After the conversation, the AI must provide feedback regarding identified issues, strengths, and suggestions for improvement.
•FR-070. The AI must be able to tailor conversation topics to the user's preferences.
5.11. Tests and Exams
•FR-071. There must be a separate "Tests and Exams" section within the system's main navigation.
•FR-072. The section must include grammar tests, covering topics such as verb tenses and parts of speech.
•FR-073. The section must include a test to provide an approximate assessment of the user's vocabulary level.
•FR-074. Users should be able to practice unfamiliar vocabulary, including through the use of games.
•FR-075. The possibility of including additional tests for the areas of Listening, Reading, Writing, and Speaking should be considered.
•FR-076. The possibility of adding tests for preparation for IELTS and TOEFL exams should be considered. The scope of this requirement and the phase for its implementation have not yet been defined.
5.12. Learning English through Songs
The purpose of this section is to simultaneously develop skills in Listening, Grammar, Vocabulary, and Writing through the use of songs, making the learning process more engaging and combining enjoyment with utility.
•FR-077. The system must include a dedicated section titled "Learning English through Songs."
•FR-078. For each song, there must be an option to listen, as well as a grammatical analysis that covers the grammatical structures used in the song and explains their application.
•FR-079. For each song, there must be an analysis of vocabulary and lexicon, presenting the words and expressions used along with their meanings.
•FR-080. By listening to songs and following their content, users should be able to develop their listening skills.
•FR-081. For each song, exercises involving filling in missing words must be provided, featuring three levels of difficulty.
The levels of difficulty should be distinguished by the number of missing words.
•FR-082. During the exercises, the user must listen to the song and fill in the missing words, thereby developing skills in transcribing what is heard and writing correctly.
•FR-083. The materials and tasks in the songs section must integrate four areas: Listening, Grammar, Vocabulary, and Writing.
5.13. AI Personal Tutor and Study Plan
•FR-084. The AI shall create an individual daily study plan for the registered user.
•FR-085. The daily plan shall include tasks from various fields of study.
•FR-086. The AI shall take into account the user’s current proficiency level, past performance, and strengths and weaknesses.
•FR-087. The AI shall consider the user’s preferences and topics of interest.
•FR-088. The AI shall evaluate the answers to the tasks included in the plan and provide feedback.
•FR-089. The AI shall suggest study materials based on the user’s needs and preferences.
•FR-090. The AI shall periodically suggest reviewing previously covered material and addressing past mistakes.
•FR-091. The AI shall be capable of generating tests based on the user’s previous mistakes.
5.14. Learning History and Progress
•FR-092. The "Learning Path" section must display the lessons, topics, and tests the user has completed, along with their corresponding answers.
•FR-093. The "Learning Path" section must display learning statistics and percentage-based results.
•FR-094. The "User Progress" section must present the user’s progress and achievements.
•FR-095. The "User Progress" section must highlight skills that have been well mastered, as well as areas that still require further work.
•FR-096. The "Mistake Analysis" section must display the errors made by the user.
•FR-097. The "Review System" section must allow the user to revisit previously covered material and complete new exercises based on their past mistakes.
•FR-098. During review sessions, the AI must be able to remind the user of topics that previously proved challenging.
6. Proficiency Levels and Content Guidelines
The system includes the following levels: A0, A1, A2, B1, and B2.
•A0: Designed to introduce fundamental grammar and basic vocabulary. Simple elements of listening, reading, writing, and speaking may be incorporated into the grammar and vocabulary materials.
•A1–B2: The volume and complexity of the materials should increase progressively.
•The core content for the Listening and Reading sections is intended for levels A1–B2.
•Writing tasks should increase in complexity in line with the progression of levels.
•The Speaking section must provide registered users with the opportunity to engage in free-form or topic-based dialogue with an AI.
7. Data Storage and Access Rules
1.Certain progress data for unregistered users is stored in Local Storage.
2.The learning history of a registered user must be stored in association with their account.
3.Features such as the personalized AI tutor and the daily plan are intended for registered users.
4.The "Speaking" section is available exclusively to registered users.
8. Non-functional Requirements
Presented below are the preliminary non-functional requirements derived from the functional description. Their measurable limits are to be defined during the technical design phase.
•NFR-001. Usability: The interface must be intuitive and user-friendly, allowing for easy navigation between learning sections.
•NFR-002. Customization: The user must be able to change the interface language and layout.
•NFR-003. Data Persistence: Saved learning progress must remain accessible to the user during subsequent visits, subject to the implemented data storage mechanism.
•NFR-004. Feedback: The results of tests and AI-based assessments must be presented in an understandable format.
•NFR-005. Linguistic Appropriateness: The complexity of learning materials and tasks must align with the specified proficiency level. 
•NFR-006. Audio and Recording: For Listening, Reading, and Speaking capabilities, the system must provide appropriate audio playback or recording functions.
•NFR-007. Integration of AI Services: AI capabilities must be structured in such a way that the relevant module can operate within the scope of its assigned learning track.
Detailed criteria regarding security, privacy, accessibility, performance, browser compatibility, and backup are not specified in the initial description and must be provided separately.
9. Main Use Cases
UC-01. First Visit
1.The user opens the platform.
2.The system presents initial questions.
3.The user answers the questions or selects "Skip."
4.The system suggests taking a proficiency level assessment test.
5.Upon completion of the test, the system displays the estimated proficiency level and recommends a starting learning path.
UC-02. Studying a Grammar Topic
1.The user opens the Grammar section.
2.The user selects a level and a topic.
3.The user studies the rules and examples.
4.The user takes the test for the topic.
5.The system displays the correct and incorrect answers, the result, and explanations.
6.The AI can provide a general analysis.
UC-03. Using AI Assistance
1.The user is in one of the learning sections.
2.The user clicks the "Help" button.
3.The AI communication window opens.
4.The user enters their question.
5.The relevant AI model provides an explanation.
UC-04. Vocabulary Study
1.The user opens the "Vocabulary" section.
2.The user selects a level-based or thematic vocabulary list.
3.The user studies the words, their translations, and examples.
4.The user listens to the pronunciation of the words.
5.The user identifies unfamiliar words.
6.The user completes exercises or plays games based on these words.
UC-05. Completing the Personalized Daily Plan
1.A registered user opens the "Learn English with AI" section.
2.The system displays the personalized daily plan.
3.The user completes the suggested tasks.
4.The AI checks the answers and provides feedback.
5.The results are recorded in the user's learning history and progress tracking.
UC-06. Oral Conversation with AI
1.A registered user opens the "Speaking" section.
2.The user selects or suggests a topic for conversation.
3.The user presses the recording button and speaks. 4.	The AI responds via voice.
5.After the conversation, the AI provides observations regarding pronunciation and grammar.
10. Preliminary Limitations and Out-of-Scope Items
The points listed below are not final decisions; they must be clarified during the requirements validation and technical design phases.
1.Specific mechanisms for registration, login, and account recovery.
2.Selection of AI models, their quantity, APIs, and usage limitations.
3.The precise algorithm for generating the daily study plan and the number of tasks.
4.Structure of the proficiency placement test and the grading scale.
5.Whether all sections will be accessible without registration, or if some will be restricted.
6.Sources for listening and reading materials, including copyright and usage permission issues.
7.Legal and content-related restrictions regarding the use of song lyrics.
8.Inclusion of IELTS and TOEFL preparation tests and the phase for their implementation. 
9.Are other languages planned, in addition to Armenian and Russian?
10.The method for saving a customized user interface layout.
11.AI evaluation criteria and methods for verifying the accuracy of results.
12.Policies regarding data security, privacy, and the storage of recordings.




