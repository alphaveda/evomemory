EvoMemory: Enhanced Memory System for LLMs
Overview
EvoMemory is a hybrid memory system designed to exponentially improve LLM performance by providing structured, persistent, and adaptive context management. It combines human-readable Markdown files stored locally with JSON-based cloud storage for scalability.
Memory Structure
EvoMemory organizes memory into core files, optional context files, and a learning journal, stored locally in a memory-bank/ directory and synced to a cloud database.
flowchart TD
    PB[projectbrief.md] --> PC[productContext.md]
    PB --> SP[systemPatterns.md]
    PB --> TC[techContext.md]
    PB --> SM[summary.json]
    
    PC --> AC[activeContext.md]
    SP --> AC
    TC --> AC
    
    AC --> P[progress.md]
    AC --> LJ[learningJournal.json]
    
    SM --> LJ

Core Files (Required)

projectbrief.md

Defines project scope, goals, and high-level requirements.
Created at project initialization.
Example:# Project Brief
**Name**: TaskMaster
**Goal**: Build a task management app with real-time collaboration.
**Scope**: Web app with React frontend, Node.js backend, and MongoDB.
**Stakeholders**: Developers, PMs, end-users.




productContext.md

Describes the problem, user needs, and desired experience.
Example:# Product Context
**Problem**: Teams struggle with task coordination.
**Solution**: Real-time task board with notifications.
**UX Goals**: Intuitive, fast, accessible.




activeContext.md

Tracks current focus, recent changes, and next steps.
Example:# Active Context
**Current Focus**: Implement user authentication.
**Recent Changes**: Added OAuth2 login (2025-06-03).
**Next Steps**: Test login flow, add password reset.




systemPatterns.md

Documents architecture, design patterns, and component relationships.
Example:# System Patterns
**Architecture**: MVC
**Patterns**: Singleton for DB connection, Observer for notifications.
**Components**: Frontend (React), Backend (Express), DB (MongoDB).




techContext.md

Lists technologies, setup, constraints, and dependencies.
Example:# Technical Context
**Stack**: React 18, Node.js 20, MongoDB 7.
**Constraints**: Must support IE11.
**Dependencies**: axios, mongoose.




progress.md

Summarizes completed work, pending tasks, and issues.
Example:# Progress
**Completed**: Task creation UI, API endpoints.
**Pending**: Real-time sync, testing.
**Issues**: Slow API response on large datasets.




summary.json

Auto-generated summary of all core files for quick LLM context loading.
Stored locally and in the cloud.
Example:{
  "projectName": "TaskMaster",
  "summary": "Task management app with real-time collaboration, using React, Node.js, and MongoDB.",
  "currentFocus": "User authentication",
  "lastUpdated": "2025-06-04T12:30:00Z"
}




learningJournal.json

Dynamic record of project-specific patterns, preferences, and insights.
Example:{
  "patterns": [
    {"id": "1", "description": "Use async/await for API calls", "added": "2025-06-02"},
    {"id": "2", "description": "User prefers Tailwind CSS", "added": "2025-06-03"}
  ],
  "preferences": {"codeStyle": "ESLint Standard", "testing": "Jest"}
}





Optional Context Files

Stored in memory-bank/context/ (e.g., features.md, apis.md, tests.md).
Created as needed for complex projects.
Synced to cloud as JSON records.

Storage

Local: Markdown files in memory-bank/ for human readability and offline access.
Cloud: JSON records in a database (e.g., MongoDB or vector store) for scalability and retrieval.
Syncing: Automatic two-way sync when online, with conflict resolution via versioning.

Core Workflows
Initialization

Create memory-bank/ directory and core files if they don’t exist.
Generate summary.json and learningJournal.json.
Sync to cloud (if enabled).

flowchart TD
    Start[New Project] --> Create[Create memory-bank/]
    Create --> Init[Initialize Core Files]
    Init --> Summary[Generate summary.json]
    Summary --> Journal[Create learningJournal.json]
    Journal --> Sync[Sync to Cloud]

Reading Memory

Load summary.json for quick context.
Read core Markdown files if deeper context is needed.
Query learningJournal.json for patterns/preferences.
Fetch additional context files as required.

flowchart TD
    Start[Task Start] --> LoadSummary[Load summary.json]
    LoadSummary --> CheckDepth{Need Details?}
    CheckDepth -->|Yes| ReadCore[Read Core Markdown]
    CheckDepth -->|No| ReadJournal[Read learningJournal.json]
    ReadCore --> ReadJournal
    ReadJournal --> FetchContext[Fetch Optional Context]
    FetchContext --> Process[Process Task]

Updating Memory

Triggered by significant changes, user requests (update memory), or new patterns.
Review all core files and update relevant ones.
Regenerate summary.json.
Append to learningJournal.json.
Sync to cloud with versioned updates.

flowchart TD
    Start[Update Trigger] --> Review[Review All Files]
    Review --> UpdateFiles[Update Relevant Files]
    UpdateFiles --> Regen[Regenerate summary.json]
    Regen --> Append[Append to learningJournal.json]
    Append --> Sync[Sync to Cloud]

Planning Mode
See EvoMemory_Planning_Mode.md for details.
Learning Journal
The learningJournal.json evolves with the project, capturing:

Coding patterns (e.g., “Always use async/await for APIs”).
User preferences (e.g., “Prefers TypeScript over JavaScript”).
Project challenges (e.g., “Database queries slow on large datasets”).
Tool usage (e.g., “Use Prettier for formatting”).

Update Process

Identify new patterns during task execution.
Validate with user (if needed).
Append to learningJournal.json with timestamp and unique ID.
Apply patterns to future tasks.

flowchart TD
    Start[New Pattern] --> Identify[Identify Pattern]
    Identify --> Validate[Validate with User]
    Validate --> Append[Append to learningJournal.json]
    Append --> Apply[Apply in Future Tasks]

Versioning and Syncing

Local: Store version history in memory-bank/versions/ (e.g., projectbrief_v1.md).
Cloud: Use a database with versioned records (e.g., MongoDB with timestamps).
Conflict Resolution: Prioritize latest timestamp; prompt user if conflicts arise.

Best Practices

Clarity: Write concise, clear Markdown for human readers; use JSON for machine efficiency.
Consistency: Update summary.json and learningJournal.json after every task.
Scalability: Limit core file size; offload details to optional context files.
Security: Encrypt cloud data; maintain local backups.
Extensibility: Allow custom file types (e.g., YAML, TOML) via configuration.

Implementation Notes

Use Markdown for local files to ensure human readability.
Use JSON for cloud storage and summary.json/learningJournal.json for fast parsing.
Implement a lightweight CLI or API for memory management (e.g., evo init, evo sync).
Support vector embeddings for semantic search in large memory banks (future enhancement).


