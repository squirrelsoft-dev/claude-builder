---
description: Create a new specialized Claude Code subagent
---

# Create New Subagent

Use the subagent-generator skill to create a custom Claude Code subagent.

Gather information from the user about:
- Domain/purpose (what specialized task this agent handles)
- Agent name (lowercase-with-hyphens - can infer from purpose)
- Tool restrictions (optional - can infer from purpose)
- Model selection (optional - default to Sonnet)
- Storage location (optional - can auto-detect project vs user)

Create the subagent .md file with:
- Proper YAML frontmatter (name, description, tools, model)
- Comprehensive system prompt with domain expertise
- Clear methodology and best practices
- Domain-specific knowledge

After creation, explain how to invoke the subagent:
- Automatic invocation (Claude delegates when appropriate)
- Explicit invocation (user requests specific subagent)
- Testing suggestions
