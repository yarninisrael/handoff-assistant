# handoff-assistant

A Claude Code skill that enforces project handovers and debugging logs for cross-session continuity.

## Features

- **Automatic Triggers**: Activates on git operations (push, commit) and debugging scenarios
- **Handoff Logs**: Maintains `CLAUDE_LOG.md` with session summaries
- **Debug Traces**: Tracks failed fix attempts in `DEBUG_TRACE.md` to avoid repeating strategies
- **Audit Trail**: Appends entries with ISO timestamps for full history

## Trigger Conditions

| Trigger | Keywords |
|---------|----------|
| Git Operations | "push", "commit", "save to github" |
| Debugging | "debug", "it's not working", "try again", fix failures |

## Generated Files

- `CLAUDE_LOG.md` - Session handoff summaries
- `DEBUG_TRACE.md` - Failed fix attempts and lessons learned

## Installation

Place this skill in your Claude Code skills directory:
```
~/.claude/skills/handoff-assistant/
```

## Usage

The skill auto-triggers based on context, or invoke manually:
```
/handoff-assistant
```

## License

MIT
