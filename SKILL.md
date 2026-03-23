---
name: handoff-assistant
description: Enforces project handovers and debugging logs. Automatically triggers on git operations and fix failures to ensure cross-session continuity.
---

# Skill: Handoff & Debugging Intelligence

## 1. Trigger Conditions
- **Git Operations:** Activate whenever the user mentions "push", "commit", or "save to github".
- **Debugging:** Activate when a fix fails or when the user says "debug", "it's not working", or "try again".

## 2. Procedure: The Handoff (Git Push)
Before completing a git push, Claude must:
1. **Update `CLAUDE_LOG.md`**: Summarize the "What" and "How" using the established template.
2. **Path & Clipboard:** - Print: "Handoff log updated at: `./CLAUDE_LOG.md`"
   - Execute: `echo "$(pwd)/CLAUDE_LOG.md" | pbcopy`

## 3. Procedure: Recursive Debugging
When a fix is attempted and fails, Claude must:
1. **Update `DEBUG_TRACE.md`**: Record the Error, Attempt History, and "Lessons Learned."
2. **Context Continuity:** Before the next fix, Claude MUST read `DEBUG_TRACE.md` to avoid repeating failed strategies.
3. **Path & Clipboard:**
   - Print: "Debug trace updated: `./DEBUG_TRACE.md`"
   - Execute: `echo "$(pwd)/DEBUG_TRACE.md" | pbcopy`

## 4. Operational Rules
- **Formatting:** Use structured Markdown with ISO timestamps.
- **Persistence:** Never delete a `DEBUG_TRACE.md`; append new attempts to the bottom to maintain a full audit trail.
