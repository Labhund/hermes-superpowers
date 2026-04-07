---
name: superpowers-slash-commands
description: "Slash command dispatcher for Superpowers skills. Detects /superpowers-skill-name syntax and loads the appropriate skill without conflicting with existing Hermes skills."
---

# Superpowers Slash Commands

This skill detects and dispatches `/superpowers-skill-name` commands to load Superpowers skills with proper namespacing.

## Command Syntax

```
/superpowers-<skill-name>
```

## Available Commands

- `/superpowers-brainstorming` - Turn ideas into fully formed designs
- `/superpowers-writing-plans` - Create detailed implementation plans
- `/superpowers-systematic-debugging` - 4-phase root cause debugging
- `/superpowers-test-driven-development` - RED-GREEN-REFACTOR TDD cycle
- `/superpowers-subagent-driven-development` - Fast iteration with two-stage review
- `/superpowers-requesting-code-review` - Pre-review checklist
- `/superpowers-receiving-code-review` - Responding to feedback
- `/superpowers-executing-plans` - Batch execution with checkpoints
- `/superpowers-dispatching-parallel-agents` - Concurrent subagent workflows
- `/superpowers-using-git-worktrees` - Parallel development branches
- `/superpowers-finishing-a-development-branch` - Merge/PR decision workflow
- `/superpowers-verification-before-completion` - Ensure it's actually fixed
- `/superpowers-writing-skills` - Create new skills following best practices
- `/superpowers-using-superpowers` - Introduction to the skills system

## How It Works

When you use a `/superpowers-` command:

1. This skill parses the command and extracts the skill name
2. Loads the corresponding `superpowers-<skill-name>` skill
3. The skill takes over and guides the workflow
4. No conflict with existing Hermes skills (e.g., `/plan` vs `/superpowers-writing-plans`)

## Usage

Just type the command naturally in conversation:

```
/superpowers-brainstorming I want to build a feature for tracking user engagement
```

```
/superpowers-debugging This test is failing intermittently
```

```
/superpowers-writing-plans Create an implementation plan for the search feature
```

## Technical Implementation

This skill serves as a dispatcher. When a `/superpowers-` command is detected:

1. Extract skill name from the command (e.g., `/superpowers-brainstorming` → `brainstorming`)
2. Construct full skill name: `superpowers-{skill_name}`
3. Load the skill using `skill_view(name="superpowers-{skill_name}")`
4. Pass through any additional context from the command

## Routing Logic

When the command `/superpowers-<skill-name>` is detected, use:

```
skill_view(name="superpowers-{skill-name}")
```

For example:
- `/superpowers-brainstorming` → `skill_view(name="superpowers-brainstorming")`
- `/superpowers-writing-plans` → `skill_view(name="superpowers-writing-plans")`
- `/superpowers-test-driven-development` → `skill_view(name="superpowers-test-driven-development")`

## Namespace Philosophy

All Superpowers skills are prefixed with `superpowers-` to:

- Prevent naming conflicts with native Hermes skills
- Make it clear which skill system is being used
- Allow comparison between similar workflows (e.g., `test-driven-development` vs `superpowers-test-driven-development`)
- Enable selective usage of either system
