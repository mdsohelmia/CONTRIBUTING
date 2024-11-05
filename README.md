# Enhanced Developer's Guide to Conventional Commits and Git Workflow 🚀

## Table of Contents
- [Quick Reference](#quick-reference)
- [Commit Message Structure](#commit-message-structure)
- [Branch Management](#branch-management)
- [Development Workflow](#development-workflow)
- [Common Scenarios](#common-scenarios)
- [Best Practices](#best-practices)

## Quick Reference

### Commit Format
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Most Used Types
- `feat`: New features
- `fix`: Bug fixes
- `refactor`: Code restructuring
- `docs`: Documentation updates
- `style`: Code formatting
- `test`: Test-related changes

### Common Scopes
- `auth`: Authentication/Authorization
- `api`: API endpoints/logic
- `ui`: User interface
- `core`: Core functionality
- `db`: Database related

## Branch Management

### Branch Types
```bash
feature/   # New features
bugfix/    # Bug fixes
hotfix/    # Urgent fixes for production
release/   # Release preparation
docs/      # Documentation updates
```

### Branch Naming
```bash
# Format
<type>/<ticket-number>-<brief-description>

# Examples
feature/AUTH-123-google-login
bugfix/UI-456-nav-alignment
hotfix/API-789-memory-leak
```

## Development Workflow

### 1. Starting New Work
```bash
# Update main branch
git checkout main
git pull --rebase origin main

# Create feature branch
git checkout -b feature/AUTH-123-google-login

# Create bugfix branch
git checkout -b bugfix/UI-456-nav-alignment
```

### 2. Daily Development
```bash
# Start of day
git checkout main
git pull --rebase origin main
git checkout feature/AUTH-123-google-login
git rebase main

# During development
git add <files>
git commit -m "feat(auth): implement Google OAuth flow

- Add OAuth2.0 client
- Implement token handling
- Add user profile mapping

Relates to AUTH-123"
```

### 3. Preparing for Review
```bash
# Update with latest changes
git checkout main
git pull --rebase origin main
git checkout feature/AUTH-123-google-login
git rebase main

# Review commits
git log --oneline main..HEAD

# Push changes
git push origin feature/AUTH-123-google-login
```

## Common Scenarios

### 1. Feature Development Sequence
```bash
# Initial setup
git commit -m "feat(auth): add Google OAuth structure

- Create service interfaces
- Add configuration templates
- Setup basic components"

# Implementation
git commit -m "feat(auth): implement OAuth login flow

- Add token handling
- Implement user mapping
- Add error handling"

# Testing
git commit -m "test(auth): add OAuth integration tests

- Add service mocks
- Test success flows
- Test error scenarios"

# Documentation
git commit -m "docs(auth): add OAuth setup guide

- Add configuration steps
- Document API usage
- Include examples"
```

### 2. Bug Fix Sequence
```bash
# Investigation commit
git commit -m "test(ui): reproduce navigation bug

- Add failing test case
- Document expected behavior
- Track related issues"

# Fix implementation
git commit -m "fix(ui): resolve navigation state sync

- Update state management
- Fix event handlers
- Add validation checks"

# Verification
git commit -m "test(ui): verify navigation fix

- Add regression tests
- Update existing tests
- Document edge cases"
```

## Best Practices

### 1. Commit Messages
✅ DO:
```bash
feat(auth): implement password reset flow
fix(api): handle null response from payment service
docs(readme): update deployment instructions
```

❌ DON'T:
```bash
update code
fix bug
WIP
```

### 2. Branch Management
✅ DO:
- Keep branches focused and small
- Regularly rebase with main
- Delete branches after merging

❌ DON'T:
- Mix multiple features in one branch
- Keep stale branches
- Push directly to main

### 3. Commit Organization
✅ DO:
- Group related changes
- Include tests with features
- Update documentation

❌ DON'T:
- Mix unrelated changes
- Skip tests
- Leave TODO comments

## Pre-Review Checklist

### Code Quality
```bash
# Run tests
npm run test

# Check linting
npm run lint

# Build verification
npm run build
```

### Git Hygiene
```bash
# Update with main
git rebase main

# Review changes
git log --oneline main..HEAD
git diff main

# Verify commit messages
git log --pretty=format:"%h %s"
```

### Final Checks
- [ ] All tests passing
- [ ] Documentation updated
- [ ] No debug code
- [ ] Commit messages follow convention
- [ ] Branch rebased with main

## Troubleshooting

### Common Issues

1. **Wrong Branch Base**
```bash
# Check current base
git merge-base HEAD main

# Rebase if needed
git rebase main
```

2. **Messy Commit History**
```bash
# Interactive rebase to clean up
git rebase -i main
```

3. **Conflict Resolution**
```bash
# During rebase
git rebase main

# If conflicts occur
git status
# Fix conflicts
git add <resolved-files>
git rebase --continue
```

Remember: The goal is to maintain a clean, traceable history while making the code review process efficient and effective.
