---
name: handoff-assistant
description: Enforces project handovers and debugging logs. Automatically triggers on git operations and fix failures to ensure cross-session continuity.
---

# Skill: Handoff & Debugging Intelligence

## 1. Trigger Conditions
- **Git Operations:** Activate whenever the user mentions "push", "commit", "save", or "save to github".
- **Debugging:** Activate when a fix fails or when the user says "debug", "it's not working", or "try again".

## 2. Procedure: The Handoff (Git Push/Save)
Before completing a git push or save, Claude MUST:
1. **Update `CLAUDE_LOG.md`**: Use the **Sprint Summary Template** below (MANDATORY).
2. **Path & Clipboard:**
   - Print: "Handoff log updated at: `./CLAUDE_LOG.md`"
   - Execute: `echo "$(pwd)/CLAUDE_LOG.md" | pbcopy`

## 3. Procedure: Recursive Debugging
When a fix is attempted and fails, Claude MUST:
1. **Initialize/Update `DEBUG_TRACE.md`**: Use the **Debug Trace Template** below (MANDATORY).
2. **Context Continuity:** Before the next fix, Claude MUST read `DEBUG_TRACE.md` to avoid repeating failed strategies.
3. **Path & Clipboard:**
   - Print: "Debug trace updated: `./DEBUG_TRACE.md`"
   - Execute: `echo "$(pwd)/DEBUG_TRACE.md" | pbcopy`

## 4. Operational Rules
- **Persistence:** Never delete a `DEBUG_TRACE.md`; append new attempts to the bottom to maintain a full audit trail.
- **Template Compliance:** The templates below are MANDATORY. Do not deviate from their structure.

---

## 5. CLAUDE_LOG.md Template (Sprint Summary)

```markdown
🟢 [PROJECT NAME] STATUS: [YYYY-MM-DD]

**Current Focus:** [1 sentence describing the main goal]

✅ **Completed:**
- Task 1
- Task 2
- Task 3

⏳ **In Progress:**
- Current open task 1
- Current open task 2

🚀 **Next Steps:**
- First task for next session
```

---

## 6. DEBUG_TRACE.md Template (Debug Trace)

```markdown
# Debug Trace: [PROJECT NAME]

**Error:** [Brief description of the issue]

**Started:** [YYYY-MM-DD HH:MM]

| Strategy Attempted | Result | Why it Failed |
|--------------------|--------|---------------|
| [What was tried] | [What happened] | [Root cause / reason] |
| [What was tried] | [What happened] | [Root cause / reason] |
| [What was tried] | [What happened] | [Root cause / reason] |

**Resolution:** [Final fix or current status]
```

---

## 7. Quick Reference

| User Says | Claude Action |
|-----------|---------------|
| "save", "push", "commit", "save to github" | Update `CLAUDE_LOG.md` using Sprint Summary Template |
| "debug", "it's not working", "try again", fix fails | Update `DEBUG_TRACE.md` using Debug Trace Template |
