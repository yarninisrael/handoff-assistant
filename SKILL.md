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
1. **Update `DEBUG_TRACE.md`**: Use the **Error Audit Template** below (MANDATORY).
2. **Context Continuity:** Before the next fix, Claude MUST read `DEBUG_TRACE.md` to avoid repeating failed strategies.
3. **Path & Clipboard:**
   - Print: "Debug trace updated: `./DEBUG_TRACE.md`"
   - Execute: `echo "$(pwd)/DEBUG_TRACE.md" | pbcopy`

## 4. Operational Rules
- **Formatting:** Use structured Markdown with ISO timestamps.
- **Persistence:** Never delete a `DEBUG_TRACE.md`; append new attempts to the bottom to maintain a full audit trail.
- **Template Compliance:** The templates below are MANDATORY. Do not deviate from their structure.

---

## 5. CLAUDE_LOG.md Template (Sprint Summary)

```markdown
# Project Handoff Log

## Last Updated
<!-- ISO 8601 timestamp -->
**Date:** YYYY-MM-DDTHH:MM:SS

## Current Status
<!-- One-line summary of where the project stands -->
**Status:** [In Progress | Blocked | Complete | Needs Review]
**Summary:** [Brief description of current state]

## Accomplishments
<!-- What was completed this session -->
- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

## Technical State

### Files Modified
| File | Change Type | Description |
|------|-------------|-------------|
| `path/to/file` | Created/Modified/Deleted | Brief description |

### MCP Servers / Dependencies
| Server/Dependency | Status | Notes |
|-------------------|--------|-------|
| `server-name` | Online/Offline/Error | Any relevant info |

### Environment Notes
<!-- Any env vars, config changes, or setup notes -->
- Note 1
- Note 2

## Next Steps
<!-- Clear action items for the next session -->
1. [ ] Next action item
2. [ ] Next action item
3. [ ] Next action item

## Blockers / Open Questions
<!-- Anything that needs resolution -->
- Blocker or question 1
- Blocker or question 2
```

---

## 6. DEBUG_TRACE.md Template (Error Audit)

```markdown
# Debug Trace Log

## Session Info
**Started:** YYYY-MM-DDTHH:MM:SS
**Project:** [Project name or path]

---

## Initial Error
<!-- Capture the original error exactly as it appeared -->
**Error Type:** [e.g., Runtime, Compile, Connection, Logic]
**Error Message:**
```
[Paste exact error message here]
```
**Context:** [What was happening when the error occurred]

---

## Attempt History

| # | Timestamp | Hypothesis | Action Taken | Result | Outcome |
|---|-----------|------------|--------------|--------|---------|
| 1 | HH:MM:SS | [What we thought was wrong] | [What we tried] | [What happened] | Failed/Partial/Success |
| 2 | HH:MM:SS | [What we thought was wrong] | [What we tried] | [What happened] | Failed/Partial/Success |
| 3 | HH:MM:SS | [What we thought was wrong] | [What we tried] | [What happened] | Failed/Partial/Success |

---

## Lessons Learned
<!-- Key insights to prevent repeating failed strategies -->
- **What didn't work:** [Approach that failed and why]
- **What finally worked:** [The successful fix, if found]
- **Root cause:** [The actual underlying issue]
- **Prevention:** [How to avoid this in the future]

---

## Resolution Status
**Resolved:** [Yes/No/Partial]
**Final Fix:** [Description of the solution]
**Time to Resolution:** [Duration]
```

---

## 7. Quick Reference

| User Says | Claude Action |
|-----------|---------------|
| "save", "push", "commit", "save to github" | Update `CLAUDE_LOG.md` using Sprint Summary Template |
| "debug", "it's not working", "try again", fix fails | Update `DEBUG_TRACE.md` using Error Audit Template |
