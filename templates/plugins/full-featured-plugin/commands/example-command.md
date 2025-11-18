---
description: Example command demonstrating how slash commands work in Claude Code
---

# Example Command

This is an example command that demonstrates how Claude Code slash commands work.

## How Commands Work

When you type `/example-command`, Claude receives these instructions and responds accordingly. Commands are:

- **User-Invoked**: You explicitly type `/command-name` to trigger them
- **Simple Prompts**: They expand into instructions for Claude
- **Quick Shortcuts**: Fast access to common operations

## What This Command Does

When invoked, explain to the user:

1. **What commands are**: User-invoked prompt expansions
2. **How they differ from skills**: Commands require explicit invocation
3. **How to create them**: Simple markdown files with optional description
4. **Usage examples**: Show common command patterns

## Example Response

Provide a response like:

"You've invoked the example-command! Here's how commands work:

**Commands vs Skills:**
- Commands: You type `/command` explicitly (like you just did)
- Skills: Claude automatically uses them based on context

**Creating Commands:**
1. Create a .md file in commands/ directory
2. Add optional description in YAML frontmatter
3. Write instructions for Claude
4. Command name = filename (example-command.md → /example-command)

**Common Uses:**
- `/run-tests` - Run test suite
- `/deploy` - Deploy application
- `/review-pr` - Review pull request
- `/format` - Format code

Commands are great for frequently-used operations you want quick access to!"

## Customization

To create your own command:

1. Create a new .md file in commands/ directory
2. Name it what you want the command to be called (my-command.md → /my-command)
3. Add description in frontmatter (optional but recommended)
4. Write clear instructions for what Claude should do

Example:
```markdown
---
description: Run the test suite and report results
---

# Run Tests

Execute the project's test suite using the appropriate test runner (npm test, pytest, cargo test, etc.).

Analyze the results and report:
- Number of tests passed/failed
- Any error messages
- Suggestions for fixing failures
```

That's it! Simple but powerful.
