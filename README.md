# AI-DLC Lite Plugin for Claude Code

A lightweight, speed-optimized version of the AI-Driven Development Lifecycle methodology.

AI-DLC Lite follows the same three-phase lifecycle as the [full AI-DLC plugin](https://github.com/ijin/aidlc-cc-plugin), but reduces overhead at every stage: fewer questions, bounded follow-ups, single approval gates, and reasonable defaults for low-impact decisions.

## Installation

First, add the marketplace to your Claude Code (one-time setup):

```bash
/plugin marketplace add ijin/aidlc-lite-cc-plugin
```

Then install the plugin:

```bash
/plugin install aidlc-lite@aidlc-lite-cc-plugin
```

## Quick Start

Start a new AI-DLC Lite workflow:

```bash
/aidlc-lite:start Develop a recommendation engine for cross-selling products
```

Or resume an existing session:

```bash
/aidlc-lite:start
```

Claude will automatically detect your previous session (via `aidlc-docs/aidlc-state.md`) and offer to resume where you left off.

## How It Works

AI-DLC Lite guides you through a three-phase adaptive workflow:

```
User Request
    |
    v
+--INCEPTION PHASE---------------------------+
| Workspace Detection      [ALWAYS]          |
| Reverse Engineering       [CONDITIONAL]    |
| Requirements Analysis    [ALWAYS]          |
| User Stories              [CONDITIONAL]    |
| Workflow Planning        [ALWAYS]          |
| Application Design        [CONDITIONAL]    |
| Units Generation          [CONDITIONAL]    |
+--------------------------------------------+
    |
    v
+--CONSTRUCTION PHASE------------------------+
| Per-Unit Loop:                             |
|   Functional Design       [CONDITIONAL]    |
|   NFR Requirements        [CONDITIONAL]    |
|   NFR Design              [CONDITIONAL]    |
|   Infrastructure Design   [CONDITIONAL]    |
|   Code Generation        [ALWAYS]          |
| Build and Test           [ALWAYS]          |
+--------------------------------------------+
    |
    v
+--OPERATIONS PHASE--------------------------+
| Operations                [PLACEHOLDER]    |
+--------------------------------------------+
```

### What Makes Lite Different?

| Aspect | Full AI-DLC | AI-DLC Lite |
|---|---|---|
| Questioning depth | Exhaustive | Targeted — focuses on high-impact questions |
| Follow-up rounds | Unlimited | One round max; documents assumptions and moves on |
| Approval checkpoints | Two per multi-part stage | One per stage |
| Default behavior | Asks when in doubt | Applies reasonable defaults for low-impact decisions |

**What is preserved**: Approval gates, audit logging, state tracking, code location rules, brownfield file modification rules, and the three-phase lifecycle structure.

### Key Principles

**Adaptive Workflow** -- Stages execute only when they add value. Simple changes skip unnecessary planning.

**User Control** -- Approve execution plans before work begins. Request changes at any approval gate.

**Complete Audit Trail** -- All decisions logged with timestamps in `aidlc-docs/audit.md`.

**Chat-Based Interaction** -- Answer questions directly in conversation. No file editing required.

**Speed Over Depth** -- Get to working code faster without sacrificing correctness.

## Managing Artifacts

AI-DLC creates documentation in the `aidlc-docs/` directory:

```
<workspace-root>/
+-- [your application code]
+-- aidlc-docs/
    +-- aidlc-state.md           # Progress tracking
    +-- aidlc-preferences.md     # Q&A style preference
    +-- audit.md                 # Audit trail
    +-- inception/
    |   +-- reverse-engineering/  # (brownfield only, 2 consolidated files)
    |   +-- requirements/
    |   +-- user-stories/         # (if executed)
    |   +-- application-design/   # (if executed)
    +-- construction/
    |   +-- {unit-name}/
    |   |   +-- functional-design/
    |   |   +-- nfr-requirements/
    |   |   +-- nfr-design/
    |   |   +-- infrastructure-design/
    |   |   +-- code/
    |   +-- build-and-test/
    +-- operations/               # (placeholder)
```

## When to Use Lite vs Full AI-DLC

| Use AI-DLC Lite when... | Use Full AI-DLC when... |
|---|---|
| Requirements are clear and well-understood | Requirements are ambiguous and need extensive discovery |
| You want to move quickly | You want thorough exploration of every edge case |
| Scope is straightforward | Complex integrations or regulatory constraints |
| You prefer fewer questions and reasonable defaults | You prefer exhaustive clarification at every stage |

Both can be used for production work. Choose based on the complexity and risk of the task.

## Examples

### Greenfield Project
```bash
/aidlc-lite:start Build a REST API for managing customer subscriptions with Stripe integration
```

### Brownfield Enhancement
```bash
/aidlc-lite:start Add user authentication with OAuth2 to the existing API
```

### Simple Bug Fix
```bash
/aidlc-lite:start Fix the race condition in the payment processing queue
```

## Acknowledgments

This plugin is adapted from the [AI-DLC Lite](https://github.com/awslabs/sample-aidlc-lite) reference implementation, a lightweight variant of the [AWS AI-DLC Workflows](https://github.com/awslabs/aidlc-workflows). Originally designed for Amazon Q Developer / Kiro CLI, it has been adapted for Claude Code's plugin system with chat-based interaction patterns.

For more information about AI-DLC methodology, see:
- [AI-DLC Methodology Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [AI-DLC Open-source Launch Blog](https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/)
- [AI-DLC Example Walkthrough Blog](https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/)

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-improvement`)
3. Make your changes
4. Test thoroughly with `claude --plugin-dir .`
5. Submit a pull request

## License

This project is licensed under MIT-0 - see the [LICENSE](LICENSE) file for details.
