# Full-Featured Plugin Template

A comprehensive Claude Code plugin template demonstrating all extensibility features: Skills, Commands, Subagents, and Hooks.

## Features

This template includes examples of:

- ✅ **Skills**: Model-invoked capabilities
- ✅ **Commands**: User-invoked shortcuts
- ✅ **Subagents**: Specialized AI assistants
- ✅ **Hooks**: Event-driven automation

## Structure

```
full-featured-plugin/
├── .claude-plugin/
│   └── plugin.json           # Plugin metadata
├── skills/
│   └── example-helper/       # Example skill
│       └── SKILL.md
├── commands/
│   └── example-command.md    # Example command
├── agents/
│   └── example-agent.md      # Example subagent
├── hooks/
│   └── hooks.json            # Example hooks
└── README.md                 # This file
```

## Installation

### Local Development

```bash
# Create dev marketplace
mkdir -p ~/.claude/marketplaces/dev/.claude-plugin
echo '{"name":"dev","description":"Development marketplace"}' > ~/.claude/marketplaces/dev/.claude-plugin/marketplace.json

# Link this plugin
ln -s /path/to/full-featured-plugin ~/.claude/marketplaces/dev/full-featured-plugin

# Add marketplace and install
/plugin marketplace add ~/.claude/marketplaces/dev
/plugin install full-featured-plugin@dev
```

### Team Installation

Add to `.claude/settings.json` in your repository:

```json
{
  "plugins": {
    "marketplaces": [
      {
        "path": "/team/shared/marketplace"
      }
    ],
    "installed": [
      {
        "name": "full-featured-plugin",
        "marketplace": "team"
      }
    ]
  }
}
```

## Components

### Skills

**Location**: `skills/*/SKILL.md`

Skills are model-invoked capabilities that Claude automatically uses when relevant.

**Example**: `skills/example-helper/SKILL.md`
- Activates when specific keywords are mentioned
- Can restrict tools for safety
- Supports progressive disclosure with supporting files

**Usage**: Claude automatically invokes when relevant, or use explicitly:
```
"Use the example-helper skill to..."
```

### Commands

**Location**: `commands/*.md`

Commands are user-invoked shortcuts for common operations.

**Example**: `commands/example-command.md`
- Invoked by typing `/example-command`
- Simple prompt expansion
- Quick access to frequent tasks

**Usage**:
```
/example-command
```

### Subagents

**Location**: `agents/*.md`

Subagents are specialized AI assistants with their own context and expertise.

**Example**: `agents/example-agent.md`
- Isolated context window
- Can use different model (Sonnet/Opus/Haiku)
- Restricted or full tool access

**Usage**: Claude delegates automatically, or invoke explicitly:
```
"Use the example-agent subagent to investigate this issue"
```

### Hooks

**Location**: `hooks/hooks.json`

Hooks are event-driven automation that runs at specific points.

**Example**: `hooks/hooks.json`
- PostToolUse: Run after tool execution
- PreToolUse: Run before (can block operations)
- Various other lifecycle events

**Usage**: Hooks run automatically when events trigger.

## Customization

### 1. Update Plugin Metadata

Edit `.claude-plugin/plugin.json`:
- Change `name` to your plugin name (lowercase-with-hyphens)
- Update `description`, `author`, `repository`, etc.
- Increment `version` as you make changes

### 2. Customize Skills

Edit `skills/*/SKILL.md`:
- Update YAML frontmatter (name, description, tools)
- Modify system prompt content
- Add supporting files if needed

### 3. Customize Commands

Edit `commands/*.md`:
- Update YAML frontmatter (description)
- Modify command instructions

### 4. Customize Subagents

Edit `agents/*.md`:
- Update YAML frontmatter (name, description, tools, model)
- Modify system prompt and expertise

### 5. Customize Hooks

Edit `hooks/hooks.json`:
- Change event types
- Update tool matchers
- Modify shell commands

## Development Workflow

### 1. Make Changes
Edit skills, commands, agents, or hooks

### 2. Test Locally
Use the local development installation method

### 3. Uninstall/Reinstall to Test Changes
```bash
/plugin uninstall full-featured-plugin
/plugin install full-featured-plugin@dev
```

### 4. Iterate
Make changes, reinstall, test

### 5. Version and Release
- Update version in plugin.json
- Tag release in git
- Share updated marketplace

## Best Practices

### Skills
- Keep descriptions clear with trigger keywords
- Use tool restrictions for safety
- Make system prompts detailed and specific
- Test with various trigger phrases

### Commands
- Keep them simple and focused
- Use clear, memorable names
- Document what they do

### Subagents
- Use when isolated context is needed
- Choose appropriate model (Haiku for simple, Opus for complex)
- Restrict tools to minimum needed
- Provide domain-specific expertise

### Hooks
- Keep commands fast (they block operations)
- Test thoroughly before deploying
- Be careful with PreToolUse blocking
- Log errors for debugging

## Distribution

### Via Git Repository

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin <your-repo>
git push -u origin main
```

### Via Marketplace

Create marketplace structure:
```
marketplace/
├── .claude-plugin/
│   └── marketplace.json
└── your-plugin/
    └── (plugin files)
```

Share the marketplace directory with your team.

## Troubleshooting

### Plugin not loading
- Check plugin.json is valid JSON
- Verify .claude-plugin/ directory exists
- Ensure name in plugin.json matches directory name

### Skill not activating
- Check description includes relevant keywords
- Verify YAML frontmatter is valid
- Test with explicit invocation first

### Command not found
- Ensure filename matches command (command.md → /command)
- Check file is in commands/ directory
- Verify plugin is enabled

### Hook not running
- Check hooks.json is valid JSON
- Verify event names and tool matchers
- Test hook command manually

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

MIT License - See LICENSE file for details

## Support

For issues or questions:
- Open an issue on GitHub
- Check Claude Code documentation
- Consult the community

---

**Happy building!** Use this template as a starting point for your own powerful Claude Code plugins.
