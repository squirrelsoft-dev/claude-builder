---
description: Scaffold a new Claude Code plugin structure
---

# Create New Plugin

Use the plugin-scaffolder skill to create a complete Claude Code plugin structure.

Gather information from the user about:
- Plugin name (lowercase-with-hyphens)
- Plugin purpose (what features it will provide)
- Author name (optional - can infer or use default)
- Which components to include (optional - can create all directories)

Create the complete plugin structure with:
- .claude-plugin/plugin.json manifest
- Directory structure (skills/, commands/, agents/, hooks/)
- README with usage instructions
- Optional git initialization

After creation, provide instructions for:
- Local development/testing
- Adding features to the plugin
- Team distribution
