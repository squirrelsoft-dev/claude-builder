# Plugin Templates

This directory contains plugin templates for different use cases.

## Available Templates

### 1. Minimal Plugin (`minimal-plugin/`)

A bare-bones template to get started quickly.

**Contains:**
- Required plugin.json
- Basic README
- Empty skills/ directory

**Use when:**
- Starting from scratch
- Building simple plugins
- Want minimal boilerplate

**Next steps after using:**
- Add Skills using skill-generator
- Add Commands as needed
- Add Subagents if beneficial

---

### 2. Full-Featured Plugin (`full-featured-plugin/`)

A comprehensive template showing all extensibility features.

**Contains:**
- Complete plugin.json with all optional fields
- Example Skill (skills/example-helper/)
- Example Command (commands/example-command.md)
- Example Subagent (agents/example-agent.md)
- Example Hooks (hooks/hooks.json)
- Comprehensive README

**Use when:**
- Want to see all features in action
- Building complex plugins
- Need reference examples

**Features demonstrated:**
- Skills with tool restrictions
- User-invoked commands
- Specialized subagents with custom models
- Event-driven hooks
- Complete documentation

---

## Choosing a Template

### Use Minimal Plugin if:
- ✅ You want to build incrementally
- ✅ You only need one or two features
- ✅ You prefer minimal boilerplate
- ✅ You're comfortable adding features as needed

### Use Full-Featured Plugin if:
- ✅ You want to see all features working together
- ✅ You're building a comprehensive toolkit
- ✅ You want reference examples
- ✅ You need documentation templates

## Using a Template

### Option 1: Copy Template

```bash
# Copy template to your location
cp -r templates/plugins/minimal-plugin ~/my-custom-plugin

# Or for full-featured
cp -r templates/plugins/full-featured-plugin ~/my-custom-plugin

# Customize
cd ~/my-custom-plugin
# Edit .claude-plugin/plugin.json
# Add your features
```

### Option 2: Use Plugin Scaffolder

```bash
# Use the plugin-scaffolder skill or command
/new-plugin my-custom-plugin

# Or in conversation
"I want to create a new plugin called my-custom-plugin"
# (plugin-scaffolder skill will activate)
```

## Customization Steps

After copying a template:

### 1. Update Plugin Metadata

Edit `.claude-plugin/plugin.json`:

```json
{
  "name": "your-plugin-name",           // Change this
  "description": "Your description",     // Change this
  "version": "1.0.0",
  "author": {
    "name": "Your Name",                // Change this
    "email": "you@example.com"          // Optional
  }
}
```

### 2. Add Your Features

**Add Skills:**
```bash
mkdir -p skills/your-skill
# Create skills/your-skill/SKILL.md
# Use skill-generator or copy from templates/skills/
```

**Add Commands:**
```bash
mkdir -p commands
# Create commands/your-command.md
```

**Add Subagents:**
```bash
mkdir -p agents
# Create agents/your-agent.md
# Use subagent-generator or copy from templates/agents/
```

**Add Hooks:**
```bash
mkdir -p hooks
# Create hooks/hooks.json
# Use hook-generator or copy from templates/hooks/
```

### 3. Test Locally

```bash
# Create development marketplace
mkdir -p ~/.claude/marketplaces/dev/.claude-plugin
echo '{"name":"dev","description":"Development marketplace"}' > ~/.claude/marketplaces/dev/.claude-plugin/marketplace.json

# Link your plugin
ln -s /path/to/your-plugin ~/.claude/marketplaces/dev/your-plugin

# Install
/plugin marketplace add ~/.claude/marketplaces/dev
/plugin install your-plugin@dev
```

### 4. Iterate

Make changes → Uninstall → Reinstall → Test

```bash
/plugin uninstall your-plugin
/plugin install your-plugin@dev
```

### 5. Distribute

**Via Git:**
```bash
cd your-plugin
git init
git add .
git commit -m "Initial commit"
git remote add origin <url>
git push
```

**Via Team Marketplace:**
```bash
# Copy to shared marketplace
cp -r your-plugin /team/shared/marketplace/your-plugin
# Team members can install from there
```

## Template Comparison

| Feature | Minimal | Full-Featured |
|---------|---------|---------------|
| plugin.json | ✅ Basic | ✅ Complete |
| README | ✅ Short | ✅ Comprehensive |
| Example Skill | ❌ | ✅ |
| Example Command | ❌ | ✅ |
| Example Subagent | ❌ | ✅ |
| Example Hooks | ❌ | ✅ |
| Documentation | 📄 Minimal | 📚 Extensive |

## Best Practices

### Plugin Structure
- Keep plugin.json valid and complete
- Include comprehensive README
- Organize features by type (skills/, commands/, etc.)
- Use clear, descriptive names

### Development
- Test locally before distributing
- Version your changes (update plugin.json version)
- Document all features
- Keep dependencies minimal

### Distribution
- Use git for version control
- Tag releases
- Provide installation instructions
- Include usage examples

## Examples by Use Case

### Team Coding Standards Plugin
**Template**: Full-Featured
**Features**:
- Skills: code-reviewer, style-checker
- Commands: /format, /lint
- Hooks: Auto-format on save
- Subagents: Style auditor

### Personal Productivity Plugin
**Template**: Minimal → Add as needed
**Features**:
- Skills: note-taker, todo-helper
- Commands: /daily-standup, /weekly-review

### Service Integration Plugin
**Template**: Minimal
**Features**:
- Skills: service-helper
- MCP: Service API connection
- Commands: /deploy, /status

### Security Toolkit Plugin
**Template**: Full-Featured
**Features**:
- Skills: vulnerability-scanner
- Subagents: security-auditor
- Commands: /security-check
- Hooks: Block commits with secrets

## Additional Resources

- See `templates/skills/` for skill templates
- See `templates/agents/` for subagent templates
- See `templates/hooks/` for hook templates
- Use generator skills to create features
- Check documentation in `docs/`

## Support

- Use claude-builder plugin generators for help
- Check structure-checker subagent to validate
- Use yaml-validator to check configurations
- Reference Claude Code documentation

---

**Ready to build?** Choose your template and start creating!
