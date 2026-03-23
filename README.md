# 🧠 cerebrum

Task coordination hub for the Jimmy agent system.

## Agents

| Agent | Role |
|-------|------|
| **Jimmy** | Orchestrator — writes task briefs, coordinates, reports to Václav |
| **Reviewer** | Quality gate — reviews task briefs before execution |
| **Claude Code** | Builder — implements tasks on crib |

## Workflow

```
Václav → Jimmy → [writes issue] → Reviewer → APPROVED/NEEDS_REVISION
                                              ↓ APPROVED
                                         Claude Code → PR
                                              ↓
                                         Jimmy verifies → merged
                                              ↓
                                         Václav notified on TG
```

## Issue Labels

- `needs-review` — written by Jimmy, waiting for Reviewer
- `approved` — Reviewer approved, ready for Claude Code
- `in-progress` — Claude Code is working on it
- `needs-revision` — Reviewer flagged issues, Jimmy must fix brief
- `done` — verified and merged

## Rules

1. No code work starts without `approved` label
2. Every issue must have binary acceptance criteria (command + expected output)
3. Claude Code PRs must reference the issue (`fixes #N`)
4. Jimmy verifies acceptance criteria before closing issue
5. TG is for status updates only — all task detail lives here
