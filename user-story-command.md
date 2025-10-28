# User Story Development Command

You will be provided with a user story number (e.g., "03") as an argument. Your task is to analyze, plan, and incrementally implement that user story following the workflow below.

## Workflow

### Phase 1: Analysis & Planning (Automatic)
1. **Locate the Story**: Read the file `/user-stories/$ARGUMENTS.md` where $ARGUMENTS is the story number provided
2. **Analyze Requirements**: Review the user story description, requirements, and any existing context
3. **Check Dependencies**: Review related code, database models, and existing features that will be affected
4. **Create Refinement Section**: Add a `## Refinement` section to the story file with:
   - Technical analysis of requirements
   - Database schema changes needed (if any)
   - API/route changes needed (if any)
   - Frontend changes needed (if any)
   - Dependencies on existing code
   - Potential risks or challenges
   - Questions or clarifications needed (if any)
5. **Create Planning Section**: Add a `## Planning` section with:
   - Ordered task list breaking down the work into small increments
   - Each task should be testable independently
   - Tasks organized by phase (e.g., Database, Backend, Frontend, Testing)
   - Estimated complexity (Simple/Medium/Complex) for each task
6. **Present Plan**: Show the user the Refinement and Planning sections and **WAIT for user confirmation before proceeding**

### Phase 2: Incremental Implementation (After User Approval)
7. **Never start coding without explicit user confirmation**
8. **Implement one task at a time** from the Planning section:
   - Mark the current task as "in progress" using TodoWrite
   - Implement the task with clean, well-documented code
   - Test the implementation manually or with provided tests
   - Mark the task as complete
   - **STOP and show the user what was done**
9. **Wait for user feedback** after each increment:
   - User may test the feature
   - User may request changes
   - User may approve and ask to continue
10. **Update Implementation Section**: As you complete tasks, update the `## Implementation` section with:
    - High-level summary of what was implemented
    - Key technical decisions made
    - Any deviations from the original plan
    - Files modified/created with line references
    - **DO NOT include actual code snippets** - just references and descriptions

## Story File Format

The user story file should follow this structure:

```markdown
# User Story XX: [Title]

## User Story
As a [role] I want [feature] so that [benefit]

## Requirements
- Requirement 1
- Requirement 2
...

## Refinement
### Technical Analysis
- Database changes: ...
- Backend changes: ...
- Frontend changes: ...
- Dependencies: ...

### Risks & Challenges
- Challenge 1: ...
- Challenge 2: ...

### Open Questions
- Question 1: ...

## Planning
### Phase 1: Database Layer (if needed)
- [ ] Task 1 (Simple) - Description
- [ ] Task 2 (Medium) - Description

### Phase 2: Backend API
- [ ] Task 3 (Medium) - Description
- [ ] Task 4 (Complex) - Description

### Phase 3: Frontend UI
- [ ] Task 5 (Simple) - Description

### Phase 4: Testing & Polish
- [ ] Task 6 (Simple) - Description

## Implementation
### Summary
Brief description of what was implemented

### Key Changes
- [file.py:123](file.py#L123) - Description of change
- [template.html:45-67](template.html#L45-L67) - Description of change

### Technical Decisions
- Decision 1: Rationale
- Decision 2: Rationale

## Implementation Status
🟡 **In Progress** - [Brief status update]
or
🟢 **Completed** - [Brief completion summary]
```

## Important Rules

1. **Never start coding without user confirmation** - always present the plan first
2. **Small increments** - each task should be small enough to test in 1-5 minutes
3. **Frequent feedback** - stop after each increment and wait for user input
4. **Update the story file** - keep the user story file updated as you progress
5. **Use TodoWrite** - track tasks using the TodoWrite tool during implementation
6. **File references** - always use markdown link format: `[file.py:123](file.py#L123)`
7. **No code in story file** - the story file is documentation, not a code repository

## Example Usage

User runs: `/user-story 03`

You should:
1. Read `/user-stories/03.md`
2. Analyze the requirements and codebase
3. Add Refinement and Planning sections to the file
4. Present the plan to the user
5. Wait for confirmation with message: "I've analyzed user story 03 and created a detailed plan. Please review the Refinement and Planning sections in [user-stories/03.md](user-stories/03.md). Would you like me to proceed with implementation?"
6. Only after user says "yes" or "proceed" or similar, start implementing incrementally

$ARGUMENTS