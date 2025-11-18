# Hook Templates

This directory contains example hook configurations for common automation tasks.

## Available Templates

### 1. Auto-Formatter (`auto-formatter-example.json`)

Automatically formats code after editing based on file type:
- TypeScript/JavaScript → Prettier
- Python → Black
- Go → gofmt

**Usage**: Add to `.claude/settings.json` or `~/.claude/settings.json`

**Requirements**:
- `prettier` installed for TS/JS
- `black` installed for Python
- `gofmt` installed for Go

### 2. Command Logger (`command-logger-example.json`)

Logs all Bash commands to a file for auditing and compliance.

**Log Location**: `~/.claude/logs/bash-commands.log`

**Usage**: Add to settings.json. Creates log directory automatically.

### 3. Notification (`notification-example.json`)

Shows desktop notification when Claude needs user attention.

**Platform**: macOS (uses osascript)

**Usage**: Add to settings.json for notifications when Claude is waiting.

**Note**: For Linux, replace with `notify-send`. For Windows, use PowerShell notifications.

### 4. File Protection (`file-protection-example.json`)

Blocks edits to sensitive files:
- `.env` and `.env.*` files
- Lock files (`*.lock`)
- Files with "secrets" in name

**Usage**: Add to `.claude/settings.json` for project-wide protection.

**Behavior**: Hook exits with error code 1 to block the operation.

## Installing a Hook Template

1. **Choose template**: Select the hook that matches your need

2. **Copy configuration**: Copy the JSON content

3. **Merge into settings.json**:

   ```bash
   # For project-level (shared with team)
   # Edit .claude/settings.json

   # For user-level (personal)
   # Edit ~/.claude/settings.json
   ```

4. **Merge carefully**: Don't overwrite existing hooks, merge them:

   ```json
   {
     "hooks": {
       "PostToolUse": [
         ...existing hooks...,
         ...new hook...
       ]
     }
   }
   ```

5. **Test**: Trigger the event to verify the hook works

## Creating Custom Hooks

Use these templates as starting points:

### Basic Structure

```json
{
  "hooks": {
    "EventName": [
      {
        "matcher": "ToolName",
        "hooks": [
          {
            "type": "command",
            "command": "your shell command here"
          }
        ]
      }
    ]
  }
}
```

### Available Events

- `PreToolUse` - Before tool execution (can block)
- `PostToolUse` - After tool execution
- `UserPromptSubmit` - When user submits prompt
- `Notification` - When Claude sends notification
- `Stop` - When Claude finishes responding
- `SubagentStop` - When subagent completes
- `PreCompact` - Before compact operation
- `SessionStart` - Session starts
- `SessionEnd` - Session ends

### Accessing Parameters

Hooks receive JSON via stdin:

```bash
# Get file path from Edit/Write tools
FILE=$(jq -r '.parameters.file_path')

# Get command from Bash tool
CMD=$(jq -r '.parameters.command')

# Get tool name
TOOL=$(jq -r '.toolName')
```

### Conditional Logic

```bash
# Check file type
case $FILE in
  *.ts|*.js) echo "TypeScript/JavaScript file";;
  *.py) echo "Python file";;
esac

# Check command content
if [[ $CMD == *"rm -rf"* ]]; then
  echo "Dangerous command detected"
  exit 1
fi
```

### Blocking Operations (PreToolUse only)

Exit with code 1 to block:

```bash
if [[ condition ]]; then
  echo "Operation blocked" >&2
  exit 1
fi
```

## Best Practices

1. **Test hooks thoroughly**: Ensure they work as expected
2. **Handle errors gracefully**: Use `|| true` for non-critical operations
3. **Keep commands fast**: Hooks block operations
4. **Log to files, not stdout**: Stdout goes to user
5. **Be careful with PreToolUse blocking**: Can prevent Claude from working
6. **Document your hooks**: Add comments explaining purpose

## Troubleshooting

### Hook not running

- Check event name is correct (case-sensitive)
- Verify matcher matches the tool
- Check JSON syntax is valid
- Look for errors in Claude Code logs

### Hook fails

- Test command manually with sample JSON
- Check for missing dependencies (prettier, black, etc.)
- Verify file paths and permissions
- Add error logging to diagnose

### Performance issues

- Make hooks faster (avoid heavy operations)
- Run expensive operations in background
- Consider PostToolUse instead of PreToolUse

## Security Notes

⚠️ **Warning**: Hooks run with your environment credentials.

- Review hook commands before installing
- Don't copy hooks from untrusted sources
- Project-level hooks affect all team members
- Test in isolation before deploying to team

## Examples by Use Case

### Code Quality Automation
- Auto-formatter (PostToolUse on Edit)
- Linter (PostToolUse on Edit)
- Test runner (PostToolUse on Edit for test files)

### Security & Compliance
- Command logger (PreToolUse on Bash)
- File protection (PreToolUse on Edit/Write)
- Sensitive data checks (PreToolUse on Write)

### Notifications & Alerts
- Desktop notifications (Notification event)
- Slack/Discord webhooks (Stop event)
- Email alerts (SubagentStop event)

### Development Workflow
- Auto-commit (PostToolUse on Edit)
- Dependency updates (SessionEnd event)
- Backup before edits (PreToolUse on Edit)

## Additional Resources

- See `docs/claude-code-hooks.md` for complete documentation
- Use `/hooks` command for interactive hook management
- Use `hook-generator` skill for creating custom hooks
