# Claude Builder

A meta-development toolkit for creating Claude Code extensibility features. Build Skills, Subagents, Hooks, Commands, and Plugins faster with intelligent generators and proven templates.

## Overview

Claude Builder is a comprehensive plugin that helps you create and manage Claude Code extensibility features. It uses a hybrid approach:

- **Proactive Skills**: Claude automatically helps when you're working on extensibility features
- **Quick Commands**: Explicit shortcuts when you want to create something immediately
- **Validation Agents**: Specialized subagents that check your configurations
- **Template Library**: Proven patterns for common use cases

## Features

### Core Generator Skills

1. **skill-generator** - Create new Skills with intelligent defaults
   - Auto-detects purpose from context
   - Generates proper YAML frontmatter
   - Creates supporting file structure
   - Suggests tool restrictions

2. **plugin-scaffolder** - Scaffold complete plugin structures
   - Creates full directory layout
   - Generates plugin.json manifest
   - Sets up all component directories
   - Initializes documentation

3. **subagent-generator** - Generate custom subagents
   - Creates properly formatted .md files
   - Suggests appropriate tool restrictions
   - Recommends model selection
   - Places in correct location

4. **hook-generator** - Create and configure hooks
   - Provides common hook templates
   - Updates settings.json safely
   - Validates hook configurations

5. **extensibility-advisor** - Choose the right approach
   - Helps decide between Skills, Commands, Subagents, and Hooks
   - Analyzes use cases and suggests best practices
   - Explains trade-offs

### Quick Commands

Invoke these directly when you want immediate action:

- `/new-skill [name]` - Create a new Skill
- `/new-plugin [name]` - Scaffold a new plugin
- `/new-agent [name]` - Generate a new subagent
- `/new-hook [event]` - Create a new hook

### Validation Subagents

- **yaml-validator** - Validates YAML frontmatter in Skills and agents
- **structure-checker** - Validates plugin directory structure

### Template Library

Pre-built templates for common patterns:

**Skills:**
- code-reviewer
- test-runner
- doc-generator

**Agents:**
- debugger
- refactorer
- security-auditor

**Hooks:**
- auto-formatter
- pre-commit
- notification examples

**Plugins:**
- minimal-plugin
- full-featured-plugin

## Installation

### From Local Directory

```bash
# Create a dev marketplace
mkdir -p ~/.claude/marketplaces/dev/.claude-plugin
echo '{"name": "dev", "description": "Development marketplace"}' > ~/.claude/marketplaces/dev/.claude-plugin/marketplace.json

# Link claude-builder plugin
ln -s /path/to/claude-builder ~/.claude/marketplaces/dev/claude-builder

# Add marketplace and install
/plugin marketplace add ~/.claude/marketplaces/dev
/plugin install claude-builder@dev
```

### For Team Use

Add to your project's `.claude/settings.json`:

```json
{
  "plugins": {
    "marketplaces": [
      {
        "path": "/path/to/marketplace"
      }
    ],
    "installed": [
      {
        "name": "claude-builder",
        "marketplace": "dev"
      }
    ]
  }
}
```

## Usage

### Proactive Mode (Skills Auto-Activate)

Just start discussing what you want to create:

```
You: I need a skill that helps me review security issues in code
Claude: [skill-generator activates and helps you create it]
```

### Explicit Mode (Commands)

Use slash commands for immediate action:

```
You: /new-skill security-reviewer
Claude: [Creates a new security-reviewer skill with intelligent defaults]
```

### Getting Advice

When unsure which approach to use:

```
You: I want to automatically format code after edits. Should I use a skill or a hook?
Claude: [extensibility-advisor explains that hooks are better for deterministic automation]
```

## Examples

### Creating a New Skill

```
You: I want to create a skill that helps me write API documentation
Claude: I'll help you create an API documentation skill. Let me generate it with intelligent defaults.

[skill-generator creates:]
- skills/api-doc-generator/SKILL.md
- Proper YAML frontmatter
- System prompt for API documentation
- Tool restrictions (Read, Grep, Glob for analyzing code)
```

### Scaffolding a Plugin

```
You: /new-plugin team-productivity
Claude: Creating a new plugin structure...

[plugin-scaffolder creates:]
- team-productivity/
  - .claude-plugin/plugin.json
  - skills/
  - commands/
  - agents/
  - README.md
```

### Creating a Subagent

```
You: I need a specialized agent for database query optimization
Claude: I'll create a database optimization subagent with appropriate tools.

[subagent-generator creates:]
- agents/db-optimizer.md
- Tool access: Read, Grep, Bash (for analyzing queries)
- Model: Sonnet (good balance for analysis)
```

## Best Practices

### When to Use Each Feature

**Skills** (Model-Invoked):
- Complex, multi-step workflows
- When you want Claude to help proactively
- Reusable capabilities across projects
- Example: code-reviewer, test-generator

**Commands** (User-Invoked):
- Frequently used, simple workflows
- When you want explicit control
- Quick shortcuts to common tasks
- Example: /run-tests, /deploy

**Subagents** (Specialized Assistants):
- Domain-specific expertise
- Tasks needing isolated context
- Different tool access requirements
- Example: debugger, security-auditor

**Hooks** (Automated Events):
- Deterministic automation
- Always-on behaviors
- Formatting, logging, validation
- Example: auto-format on save, pre-commit checks

**Plugins** (Bundle Everything):
- Shareable collections
- Team workflows
- Complete feature sets
- Example: team-standards, company-best-practices

## Development Workflow

1. **Create**: Use generators to create new features
2. **Test**: Try your new Skill/Agent/Hook in conversation
3. **Iterate**: Refine based on usage
4. **Share**: Package into plugin for team use
5. **Distribute**: Share via marketplace

## Template Customization

All templates are starting points. Customize them for your needs:

1. Browse `templates/` directory
2. Copy template to your location
3. Modify YAML frontmatter and content
4. Test and iterate

## Troubleshooting

### Skill Not Activating

- Check SKILL.md description is clear and specific
- Include keywords that match your use case
- Verify YAML frontmatter is valid

### Command Not Found

- Ensure plugin is enabled: `/plugin`
- Check command file has proper .md extension
- Verify frontmatter includes description

### Hook Not Firing

- Check hook event name is correct
- Verify settings.json syntax
- Test hook command independently in shell

### Subagent Not Available

- Confirm .md file is in agents/ directory
- Check YAML frontmatter is valid
- Verify name field is lowercase with hyphens

## Contributing

This is a personal/team toolkit, but contributions are welcome:

1. Add new templates to `templates/` directories
2. Enhance generator Skills with better defaults
3. Create additional validation subagents
4. Share useful hook examples

## Version History

### 1.0.0 (Initial Release)
- Core generator Skills (skill, plugin, subagent, hook)
- Extensibility advisor Skill
- Quick-access commands
- Validation subagents
- Template library with 12+ examples
- Comprehensive documentation

## License

MIT - Use freely for personal and commercial projects

## Support

For issues or questions:
1. Check the docs/ directory for Claude Code documentation
2. Review template examples
3. Use the extensibility-advisor Skill for guidance
4. Test generators incrementally

---

Built with Claude Code for Claude Code developers. Meta-development at its finest.
