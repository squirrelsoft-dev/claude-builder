# Security Policy

## Supported Versions

We release patches for security vulnerabilities. Currently supported versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |

## Reporting a Vulnerability

We take the security of Claude Builder seriously. If you believe you have found a security vulnerability, please report it to us as described below.

### Please do NOT:

- Open a public GitHub issue about the vulnerability
- Disclose the vulnerability publicly before it has been addressed

### Please DO:

1. **Report via GitHub Security Advisories**:
   - Go to the [Security tab](https://github.com/squirrelsoft-dev/claude-builder/security/advisories) of this repository
   - Click "Report a vulnerability"
   - Provide detailed information about the vulnerability

2. **Or report via Email** (if configured):
   - Include detailed steps to reproduce the vulnerability
   - Describe the potential impact
   - Provide any proof-of-concept code (if applicable)

### What to Include:

- Type of vulnerability (e.g., YAML injection, command injection, etc.)
- Full paths of affected source files
- Location of the affected code (tag/branch/commit or direct URL)
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the vulnerability, including how an attacker might exploit it

### Response Timeline:

- **Acknowledgment**: Within 48 hours
- **Initial Assessment**: Within 1 week
- **Fix Timeline**: Depends on severity
  - Critical: Within 7 days
  - High: Within 14 days
  - Medium: Within 30 days
  - Low: Within 60 days

## Security Considerations for Claude Builder

### Hook Security

Hooks execute shell commands with your environment credentials. Users should:

- Review all hook configurations before installing
- Never copy hooks from untrusted sources without review
- Be cautious with project-level hooks (affect all team members)
- Test hooks in isolation before deployment

### Skill/Subagent Tool Restrictions

When creating Skills or Subagents:

- Use minimal tool access needed (principle of least privilege)
- Read-only operations should only have Read, Grep, Glob
- Avoid giving full tool access unless necessary
- Review tool access before sharing with team

### Plugin Distribution

When distributing plugins:

- Review all code before distribution
- Use version control for audit trail
- Document all hooks and their actions
- Test thoroughly before team deployment

### Best Practices

1. **YAML Validation**: Always validate YAML frontmatter before use
2. **Structure Checking**: Use structure-checker before distribution
3. **Code Review**: Have team review shared plugins/skills
4. **Limited Scope**: Start with user-level, then expand to project-level
5. **Documentation**: Document what each component does

## Known Security Considerations

### Shell Command Execution (Hooks)

Hooks execute arbitrary shell commands. While this provides powerful automation:

- Commands run with user's full environment credentials
- Project-level hooks affect all team members
- Malicious hooks could access sensitive data or execute harmful commands

**Mitigation**:
- Review all hook configurations
- Use trusted sources only
- Test hooks in isolation
- Document hook behaviors

### YAML Frontmatter

YAML parsing can be vulnerable to injection attacks:

- The yaml-validator subagent helps catch malformed YAML
- Always validate before using community-shared configurations

**Mitigation**:
- Use yaml-validator on all Skills/Subagents
- Review YAML from untrusted sources
- Keep YAML simple and explicit

### Tool Access

Skills and Subagents can be granted different tool access levels:

- Full access includes Bash (arbitrary command execution)
- Write/Edit access can modify any file

**Mitigation**:
- Follow principle of least privilege
- Review tool restrictions before use
- Limit full access to trusted components

## Security Updates

Security updates will be released as patches to the current version. Users should:

- Watch the repository for security advisories
- Update to the latest version promptly
- Review changelog for security fixes

## Acknowledgments

We appreciate the security research community's efforts to responsibly disclose vulnerabilities. Contributors who report valid security issues will be acknowledged (with permission) in:

- Security advisories
- Release notes
- This SECURITY.md file

Thank you for helping keep Claude Builder and its users safe!
