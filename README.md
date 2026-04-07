# Superpowers for Hermes

Superpowers is a complete software development methodology and skill library that works natively with Hermes Agent. All skills have been audited and updated to use explicit Hermes tool calls (`write_file`, `read_file`, `terminal`, `patch`, `search_files`, `delegate_task`) instead of generic descriptions or shell commands.

## Overview

Superpowers provides a systematic approach to software development that ensures code quality, test coverage, and reliable delivery. The workflow emphasizes:

- **Test-Driven Development (TDD)** - RED-GREEN-REFACTOR cycle
- **Declarative Planning** - Break work into bite-sized tasks before coding
- **Evidence-Based Development** - Verify before declaring success
- **Parallel Execution** - Dispatch independent tasks concurrently
- **Two-Stage Review** - Spec compliance, then code quality

## How It Works

Superpowers skills are loaded automatically by Hermes when their triggers are detected. Each skill provides:

- Clear objectives and success criteria
- Step-by-step instructions with explicit tool usage
- Tool examples showing correct syntax
- Common pitfalls and how to avoid them

## Skills Library

All 13 skills below are **Hermes-native** - they explicitly use Hermes tools:

### Planning Skills

| Skill | Description |
|--------|-------------|
| [brainstorming](./superpowers-brainstorming/) | Refines rough ideas through Socratic questioning, explores alternatives, presents design for validation |
| [writing-plans](./superpowers-writing-plans/) | Creates comprehensive implementation plans with bite-sized tasks (2-5 min each), exact file paths, and complete code examples |

### Execution Skills

| Skill | Description |
|--------|-------------|
| [subagent-driven-development](./superpowers-subagent-driven-development/) | Dispatches fresh subagent per task with two-stage review (spec compliance → code quality). Supports parallel dispatch for independent tasks |
| [executing-plans](./superpowers-executing-plans/) | Batch execution of plans in current session with verification checkpoints |
| [test-driven-development](./superpowers-test-driven-development/) | Enforces RED-GREEN-REFACTOR: write test first, watch it fail, write minimal code |
| [systematic-debugging](./superpowers-systematic-debugging/) | 4-phase root cause investigation: trace → analyze → test → verify |

### Review Skills

| Skill | Description |
|--------|-------------|
| [requesting-code-review](./superpowers-requesting-code-review/) | Pre-commit verification pipeline with static security scan, baseline-aware quality gates |
| [receiving-code-review](./superpowers-receiving-code-review/) | Responds to review feedback with technical rigor and verification |

### Completion Skills

| Skill | Description |
|--------|-------------|
| [verification-before-completion](./superpowers-verification-before-completion/) | Run verification commands and confirm output before claiming success |
| [finishing-a-development-branch](./superpowers-finishing-a-development-branch/) | Verify tests, present options for merge/PR/cleanup |

### Infrastructure Skills

| Skill | Description |
|--------|-------------|
| [using-git-worktrees](./superpowers-using-git-worktrees/) | Creates isolated git worktrees with smart directory selection |
| [writing-skills](./superpowers-writing-skills/) | Create new skills following best practices |
| [slash-commands](./superpowers-slash-commands/) | Dispatcher for `/superpowers:skill-name` syntax |
| [using-superpowers](./superpowers-using-superpowers/) | Introduction to the skills system and how to use it |

## Tool Reference

All skills use Hermes-native tools with explicit parameter syntax:

| Tool | Purpose | Example |
|-------|---------|---------|
| `write_file` | Create or replace files completely | `write_file(path="src/main.py", content="code here")` |
| `read_file` | Read file content with pagination | `read_file(path="README.md", offset=1, limit=100)` |
| `terminal` | Run shell commands | `terminal(command="pytest tests/", timeout=60)` |
| `patch` | Targeted find-and-replace edits | `patch(path="file.py", old_string="old", new_string="new")` |
| `search_files` | Search for files or content | `search_files(pattern="def test_", target="files", path="src/")` |
| `delegate_task` | Parallel subagent dispatch | `delegate_task(tasks=[{goal: "...", context: "..."}])` |
| `todo` | Track task progress | `todo(todos=[{id: "t1", content: "...", status: "pending"}])` |

## Getting Started

Superpowers triggers automatically based on your conversation. You don't need to install anything manually.

## Onboarding for Hermes

When using Superpowers with Hermes Agent, the skills are loaded automatically. No manual installation or configuration required.

**For New Users:**
1. Superpowers detects skill triggers and loads the appropriate skill
2. The skill provides explicit, step-by-step instructions
3. Follow the skill's guidance - all tool calls are specified
4. Skills integrate seamlessly with Hermes' existing tools (`write_file`, `read_file`, `terminal`, `patch`, `search_files`, `delegate_task`)

**Key Benefits:**
- **Automatic Activation:** Skills trigger based on conversation context
- **Hermes-Native:** All tool references use Hermes-specific syntax
- **No Configuration Required:** Works out of the box with Hermes
- **Explicit Instructions:** Every step shows exactly which tool to use and how

**Example Workflow:**
```
User: "Help me plan this feature"
→ [writing-plans] activates automatically
→ Creates comprehensive implementation plan with explicit tool calls
→ [subagent-driven-development] or [executing-plans] activates
→ Executes with proper tool usage (write_file, terminal, patch, etc.)
→ Work complete with verification
```

**Trigger patterns:**
- "Let's plan this" → `writing-plans` activates
- "How should I implement this?" → `test-driven-development` activates
- "Something's wrong" → `systematic-debugging` activates
- "Help me review this" → `requesting-code-review` activates
- "All done, what's next?" → `finishing-a-development-branch` activates

**Optional explicit invocation:**
You can also trigger skills directly with the skill prefix:
- "Use `/superpowers:brainstorming` to explore options"
- "Use `/superpowers:writing-plans` to create a plan"

## Migration Notes

**For Users Coming From Claude/Codex:**
These skills were originally designed for Claude Code but have been converted to work with Hermes Agent. The core concepts and workflows are identical, but all tool references have been updated:

- Shell commands → `terminal(command="...")`
- Generic "Read file" → `read_file(path="...")`
- Generic "Create file" → `write_file(path="...", content="...")`
- Bash operations → `patch(path="...", old_string="...", new_string="...")`

All skills now provide explicit, copy-pasteable tool examples that work reliably with Hermes.

## License

MIT

## Credits

- Superpowers methodology by Jesse Vincent
- Hermes Agent integration and auditing
- Community contributions and improvements
