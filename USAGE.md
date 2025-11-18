# Claude Builder - Usage Guide

Complete guide to using the Claude Builder plugin for creating Claude Code extensibility features.

## Table of Contents

1. [Quick Start](#quick-start)
2. [Core Features](#core-features)
3. [Skills](#skills)
4. [Commands](#commands)
5. [Subagents](#subagents)
6. [Templates](#templates)
7. [Workflows](#workflows)
8. [Tips & Best Practices](#tips--best-practices)

## Quick Start

### Create a New Skill

**Option 1: Proactive (Skill Activates)**
```
You: "I need a skill that reviews API documentation for completeness"
Claude: [skill-generator activates and creates the skill]
```

**Option 2: Explicit (Command)**
```
You: /new-skill
Claude: [prompts for details and creates skill]
```

### Create a New Plugin

```
You: /new-plugin my-team-tools
Claude: [creates complete plugin structure]
```

### Create a New Subagent

```
You: "Create a subagent for optimizing database queries"
Claude: [subagent-generator creates specialized agent]
```

### Create a New Hook

```
You: "I want to automatically format Python code after editing"
Claude: [hook-generator creates PostToolUse hook]
```

## Core Features

### 1. Generator Skills

These Skills activate automatically when you discuss creating extensibility features:

#### skill-generator
**Activates when**: Discussing creating Skills
**What it does**: Creates SKILL.md files with proper YAML frontmatter
**Example triggers**: "create a skill", "new skill for...", "skill that helps with..."

**Example**:
```
You: "I need a skill for generating unit tests"
Claude: [skill-generator activates]
        I'll create a test-generator skill with:
        - Tool access: Read, Write, Grep, Glob
        - Activates when discussing tests
        - Creates test files based on code analysis
```

#### plugin-scaffolder
**Activates when**: Discussing creating plugins
**What it does**: Scaffolds complete plugin directory structures
**Example triggers**: "create plugin", "new plugin", "scaffold plugin"

**Example**:
```
You: "Create a plugin for our team's Python coding standards"
Claude: [plugin-scaffolder activates]
        Creating python-standards plugin with:
        - Skills for code review
        - Hooks for formatting
        - Commands for linting
```

#### subagent-generator
**Activates when**: Discussing creating subagents
**What it does**: Creates specialized AI assistant .md files
**Example triggers**: "create subagent", "specialized agent for...", "agent that handles..."

**Example**:
```
You: "I need an agent specialized in React performance optimization"
Claude: [subagent-generator activates]
        Creating react-optimizer subagent with:
        - Model: Sonnet (balanced for analysis)
        - Tools: Read, Edit, Grep, Glob, Bash
        - Expertise in React optimization patterns
```

#### hook-generator
**Activates when**: Discussing automation/hooks
**What it does**: Creates hook configurations and updates settings.json
**Example triggers**: "automatically...", "hook for...", "on save...", "after editing..."

**Example**:
```
You: "Automatically run prettier after I edit TypeScript files"
Claude: [hook-generator activates]
        Creating PostToolUse hook on Edit tool:
        - Triggers after editing *.ts files
        - Runs: prettier --write
        - Location: .claude/settings.json (project-level)
```

#### extensibility-advisor
**Activates when**: Asking which feature to use
**What it does**: Recommends Skills vs Commands vs Subagents vs Hooks
**Example triggers**: "should I use...", "which approach...", "skill or command..."

**Example**:
```
You: "Should I create a skill or a hook for code formatting?"
Claude: [extensibility-advisor activates]
        Recommendation: Hook

        Why: Code formatting is deterministic automation that
        should always happen. Hooks ensure it runs every time,
        while Skills are for intelligent decision-making.

        Suggested: PostToolUse hook on Edit tool
```

### 2. Quick Commands

Explicit shortcuts for immediate action:

#### /new-skill
```
You: /new-skill
Claude: "I'll help you create a new Skill. What should it do?"
```

#### /new-plugin
```
You: /new-plugin team-toolkit
Claude: [Creates complete plugin structure]
```

#### /new-agent
```
You: /new-agent
Claude: "I'll create a new subagent. What domain should it specialize in?"
```

#### /new-hook
```
You: /new-hook
Claude: "I'll set up a new hook. What should it automate?"
```

### 3. Validation Subagents

Specialized agents for checking configurations:

#### yaml-validator
**Purpose**: Validates YAML frontmatter in Skills and subagents
**Invoke**: "Check the YAML in my skills" or "Use yaml-validator to check this"

**Example**:
```
You: "Validate the YAML in skills/code-reviewer/SKILL.md"
Claude: [Invokes yaml-validator subagent]

Validation Results for skills/code-reviewer/SKILL.md:
✅ Status: Valid
- Name: Properly formatted (lowercase-with-hyphens)
- Description: Includes trigger keywords
- Tools: Valid tool names
```

#### structure-checker
**Purpose**: Validates plugin directory structures
**Invoke**: "Check my plugin structure" or "Use structure-checker to validate"

**Example**:
```
You: "Validate the structure of my-plugin"
Claude: [Invokes structure-checker subagent]

Structure Validation Report:
✅ plugin.json exists in .claude-plugin/
✅ All SKILL.md files properly placed
✅ Naming conventions followed
⚠️  README.md missing (recommended)
```

## Skills

### Working with Generator Skills

**Proactive Activation** (Recommended):
Just describe what you want naturally:
```
"I need help reviewing security vulnerabilities in code"
→ skill-generator creates security-reviewer skill

"I want to document our API endpoints"
→ skill-generator creates api-doc-generator skill

"Help me write better commit messages"
→ skill-generator creates commit-helper skill
```

**Intelligent Defaults**:
Skills are created with smart defaults:
- Name inferred from purpose
- Tools suggested based on task
- Location auto-detected (project vs user)
- Description includes activation keywords

**Customization After Creation**:
All generated skills can be edited:
```
You: "Make the code-reviewer skill more strict about variable naming"
Claude: [Edits SKILL.md to add naming conventions]
```

### Using Existing Skills

Once created, skills activate automatically:
```
You: "Review this authentication code for security issues"
→ code-reviewer skill activates
→ Analyzes code with Read/Grep/Glob
→ Reports findings
```

## Commands

### Using Commands

Commands require explicit invocation:
```
You: /run-tests
Claude: [Executes test suite and reports results]

You: /review-pr 123
Claude: [Reviews pull request #123]
```

### Creating Commands

Commands are simple markdown files:
```markdown
---
description: What the command does
---

# Command Name

Instructions for Claude...
```

**Example**:
```markdown
---
description: Run the test suite and report results
---

# Run Tests

Execute the project's test suite.
Report passed/failed tests and any errors.
Suggest fixes for failures.
```

## Subagents

### When to Use Subagents

Use subagents for:
- **Isolated context**: Long debugging sessions, research
- **Different tools**: Review-only agents with no write access
- **Different models**: Haiku for simple tasks, Opus for complex
- **Specialized expertise**: Domain-specific knowledge

### Creating Subagents

**Automatic**:
```
You: "I need a specialized agent for Rust performance optimization"
Claude: [subagent-generator creates rust-optimizer.md]
```

**What Gets Generated**:
- Proper YAML frontmatter (name, description, tools, model)
- Comprehensive system prompt
- Domain expertise and methodology
- Best practices for the domain

### Using Subagents

**Automatic Delegation**:
```
You: "Debug this complex React rendering issue"
Claude: "I'll invoke the react-debugger subagent..."
[Subagent investigates in isolated context]
[Returns findings to main conversation]
```

**Explicit Invocation**:
```
You: "Use the security-auditor subagent to check this auth code"
Claude: [Invokes specific subagent]
```

## Templates

The plugin includes proven templates in `templates/` directory:

### Skill Templates

Located in `templates/skills/`:

**code-reviewer-SKILL.md**:
- Reviews code for bugs and security
- Tool access: Read, Grep, Glob
- Checks OWASP top 10

**test-runner-SKILL.md**:
- Executes test suites
- Analyzes failures
- Tool access: Read, Bash, Grep, Glob

**doc-generator-SKILL.md**:
- Generates documentation from code
- Creates API docs and READMEs
- Tool access: Read, Write, Grep, Glob

### Agent Templates

Located in `templates/agents/`:

**debugger-template.md**:
- Specialized debugging expert
- Model: Sonnet
- Tools: Read, Edit, Bash, Grep, Glob

**refactorer-template.md**:
- Code refactoring specialist
- Improves structure and readability
- Tools: Read, Edit, Grep, Glob

**security-auditor-template.md**:
- Security vulnerability scanner
- OWASP top 10 expert
- Tools: Read, Grep, Glob

### Hook Templates

Located in `templates/hooks/`:

**auto-formatter-example.json**:
- Formats code after editing
- Supports TS/JS/Python/Go

**command-logger-example.json**:
- Logs all bash commands
- Audit trail for compliance

**notification-example.json**:
- Desktop notifications
- Alert when Claude needs input

**file-protection-example.json**:
- Blocks edits to sensitive files
- Protects .env, lock files, secrets

### Plugin Templates

Located in `templates/plugins/`:

**minimal-plugin/**: Bare-bones starting point
**full-featured-plugin/**: Complete example with all features

## Workflows

### Workflow 1: Building a Code Quality Plugin

1. **Create plugin structure**:
   ```
   /new-plugin code-quality-tools
   ```

2. **Add code review skill**:
   ```
   "Create a skill for reviewing code quality"
   ```

3. **Add auto-formatter hook**:
   ```
   "Add a hook to auto-format TypeScript after editing"
   ```

4. **Add quick review command**:
   ```
   /new-skill
   "Create a command called 'review' for quick code review"
   ```

5. **Test locally**:
   ```bash
   ln -s /path/to/code-quality-tools ~/.claude/marketplaces/dev/code-quality-tools
   /plugin install code-quality-tools@dev
   ```

6. **Share with team**:
   - Commit to git
   - Team adds to .claude/settings.json

### Workflow 2: Personal Productivity Toolkit

1. **Start simple**:
   ```
   "Create a skill for managing my daily todos"
   ```

2. **Add meeting notes helper**:
   ```
   "Create a skill for formatting meeting notes"
   ```

3. **Add quick command**:
   ```
   /new-skill
   "Create command /daily-standup for standup notes"
   ```

4. **Store in user directory**:
   - Skills → ~/.claude/skills/
   - Commands → ~/.claude/commands/
   - Available across all projects

### Workflow 3: Language-Specific Toolkit

1. **Create plugin for Python development**:
   ```
   /new-plugin python-dev-toolkit
   ```

2. **Add Python-specific skills**:
   ```
   "Create skill for Python code review with PEP 8"
   "Create skill for generating Python docstrings"
   "Create skill for Python test generation"
   ```

3. **Add hooks**:
   ```
   "Add hook to run black formatter after editing Python files"
   "Add hook to run mypy type checker"
   ```

4. **Add subagents**:
   ```
   "Create subagent for Python performance optimization"
   ```

## Tips & Best Practices

### Skill Creation Tips

**Good Descriptions**:
```yaml
# ✅ Good - includes triggers and keywords
description: Reviews code for security vulnerabilities. Activates when user discusses security review, vulnerability scanning, or code audits. Checks OWASP top 10. Use when user mentions "security", "vulnerabilities", "audit".

# ❌ Bad - too vague
description: Reviews code
```

**Tool Restrictions**:
```yaml
# ✅ Good - minimal tools needed
allowed-tools: Read, Grep, Glob  # For code review (read-only)

# ❌ Bad - too permissive for read-only task
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
```

**Naming**:
```yaml
# ✅ Good - descriptive with hyphens
name: api-doc-generator

# ❌ Bad - unclear or wrong format
name: apiDocs  # Should use hyphens, not camelCase
```

### Command Creation Tips

**Keep them focused**:
```markdown
# ✅ Good - single purpose
/run-tests - Run test suite

# ❌ Bad - too broad
/do-everything - Run tests, format code, deploy
```

**Use clear names**:
```markdown
# ✅ Good - obvious what it does
/review-pr
/format-code
/run-tests

# ❌ Bad - unclear
/doit
/check
/go
```

### Subagent Creation Tips

**Choose appropriate model**:
```yaml
# ✅ Good choices
model: haiku    # For simple formatting, validation
model: sonnet   # For code review, debugging (default)
model: opus     # For complex architecture, research

# ❌ Bad choice
model: opus     # For simple string validation (overkill)
```

**Restrict tools appropriately**:
```yaml
# ✅ Good - review agent doesn't need write access
tools: Read, Grep, Glob

# ❌ Bad - review agent with write access (risky)
tools: Read, Write, Edit, Bash, Grep, Glob
```

### Hook Creation Tips

**Keep hooks fast**:
```bash
# ✅ Good - quick operation
prettier --write "$FILE"

# ❌ Bad - slow operation that blocks
npm install && npm test && npm run build
```

**Handle errors gracefully**:
```bash
# ✅ Good - doesn't fail if prettier missing
prettier --write "$FILE" 2>/dev/null || true

# ❌ Bad - fails hard if prettier missing
prettier --write "$FILE"
```

**Use appropriate events**:
```json
// ✅ Good - format after editing
"PostToolUse": [{"matcher": "Edit", ...}]

// ❌ Bad - format before editing (weird)
"PreToolUse": [{"matcher": "Edit", ...}]
```

### General Tips

1. **Start with generators**: Use skill-generator, plugin-scaffolder, etc.
2. **Test incrementally**: Create one feature, test it, then add more
3. **Use templates**: Copy from templates/ and customize
4. **Validate often**: Use yaml-validator and structure-checker
5. **Document as you go**: Update README with each feature
6. **Version your changes**: Update plugin.json version
7. **Share thoughtfully**: Test thoroughly before team distribution

### Getting Help

**Use extensibility-advisor**:
```
"Should I create a skill or a hook for auto-formatting?"
→ Advisor explains trade-offs and recommends approach
```

**Ask about best practices**:
```
"What's the best way to create a code review workflow?"
→ Advisor suggests Skills + Hooks + Commands combination
```

**Validate your work**:
```
"Check if my plugin structure is correct"
→ structure-checker validates everything

"Validate the YAML in all my skills"
→ yaml-validator checks all frontmatter
```

## Troubleshooting

### Skill not activating

**Problem**: Created a skill but it doesn't activate
**Solutions**:
1. Check description includes trigger keywords
2. Verify YAML frontmatter is valid (use yaml-validator)
3. Test with explicit invocation first: "Use the X skill to..."
4. Ensure SKILL.md is in correct location

### Command not found

**Problem**: Created command but `/command-name` doesn't work
**Solutions**:
1. Verify filename matches command (my-command.md → /my-command)
2. Check file is in commands/ directory
3. Ensure plugin is installed and enabled: `/plugin`
4. Restart Claude Code session

### Hook not running

**Problem**: Created hook but it doesn't trigger
**Solutions**:
1. Verify hooks.json is valid JSON
2. Check event name is correct (case-sensitive)
3. Verify tool matcher matches the tool
4. Test hook command manually
5. Check Claude Code logs for errors

### Plugin won't install

**Problem**: Plugin doesn't show up or install fails
**Solutions**:
1. Verify .claude-plugin/plugin.json exists
2. Check plugin.json is valid JSON
3. Ensure plugin name in json matches directory name
4. Check marketplace configuration

---

**Need more help?** Use the extensibility-advisor skill or check the templates for working examples!
