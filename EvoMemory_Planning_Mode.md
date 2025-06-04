EvoMemory Planning Mode
Overview
EvoMemory's Planning Mode is a robust, adaptable workflow designed to generate actionable plans for any project type (e.g., software development, animation, content creation, business planning). It leverages EvoMemory’s modular memory structure to provide context-aware planning, ensuring flexibility, scalability, and alignment with user preferences. The mode dynamically analyzes project context, asks clarifying questions, and creates phased plans that adapt to project complexity and domain.
Workflow
The Planning Mode follows a structured process to ensure universal applicability:
flowchart TD
  Start[Enter Planning Mode] --> Analyze[Analyze Memory & Project]
  Analyze --> IdentifyType[Identify Project Type]
  IdentifyType --> LoadContext[Load Relevant Context]
  LoadContext --> GenerateQuestions[Generate 5-7 Questions]
  GenerateQuestions --> UserInput[Collect User Responses]
  UserInput --> DraftPlan[Draft Phased Plan]
  DraftPlan --> ValidatePlan[Validate with Memory]
  ValidatePlan --> Approve{User Approves?}
  Approve -->|Yes| Execute[Execute Phase]
  Approve -->|No| Revise[Revise Plan]
  Execute --> UpdateMemory[Update Memory]
  UpdateMemory --> NextPhase{Next Phase?}
  NextPhase -->|Yes| Execute
  NextPhase -->|No| Complete[Complete Task]

Detailed Steps

Analyze Memory & Project:

Read summary.json for a quick overview.
Load projectbrief.md for goals and scope.
Check learningJournal.json for patterns (e.g., “User prefers Python for automation”).
Scan progress.md and activeContext.md for current status.
Identify project type (e.g., software, creative, business) from projectbrief.md metadata or user input.


Identify Project Type:

Extract keywords from projectbrief.md (e.g., “React” for software, “Blender” for animation, “marketing” for business).
If unclear, prompt: “What type of project is this (e.g., software development, animation, content creation)?”
Use learningJournal.json to infer preferences (e.g., Python for scripting).


Load Relevant Context:

Fetch domain-specific files (e.g., techContext.md for software, features.md for creative projects).
Prioritize recent entries in activeContext.md and progress.md.
Flag missing context for question generation.


Generate 5–7 Questions:

Base questions on:
Project Type: Software (tech stack, dependencies), creative (tools, assets), business (goals, audience).
Gaps in Memory: Missing details in projectbrief.md or techContext.md.
Complexity: Simple projects (e.g., Python script) need fewer questions; complex projects (e.g., full-stack app) need more.


Example Questions:
Software: “What’s the primary tech stack? Any specific frameworks or libraries?”
Animation: “Are there specific Blender tools or render settings you prefer?”
Content: “What’s the target audience? Any preferred tone or style?”




Collect User Responses:

Present questions clearly, referencing memory files.
Store responses in activeContext.md.


Draft Phased Plan:

Break tasks into phases with dependencies (e.g., “Complete API setup before frontend integration”).
Include timelines and resources based on techContext.md and learningJournal.json.
Example Plan (Software):# Task: Build User Authentication
## Phase 1: Setup
- Install dependencies (e.g., bcrypt, JWT).
- Configure database (MongoDB).
## Phase 2: Backend
- Create login/register endpoints.
- Implement token generation.
## Phase 3: Frontend
- Build login UI (React).
- Connect to backend.
## Phase 4: Testing
- Write unit tests (Jest).
- Test login flow.


Example Plan (Animation):# Task: Create 3D Character
## Phase 1: Concept
- Define character design.
## Phase 2: Modeling
- Create base mesh in Blender.
## Phase 3: Rigging
- Add bones and controls.
## Phase 4: Animation
- Create keyframe animations.
## Phase 5: Rendering
- Set up lighting and render settings.




Validate with Memory:

Cross-check plan against systemPatterns.md and techContext.md.
Ensure alignment with learningJournal.json patterns.


User Approval:

Present plan in Markdown format.
Ask: “Does this plan meet your needs? Any adjustments required?”
Revise based on feedback.


Execute Phase:

Execute each phase using tools/preferences from learningJournal.json.
Generate code, scripts, or workflows as needed.


Update Memory:

Update progress.md (e.g., “Completed login endpoints”).
Update activeContext.md with focus and next steps.
Regenerate summary.json.
Append patterns to learningJournal.json.


Iterate or Complete:

Loop back for remaining phases or finalize memory updates.



Pseudocode
def planning_mode(task_description):
    # Analyze Memory
    summary = load_json("memory-bank/summary.json")
    project_brief = load_markdown("memory-bank/projectbrief.md")
    learning_journal = load_json("memory-bank/learningJournal.json")
    progress = load_markdown("memory-bank/progress.md")
    active_context = load_markdown("memory-bank/activeContext.md")
    
    # Identify Project Type
    project_type = extract_project_type(project_brief, user_input)
    
    # Load Relevant Context
    context_files = select_context_files(project_type, ["techContext.md", "systemPatterns.md"])
    context_data = [load_markdown(f) for f in context_files]
    
    # Generate Questions
    questions = generate_questions(project_type, context_data, task_description, learning_journal)
    user_responses = prompt_user(questions)
    
    # Draft Phased Plan
    plan = create_phased_plan(task_description, user_responses, context_data, learning_journal)
    
    # Validate Plan
    if not validate_plan(plan, context_data):
        plan = revise_plan(plan, context_data)
    
    # User Approval
    while not user_approves(plan):
        plan = revise_plan(plan, prompt_user(["What needs adjustment?"]))
    
    # Execute Phases
    for phase in plan.phases:
        execute_phase(phase, learning_journal)
        update_memory(phase, progress, active_context, summary, learning_journal)
    
    # Complete
    finalize_memory(progress, active_context, summary)
    return "Task completed, memory updated."

def generate_questions(project_type, context_data, task, journal):
    questions = []
    if project_type == "software":
        questions.append("What’s the primary tech stack?")
        if not context_data["dependencies"]:
            questions.append("Are there specific dependencies required?")
    elif project_type == "animation":
        questions.append("What Blender tools or settings do you prefer?")
        if not context_data["assets"]:
            questions.append("Are there existing assets to use?")
    # Add more based on gaps and journal patterns
    return questions[:7]

def create_phased_plan(task, responses, context, journal):
    plan = {"phases": []}
    # Dynamically generate phases based on task, responses, and context
    return plan

Example Applications

Software Project (Python Web App):

Task: “Build a task management API.”
Questions: “Which framework (e.g., Flask, FastAPI)? Database preferences? Authentication requirements?”
Plan: Setup (install FastAPI), Backend (create endpoints), Testing (Pytest), Deployment (Docker).
Memory Updates: Add FastAPI to techContext.md, update progress.md.


Animation Project (Blender Character):

Task: “Create a 3D character for a game.”
Questions: “Character style (realistic, cartoon)? Blender add-ons? Render engine?”
Plan: Concept (sketch design), Modeling (mesh), Rigging (bones), Animation (keyframes), Rendering (Cycles).
Memory Updates: Add Blender preferences to learningJournal.json, update progress.md.


Content Project (Blog Post):

Task: “Write a blog post on AI trends.”
Questions: “Target audience? Preferred tone? Specific topics?”
Plan: Research (gather trends), Outline (structure), Draft (write), Edit (proofread), Publish (WordPress).
Memory Updates: Add tone preference to learningJournal.json, update activeContext.md.



MCP Integration
Planning Mode integrates with Model Context Protocol (MCP) servers by:

Querying memory via API endpoints (e.g., fetch summary.json).
Sending plans to the MCP server for execution (e.g., Python scripts, Blender tasks).
Updating memory via API calls for cloud sync.

Notes

Universal Applicability: The mode adapts to any project by analyzing projectbrief.md and learningJournal.json.
Scalability: Splits complex tasks into sub-plans, stored in optional context files.
Error Handling: Prompts user for missing context or initializes files as needed.


