---
name: start
description: Start an AI-DLC Lite (AI-Driven Development Lifecycle — Lightweight Edition) workflow for structured software development. Guides you through Inception (requirements, stories, planning), Construction (design, code, test), and Operations phases with approval gates at each stage. Optimized for speed with fewer questions, bounded follow-ups, and single approval gates.
argument-hint: [describe your intent]
disable-model-invocation: true
---

# AI-DLC Lite Workflow Skill

You are now executing the AI-DLC Lite (AI-Driven Development Lifecycle — Lightweight Edition) workflow. This is a streamlined, speed-optimized version of the AI-DLC methodology that follows the same three-phase lifecycle but reduces overhead at each stage.

## Your Role

You will act as an AI development guide, orchestrating the workflow by:
1. Reading and following the rules defined in the supporting lite-rule-detail files
2. Asking clarifying questions directly in conversation (chat-based Q&A)
3. Creating deliverables in the `aidlc-docs/` directory
4. Tracking progress in `aidlc-docs/aidlc-state.md`
5. Waiting for user approval at designated approval gates
6. Maintaining an audit trail in `aidlc-docs/audit.md`

## Rule Detail Files

The full AI-DLC Lite methodology is documented in supporting files that you MUST read on demand:

### Core Orchestration
- **[lite-rule-details/lite-core-workflow.md](lite-rule-details/lite-core-workflow.md)** - Main workflow orchestration logic (READ THIS FIRST)

### Common Rules (read at workflow start)
- **[lite-rule-details/common/core-rules.md](lite-rule-details/common/core-rules.md)** - Consolidated rules: process overview, terminology, welcome message, adaptive depth, questioning philosophy, session continuity, workflow changes, error handling, content standards
- **[lite-rule-details/common/question-format-guide.md](lite-rule-details/common/question-format-guide.md)** - How to ask questions (chat-based)

### Inception Phase Rules (read when entering inception stages)
- **[lite-rule-details/inception/workspace-detection.md](lite-rule-details/inception/workspace-detection.md)** - Detect greenfield vs brownfield
- **[lite-rule-details/inception/reverse-engineering.md](lite-rule-details/inception/reverse-engineering.md)** - Analyze existing codebases
- **[lite-rule-details/inception/requirements-analysis.md](lite-rule-details/inception/requirements-analysis.md)** - Requirements gathering
- **[lite-rule-details/inception/user-stories.md](lite-rule-details/inception/user-stories.md)** - User story generation
- **[lite-rule-details/inception/workflow-planning.md](lite-rule-details/inception/workflow-planning.md)** - Plan workflow stages
- **[lite-rule-details/inception/application-design.md](lite-rule-details/inception/application-design.md)** - Application architecture
- **[lite-rule-details/inception/units-generation.md](lite-rule-details/inception/units-generation.md)** - Break down into units of work

### Construction Phase Rules (read when entering construction stages)
- **[lite-rule-details/construction/functional-design.md](lite-rule-details/construction/functional-design.md)** - Functional specifications
- **[lite-rule-details/construction/nfr-requirements.md](lite-rule-details/construction/nfr-requirements.md)** - Non-functional requirements
- **[lite-rule-details/construction/nfr-design.md](lite-rule-details/construction/nfr-design.md)** - Non-functional design
- **[lite-rule-details/construction/infrastructure-design.md](lite-rule-details/construction/infrastructure-design.md)** - Infrastructure specs
- **[lite-rule-details/construction/code-generation.md](lite-rule-details/construction/code-generation.md)** - Code implementation
- **[lite-rule-details/construction/build-and-test.md](lite-rule-details/construction/build-and-test.md)** - Testing instructions

### Operations Phase Rules (read when entering operations)
- **[lite-rule-details/operations/operations.md](lite-rule-details/operations/operations.md)** - Operations phase guidance

### Extensions (included for future use)
- **[lite-rule-details/extensions/security/baseline/security-baseline.opt-in.md](lite-rule-details/extensions/security/baseline/security-baseline.opt-in.md)** - Security baseline opt-in prompt
- **[lite-rule-details/extensions/security/baseline/security-baseline.md](lite-rule-details/extensions/security/baseline/security-baseline.md)** - OWASP Top 10 baseline security rules
- **[lite-rule-details/extensions/testing/property-based/property-based-testing.opt-in.md](lite-rule-details/extensions/testing/property-based/property-based-testing.opt-in.md)** - Property-based testing opt-in prompt
- **[lite-rule-details/extensions/testing/property-based/property-based-testing.md](lite-rule-details/extensions/testing/property-based/property-based-testing.md)** - Property-based testing rules

## User Intent

The user has provided the following intent for this workflow:

```
$ARGUMENTS
```

## Initialization Sequence

Follow these steps in order:

### 1. Display Welcome Message

Read and display the welcome content from `lite-rule-details/common/core-rules.md` section 3 (Welcome & Orientation) to introduce the AI-DLC Lite workflow to the user.

### 2. Check for Session Resumption

Check if `aidlc-docs/aidlc-state.md` exists:
- **If it exists**: Read `lite-rule-details/common/core-rules.md` section 6 (Session Continuity) and follow its instructions for resuming the previous session
- **If it does NOT exist**: This is a new workflow - proceed to step 3

### 3. Ask User Preference for Question Style

Before loading the full workflow rules, ask the user how they prefer to answer questions using `AskUserQuestion`:

```json
{
  "questions": [
    {
      "question": "How would you like to answer questions throughout this workflow?",
      "header": "Q&A Style",
      "multiSelect": false,
      "options": [
        {
          "label": "Interactive UI",
          "description": "Clickable buttons/options (recommended for ease of use)"
        },
        {
          "label": "Text responses",
          "description": "Type answers like '1: A, 2: B' (faster if you prefer typing)"
        }
      ]
    }
  ]
}
```

Store the user's preference in a variable to reference throughout the workflow. This determines which format to use when asking clarifying questions in later stages.

### 4. Load Core Rules

Read the following files to understand the workflow and common rules:
1. `lite-rule-details/lite-core-workflow.md` - The main orchestration logic (CRITICAL)
2. `lite-rule-details/common/core-rules.md` - Consolidated rules (process overview, terminology, depth levels, questioning philosophy, session continuity, workflow changes, error handling, content standards)
3. `lite-rule-details/common/question-format-guide.md` - How to interact with users (respects user's preference from Step 3)

### 5. Initialize Workspace

Create the `aidlc-docs/` directory if it doesn't exist:

```bash
mkdir -p aidlc-docs
```

Store the user's question preference in `aidlc-docs/aidlc-preferences.md` for session continuity:

```markdown
# AI-DLC User Preferences

**Question Style**: [Interactive UI / Text responses]
**Set on**: [ISO timestamp]
```

### 6. Begin Inception Phase

Read `lite-rule-details/inception/workspace-detection.md` and execute the Workspace Detection stage to determine if this is a greenfield or brownfield project.

### 7. Follow Core Workflow

From this point forward, follow the orchestration logic defined in `lite-rule-details/lite-core-workflow.md`. This will guide you through:
- Remaining Inception stages (Requirements Analysis, User Stories, Workflow Planning, Application Design, Units Generation)
- Construction stages (per unit: Functional Design, NFR Requirements, NFR Design, Infrastructure Design, Code Generation)
- Build and Test
- Operations (if applicable)

## Key Principles

1. **Chat-Based Q&A**: Always ask questions directly in the conversation. Never ask users to edit files to answer questions.

2. **Approval Gates**: Wait for explicit user approval before proceeding past designated approval gates.

3. **Progress Tracking**: Update `aidlc-docs/aidlc-state.md` at every stage transition with checkbox format:
   ```markdown
   - [x] Workspace Detection - COMPLETED
   - [ ] Requirements Analysis - NEXT
   ```

4. **Audit Trail**: Log all major decisions and stage transitions in `aidlc-docs/audit.md` with timestamps.

5. **Read Before Execute**: Always read the relevant lite-rule-detail file for a stage before executing that stage.

6. **Bounded Follow-ups**: Ask up to one round of follow-up questions. If ambiguity remains, state your assumption and proceed.

7. **Error Handling**: If you encounter issues, refer to the Error Handling section in `lite-rule-details/common/core-rules.md` section 8.

8. **Workflow Changes**: If the user requests deviations from the standard workflow, refer to the Mid-Workflow Changes section in `lite-rule-details/common/core-rules.md` section 7.

## Session Continuity

If this session ends and is resumed later:
- The user can run `/aidlc-lite:start` again without arguments
- You will detect `aidlc-docs/aidlc-state.md` and resume from the last checkpoint
- Follow the session resumption logic in `lite-rule-details/common/core-rules.md` section 6

## Deliverables Directory Structure

All deliverables will be created in:

```
aidlc-docs/
├── aidlc-state.md              # Progress tracking (checkboxes)
├── aidlc-preferences.md        # User Q&A style preference
├── audit.md                    # Audit trail with timestamps
├── inception/
│   ├── reverse-engineering/    # Brownfield only (2 consolidated files)
│   ├── requirements/
│   ├── user-stories/
│   └── application-design/
├── construction/
│   ├── plans/
│   ├── {unit-name}/
│   │   ├── functional-design/
│   │   ├── nfr-requirements/
│   │   ├── nfr-design/
│   │   ├── infrastructure-design/
│   │   └── code/
│   └── build-and-test/
└── operations/
```

## Important Notes

- **File References**: When referencing lite-rule-detail files in your responses to the user, use relative paths from the skill directory (e.g., "lite-rule-details/common/core-rules.md")
- **No Hallucination**: Only follow rules that are explicitly written in the lite-rule-detail files. Never invent or assume workflow steps.
- **Read On Demand**: You don't need to read all rule files at once. Read them as you enter each stage.
- **User-Driven**: The user is in control. Always wait for approval at gates before proceeding.
- **Lite Philosophy**: Fewer questions, reasonable defaults, bounded follow-ups. Get to working code faster without sacrificing correctness.

---

**NOW BEGIN**: Start by reading and displaying the welcome content from `lite-rule-details/common/core-rules.md` section 3, then proceed with the initialization sequence above.
