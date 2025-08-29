# Copilot Agent Instructions

## Required Validation Steps

### Before Considering Work Complete
1. **Always run ansible-lint** to ensure YAML files are properly formatted
   ```bash
   ansible-lint
   ```
2. **Run any existing tests** to validate changes don't break functionality
3. **Check git diff** to ensure changes are minimal and expected

### Development Best Practices
1. **Start with exploration** - understand existing code structure before making changes
2. **Run linting/testing early** - understand current state and any pre-existing issues
3. **Make surgical changes** - modify as few lines as possible to achieve the goal
4. **Test iteratively** - validate each change with appropriate linting/testing
5. **Review committed files** - use `git diff` to confirm only intended changes are included

### Quality Assurance
1. **YAML files must end with newlines** - ansible-lint requires this
2. **Use existing code patterns** - maintain consistency with project style
3. **Preserve working functionality** - only fix issues related to the current task
4. **Use ecosystem tools** - leverage npm, pip, ansible-galaxy, etc. for automation

### File Management
1. **Use `.gitignore`** - exclude build artifacts, dependencies, temp files
2. **Clean up temp files** - create temporary files in `/tmp` if needed
3. **Minimal commits** - only commit files directly related to the task

## Common Commands

### Ansible Validation
```bash
# Lint all files
ansible-lint

# Lint specific files
ansible-lint path/to/file.yml

# Check YAML syntax
ansible-playbook --syntax-check playbook.yml
```

### Git Workflow
```bash
# Check what files changed
git diff --name-only

# Review specific changes
git diff path/to/file

# Check line count changes
git diff --numstat
```

Remember: Quality over speed - always validate changes thoroughly before completion.