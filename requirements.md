# Requirements Document

## Introduction

LearnFlow AI is a real-time, dual-mode AI platform that provides personalized learning assistance and code debugging support. The system acts as an intelligent tutor for students learning programming concepts and as a debugging assistant for developers fixing code issues. The platform uses sentiment analysis to detect user confusion and adapts its teaching approach through progressive hints, flashcard generation, and customizable learning styles.

## Glossary

- **LearnFlow_System**: The complete AI platform including backend logic, API, and user interface
- **Student**: A user learning new programming concepts such as Python or Data Structures and Algorithms
- **Developer**: A user seeking assistance with debugging broken code
- **AI_Engine**: The backend logic powered by Gemini API that analyzes user input and generates responses
- **Learning_Mode**: An operational mode where the system explains concepts using analogies and interactive examples
- **Debugging_Mode**: An operational mode where the system accepts code input and identifies errors through progressive hints
- **Confusion_Level**: A computed metric based on sentiment analysis indicating user understanding (Low, Medium, High)
- **Hint_Ladder**: A three-tier progressive hint system (Conceptual, Syntax, Solution)
- **Flashcard**: A learning object containing an error description (front) and its correction (back)
- **Learning_Style**: A user preference for how information is presented (ELI5, Visual, Standard)
- **Session_History**: A persistent record of user interactions, flashcards, and learning progress

## Requirements

### Requirement 1: Dual-Mode Operation

**User Story:** As a user, I want to switch between learning and debugging modes, so that I can receive appropriate assistance based on my current task.

#### Acceptance Criteria

1. THE LearnFlow_System SHALL support two distinct operational modes: Learning_Mode and Debugging_Mode
2. WHEN a user selects Learning_Mode, THE LearnFlow_System SHALL configure the AI_Engine to provide conceptual explanations with analogies and examples
3. WHEN a user selects Debugging_Mode, THE LearnFlow_System SHALL configure the AI_Engine to analyze code and provide progressive hints
4. WHEN a user switches modes, THE LearnFlow_System SHALL preserve the Session_History and maintain context continuity
5. THE LearnFlow_System SHALL display the current active mode to the user at all times

### Requirement 2: Real-Time Sentiment Analysis and Confusion Detection

**User Story:** As a student, I want the system to detect when I'm confused, so that it can automatically simplify explanations and help me understand better.

#### Acceptance Criteria

1. WHEN a user sends a message, THE LearnFlow_System SHALL analyze the sentiment of that message in real-time
2. WHEN sentiment analysis indicates negative sentiment or repeated similar questions, THE LearnFlow_System SHALL classify the Confusion_Level as High
3. IF the Confusion_Level is High, THEN THE LearnFlow_System SHALL generate a simplified explanation using basic vocabulary and concrete examples
4. IF the Confusion_Level is High, THEN THE LearnFlow_System SHALL update the UI badge indicator to red
5. WHEN the Confusion_Level returns to Low or Medium, THE LearnFlow_System SHALL restore the UI badge indicator to its normal state
6. THE LearnFlow_System SHALL track Confusion_Level changes throughout the session for adaptive learning

### Requirement 3: Progressive Hint Ladder for Debugging

**User Story:** As a developer, I want to receive progressive hints instead of immediate solutions, so that I can learn to debug code independently.

#### Acceptance Criteria

1. WHEN a user requests help in Debugging_Mode, THE LearnFlow_System SHALL generate three progressive hints without immediately revealing the complete solution
2. THE LearnFlow_System SHALL generate a Conceptual_Hint that explains the logical error without referencing specific code
3. THE LearnFlow_System SHALL generate a Syntax_Hint that provides the line number and relevant keyword where the error occurs
4. THE LearnFlow_System SHALL generate a Solution_Hint that contains the corrected code
5. WHEN a user requests the next hint, THE LearnFlow_System SHALL reveal hints sequentially in order: Conceptual, Syntax, then Solution
6. THE LearnFlow_System SHALL prevent skipping hint levels unless explicitly requested by the user

### Requirement 4: Automatic Flashcard Generation

**User Story:** As a student, I want the system to automatically create flashcards from my mistakes, so that I can review and reinforce my learning later.

#### Acceptance Criteria

1. WHEN the AI_Engine detects a user mistake or syntax error, THE LearnFlow_System SHALL automatically generate a Flashcard object
2. THE Flashcard SHALL contain the error description on the front side
3. THE Flashcard SHALL contain the correction explanation on the back side
4. WHEN a Flashcard is generated, THE LearnFlow_System SHALL save it to the user's Session_History immediately
5. THE LearnFlow_System SHALL associate each Flashcard with a timestamp and the context in which it was created
6. THE LearnFlow_System SHALL allow users to retrieve and review all generated Flashcards from their Session_History

### Requirement 5: Adaptive Learning Styles

**User Story:** As a user with specific learning preferences, I want to customize how information is presented to me, so that I can learn in the way that works best for me.

#### Acceptance Criteria

1. WHERE a user selects ELI5_Style, THE LearnFlow_System SHALL restrict vocabulary to simple, everyday terms and use basic analogies
2. WHERE a user selects Visual_Style, THE LearnFlow_System SHALL include ASCII diagrams, visual metaphors, or structured representations in responses
3. WHERE a user selects Standard_Style, THE LearnFlow_System SHALL use technical terminology appropriate for the topic
4. WHEN a user changes their Learning_Style preference, THE LearnFlow_System SHALL apply the new style to all subsequent responses immediately
5. THE LearnFlow_System SHALL persist the user's Learning_Style preference across sessions

### Requirement 6: Code Input and Analysis

**User Story:** As a developer, I want to submit my broken code for analysis, so that I can identify and fix errors with guided assistance.

#### Acceptance Criteria

1. WHEN a user is in Debugging_Mode, THE LearnFlow_System SHALL accept code input in multiple programming languages
2. WHEN code is submitted, THE AI_Engine SHALL analyze the code for syntax errors, logical errors, and runtime issues
3. WHEN errors are detected, THE LearnFlow_System SHALL categorize each error by type (syntax, logic, runtime)
4. THE LearnFlow_System SHALL identify the specific line numbers where errors occur
5. WHEN multiple errors exist, THE LearnFlow_System SHALL prioritize errors by severity and present them in order

### Requirement 7: Concept Explanation in Learning Mode

**User Story:** As a student, I want clear explanations of programming concepts, so that I can build a strong foundational understanding.

#### Acceptance Criteria

1. WHEN a user requests a concept explanation in Learning_Mode, THE LearnFlow_System SHALL generate a response that includes a definition, analogy, and practical example
2. THE LearnFlow_System SHALL adapt explanation complexity based on the detected Confusion_Level
3. WHEN explaining Data Structures and Algorithms, THE LearnFlow_System SHALL include time and space complexity information
4. THE LearnFlow_System SHALL provide interactive code examples that users can modify and test
5. WHEN a concept builds on prerequisite knowledge, THE LearnFlow_System SHALL identify and offer to explain those prerequisites first

### Requirement 8: Session Management and History

**User Story:** As a user, I want my learning progress and interactions to be saved, so that I can continue where I left off and track my improvement over time.

#### Acceptance Criteria

1. THE LearnFlow_System SHALL create a unique Session_History for each user
2. WHEN a user interacts with the system, THE LearnFlow_System SHALL record all messages, mode changes, and generated content in the Session_History
3. THE LearnFlow_System SHALL persist Session_History data across user sessions
4. WHEN a user returns to the platform, THE LearnFlow_System SHALL load their previous Session_History and restore context
5. THE LearnFlow_System SHALL allow users to export their Session_History including all Flashcards and interactions

### Requirement 9: Real-Time API Integration

**User Story:** As a system administrator, I want the platform to integrate with the Gemini API efficiently, so that responses are generated quickly and reliably.

#### Acceptance Criteria

1. THE LearnFlow_System SHALL integrate with the Gemini API for natural language processing and code analysis
2. WHEN a user sends a request, THE LearnFlow_System SHALL transmit the request to the Gemini API within 100 milliseconds
3. WHEN the Gemini API returns a response, THE LearnFlow_System SHALL process and display it to the user within 500 milliseconds
4. IF the Gemini API request fails, THEN THE LearnFlow_System SHALL retry the request up to three times with exponential backoff
5. IF all retry attempts fail, THEN THE LearnFlow_System SHALL display a user-friendly error message and log the failure details

### Requirement 10: FastAPI Backend Architecture

**User Story:** As a developer, I want a well-structured FastAPI backend, so that the system is maintainable, scalable, and follows best practices.

#### Acceptance Criteria

1. THE LearnFlow_System SHALL implement the backend using FastAPI framework
2. THE LearnFlow_System SHALL expose RESTful API endpoints for mode selection, message submission, hint requests, and flashcard retrieval
3. WHEN an API endpoint receives a request, THE LearnFlow_System SHALL validate the request payload against defined schemas
4. IF request validation fails, THEN THE LearnFlow_System SHALL return a 400 status code with descriptive error details
5. THE LearnFlow_System SHALL implement proper error handling and return appropriate HTTP status codes for all scenarios
6. THE LearnFlow_System SHALL support CORS configuration to allow frontend integration
