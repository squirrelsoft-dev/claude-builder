# Minimal Plugin Template

A bare-bones Claude Code plugin template to get started quickly.

## Structure

```
minimal-plugin/
├── .claude-plugin/
│   └── plugin.json       # Plugin metadata (required)
├── skills/               # Add your Skills here
└── README.md             # This file
```

## Getting Started

1. **Rename the plugin**:
   - Change `minimal-plugin` to your plugin name (lowercase-with-hyphens)
   - Update `name` in `.claude-plugin/plugin.json`

2. **Update metadata**:
   - Edit `.claude-plugin/plugin.json`:
     - Set `description` to describe your plugin
     - Set `author.name` to your name
     - Optionally add `email`, `url`, `repository`, `license`

3. **Add features**:
   - Create Skills in `skills/` directory
   - Add Commands in `commands/` directory (create if needed)
   - Add Subagents in `agents/` directory (create if needed)

4. **Test locally**:
   ```bash
   # Create dev marketplace
   mkdir -p ~/.claude/marketplaces/dev/.claude-plugin
   echo '{"name":"dev","description":"Dev marketplace"}' > ~/.claude/marketplaces/dev/.claude-plugin/marketplace.json

   # Link your plugin
   ln -s /path/to/your-plugin ~/.claude/marketplaces/dev/your-plugin

   # Add marketplace and install
   /plugin marketplace add ~/.claude/marketplaces/dev
   /plugin install your-plugin@dev
   ```

## Adding Features

### Add a Skill

```bash
mkdir -p skills/my-skill
# Create skills/my-skill/SKILL.md with YAML frontmatter
```

### Add a Command

```bash
mkdir -p commands
# Create commands/my-command.md with instructions
```

### Add a Subagent

```bash
mkdir -p agents
# Create agents/my-agent.md with YAML frontmatter
```

## Sharing

1. **Via git**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **Via marketplace**:
   - Create or add to existing marketplace
   - Copy plugin directory to marketplace
   - Share marketplace with team

## License

MIT (or your preferred license)
