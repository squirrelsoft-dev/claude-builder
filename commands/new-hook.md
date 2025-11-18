---
description: Create a new Claude Code hook for event-driven automation
---

# Create New Hook

Use the hook-generator skill to create a Claude Code hook configuration.

Gather information from the user about:
- Purpose (what should the hook do?)
- Event type (when should it trigger - can infer from purpose)
- Tool matcher (which tools - can infer from purpose)
- Scope (user vs project - can infer from purpose)

Create or update settings.json with:
- Proper hook configuration structure
- Valid event name and matcher
- Shell command that accomplishes the purpose
- Safe merge with existing hooks

After creation, provide:
- Testing instructions (how to trigger the hook)
- Debugging guidance (how to verify it works)
- Safety notes (what the hook does and when)

Remember: Hooks are deterministic automation that runs every time an event occurs. Make them reliable and well-tested.
