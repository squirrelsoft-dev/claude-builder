# Contributing to Claude Builder

Thank you for your interest in contributing to Claude Builder! This document provides guidelines for contributing to the project.

## Ways to Contribute

### 1. Add New Templates

**Skill Templates** (`templates/skills/`):
- Identify common use cases not covered by existing templates
- Create complete SKILL.md with YAML frontmatter
- Include comprehensive system prompt with methodology
- Add examples and best practices

**Agent Templates** (`templates/agents/`):
- Focus on specialized domains
- Include appropriate tool restrictions
- Suggest suitable model (Haiku/Sonnet/Opus)
- Provide domain expertise

**Hook Templates** (`templates/hooks/`):
- Common automation patterns
- Different hook events (PreToolUse, PostToolUse, etc.)
- Cross-platform when possible
- Include clear documentation

**Plugin Templates** (`templates/plugins/`):
- Complete working examples
- Different complexity levels
- Real-world use cases
- Comprehensive documentation

### 2. Improve Generator Skills

**skill-generator** improvements:
- Better defaults inference
- More pattern recognition
- Enhanced templates
- Improved suggestions

**plugin-scaffolder** improvements:
- Additional plugin patterns
- Better marketplace support
- Enhanced initialization

**subagent-generator** improvements:
- Better model recommendations
- Tool restriction patterns
- Domain-specific templates

**hook-generator** improvements:
- More hook templates
- Better event selection
- Enhanced validation

**extensibility-advisor** improvements:
- More decision frameworks
- Better recommendations
- Additional examples

### 3. Enhance Validation

**yaml-validator** improvements:
- Better error messages
- Auto-fix suggestions
- Batch validation
- Performance optimization

**structure-checker** improvements:
- More validation rules
- Auto-fix capabilities
- Better reporting
- Cross-platform path handling

### 4. Documentation

- Improve usage examples
- Add troubleshooting guides
- Create video tutorials
- Write blog posts
- Translate documentation

### 5. Bug Reports

- Report issues you encounter
- Provide reproduction steps
- Suggest fixes if possible
- Test on different platforms

## Contribution Process

### 1. Fork and Clone

```bash
# Fork on GitHub, then:
git clone https://github.com/YOUR-USERNAME/claude-builder.git
cd claude-builder
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

### 3. Make Changes

Follow the guidelines below for the type of contribution.

### 4. Test Thoroughly

```bash
# Create dev marketplace
mkdir -p ~/.claude/marketplaces/dev/.claude-plugin
echo '{"name":"dev","description":"Dev marketplace"}' > ~/.claude/marketplaces/dev/.claude-plugin/marketplace.json

# Link your modified plugin
ln -sf $(pwd) ~/.claude/marketplaces/dev/claude-builder

# Install
/plugin marketplace add ~/.claude/marketplaces/dev
/plugin install claude-builder@dev

# Test your changes thoroughly
```

### 5. Commit

```bash
git add .
git commit -m "Brief description of changes"
```

**Commit Message Guidelines**:
```
<type>: <description>

[optional body]

Types:
- feat: New feature
- fix: Bug fix
- docs: Documentation
- style: Formatting
- refactor: Code restructuring
- test: Adding tests
- chore: Maintenance
```

**Examples**:
```
feat: Add PostgreSQL optimization agent template

docs: Improve hook creation examples

fix: Correct YAML validation for optional fields

refactor: Simplify skill-generator tool selection logic
```

### 6. Push and Create PR

```bash
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub with:
- Clear description of changes
- Why the change is needed
- How to test it
- Screenshots if applicable

## Contribution Guidelines by Type

### Adding Skill Templates

**Location**: `templates/skills/[name]-SKILL.md`

**Requirements**:
1. **Valid YAML Frontmatter**:
   ```yaml
   ---
   name: skill-name
   description: Clear description with trigger keywords...
   allowed-tools: Tool1, Tool2  # Or omit for full access
   ---
   ```

2. **Comprehensive System Prompt**:
   - Clear purpose statement
   - Detailed methodology
   - Best practices
   - Examples
   - Output format specification

3. **Documentation**:
   - Add to templates/skills/README.md if one exists
   - Or create README documenting all skill templates

**Quality Checklist**:
- [ ] YAML frontmatter is valid
- [ ] Name follows conventions (lowercase-with-hyphens)
- [ ] Description includes activation triggers
- [ ] Tool restrictions are appropriate
- [ ] System prompt is detailed and actionable
- [ ] Examples are included
- [ ] Tested in actual use

### Adding Agent Templates

**Location**: `templates/agents/[name]-template.md`

**Requirements**:
1. **Valid YAML Frontmatter**:
   ```yaml
   ---
   name: agent-name
   description: When to invoke this agent...
   tools: Tool1, Tool2  # Optional
   model: sonnet  # Optional: sonnet/opus/haiku
   ---
   ```

2. **Specialized Expertise**:
   - Domain-specific knowledge
   - Clear methodology
   - Best practices for the domain
   - Example patterns

**Quality Checklist**:
- [ ] YAML frontmatter is valid
- [ ] Model selection is appropriate
- [ ] Tool restrictions make sense
- [ ] Expertise is clearly defined
- [ ] Methodology is detailed
- [ ] Domain knowledge is accurate
- [ ] Tested with real scenarios

### Adding Hook Templates

**Location**: `templates/hooks/[name]-example.json`

**Requirements**:
1. **Valid JSON**:
   ```json
   {
     "hooks": {
       "EventName": [
         {
           "matcher": "ToolName",
           "hooks": [
             {
               "type": "command",
               "comment": "What this hook does",
               "command": "shell command here"
             }
           ]
         }
       ]
     }
   }
   ```

2. **Documentation**:
   - Add to templates/hooks/README.md
   - Explain what the hook does
   - List requirements (tools like prettier, black, etc.)
   - Provide usage instructions

**Quality Checklist**:
- [ ] JSON is valid
- [ ] Event name is correct
- [ ] Tool matcher is appropriate
- [ ] Shell command works on target platforms
- [ ] Error handling is graceful
- [ ] Performance is acceptable
- [ ] Documented in README
- [ ] Tested on macOS/Linux/Windows (if applicable)

### Adding Plugin Templates

**Location**: `templates/plugins/[name]/`

**Requirements**:
1. **Complete Structure**:
   ```
   plugin-name/
   ├── .claude-plugin/
   │   └── plugin.json
   ├── skills/ (or other feature directories)
   └── README.md
   ```

2. **Valid plugin.json**:
   ```json
   {
     "name": "plugin-name",
     "description": "Clear description",
     "version": "1.0.0",
     "author": {
       "name": "Author Name"
     }
   }
   ```

3. **Comprehensive README**:
   - Installation instructions
   - Feature descriptions
   - Usage examples
   - Customization guide

**Quality Checklist**:
- [ ] Valid plugin.json
- [ ] All feature files valid (Skills, Commands, Agents, Hooks)
- [ ] README is comprehensive
- [ ] Installation tested
- [ ] Features work as documented
- [ ] Represents a useful pattern

### Improving Generator Skills

**Files**: `skills/*/SKILL.md`

**Types of Improvements**:

1. **Better Inference**:
   - Improve context analysis
   - Better default suggestions
   - More pattern recognition

2. **Enhanced Templates**:
   - Better structure generation
   - More comprehensive prompts
   - Improved examples

3. **Better Validation**:
   - Catch more errors
   - Provide better feedback
   - Suggest corrections

**Testing Requirements**:
- Test with various input scenarios
- Verify intelligent defaults work
- Check error handling
- Validate generated output

### Improving Validation Subagents

**Files**: `agents/yaml-validator.md`, `agents/structure-checker.md`

**Types of Improvements**:

1. **Better Validation Rules**:
   - Catch more issues
   - More specific error messages
   - Suggest fixes

2. **Enhanced Reporting**:
   - Clearer output
   - Better formatting
   - Actionable suggestions

3. **Performance**:
   - Faster validation
   - Batch processing
   - Efficient file scanning

### Documentation Improvements

**Files**: `README.md`, `USAGE.md`, `CONTRIBUTING.md`, template READMEs

**Types of Improvements**:
- Fix typos and errors
- Clarify confusing sections
- Add missing information
- Improve examples
- Add troubleshooting guides
- Create tutorials

**Documentation Standards**:
- Clear and concise
- Practical examples
- Step-by-step instructions
- Screenshots/diagrams when helpful
- Keep formatting consistent

## Testing Guidelines

### Testing Skills

1. **Activation Testing**:
   ```
   Test various phrases that should trigger the skill
   Verify skill activates correctly
   Check it doesn't activate incorrectly
   ```

2. **Functionality Testing**:
   ```
   Test the skill performs its purpose
   Verify tool restrictions work
   Check error handling
   Test edge cases
   ```

3. **Output Quality**:
   ```
   Verify output is helpful
   Check formatting is correct
   Ensure responses are accurate
   ```

### Testing Subagents

1. **Invocation Testing**:
   ```
   Test automatic delegation
   Test explicit invocation
   Verify description triggers correctly
   ```

2. **Isolation Testing**:
   ```
   Verify separate context
   Check model selection works
   Confirm tool restrictions
   ```

3. **Expertise Testing**:
   ```
   Test domain knowledge
   Verify methodology works
   Check output quality
   ```

### Testing Hooks

1. **Trigger Testing**:
   ```
   Verify hook fires on correct events
   Test tool matcher works
   Check timing (Pre vs Post)
   ```

2. **Command Testing**:
   ```
   Test shell command works
   Verify error handling
   Check performance impact
   Test cross-platform (if applicable)
   ```

3. **Integration Testing**:
   ```
   Test with actual workflow
   Verify doesn't break operations
   Check blocking behavior (PreToolUse)
   ```

### Testing Templates

1. **Validity Testing**:
   ```
   Use yaml-validator on Skills/Agents
   Use structure-checker on plugins
   Verify all JSON is valid
   ```

2. **Installation Testing**:
   ```
   Install from template
   Test all features work
   Verify documentation is accurate
   ```

3. **Customization Testing**:
   ```
   Follow customization instructions
   Verify changes work
   Test with real use cases
   ```

## Code Style

### YAML Frontmatter

```yaml
---
name: lowercase-with-hyphens
description: Start with purpose. Include trigger keywords. Be specific.
allowed-tools: Tool1, Tool2  # Only if restricting
model: sonnet  # Only for subagents, only if not default
---
```

### Markdown

- Use headers appropriately (# for title, ## for sections)
- Keep lines under 100 characters when possible
- Use code blocks with language specification
- Use lists for multiple items
- Use emphasis sparingly

### JSON

- 2-space indentation
- No trailing commas
- Quote all keys and string values
- Use comments (via "comment" fields in hooks)

### Shell Commands

- Quote variables: `"$FILE"` not `$FILE`
- Handle errors gracefully: `|| true` for non-critical
- Be cross-platform when possible
- Keep commands fast

## Review Process

### What We Look For

1. **Functionality**: Does it work as intended?
2. **Quality**: Is the code/content high quality?
3. **Testing**: Has it been tested thoroughly?
4. **Documentation**: Is it well documented?
5. **Consistency**: Does it match existing patterns?
6. **Value**: Does it add meaningful value?

### Response Time

- Initial response: Within 1 week
- Review iterations: Within 3-5 days
- Merge: When approved and tests pass

### Feedback

- Be constructive and respectful
- Explain the "why" behind suggestions
- Provide examples when helpful
- Recognize good work

## Questions?

- Open an issue for questions
- Check existing issues/PRs
- Review documentation
- Ask in pull request comments

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Credited in related documentation

Thank you for contributing to Claude Builder! 🎉
