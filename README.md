# Git Workflow Guide - Commits and Branching

This guide establishes standard practices for branching strategies, commit conventions, and collaborative development workflows across all repositories.

## Branching Strategy

We follow a Feature-Flow branching strategy to ensure smooth collaboration and organized code management throughout the development lifecycle.

### Branch Types

1. **main**
   * The production branch containing stable, released code
   * Never commit directly to main
   * Changes merge from staging or hotfix branches only
   * Protected branch requiring pull request reviews

2. **development**
   * Primary integration branch for ongoing development
   * All features and bug fixes merge here after code review
   * Continuous integration and automated testing occur on this branch
   * Changes are tested before promotion to staging

3. **staging**
   * Pre-production branch reflecting tested features
   * Used for final quality assurance and user acceptance testing
   * Mirror of production environment for comprehensive testing
   * Changes merge to main after successful validation

### Feature Branches

Create feature branches for all development work:
* Branch from development for new features
* Branch from main for critical hotfixes
* Keep branches focused on single features or issues
* Delete branches after successful merge

## Branch Naming Convention

Use consistent naming patterns to improve organization and automation:

**Format:** `[branch-type]/[TICKET-ID]-[description]`

### Branch Types and Examples

**Feature Branches**
```
feature/PROJ-123-user-authentication
feature/PROJ-456-payment-integration
```

**Bug Fix Branches**
```
fix/PROJ-234-validation-error
fix/PROJ-567-memory-leak
```

**Task/Chore Branches**
```
task/PROJ-345-update-dependencies
task/PROJ-678-refactor-database-schema
```

**Hotfix Branches**
```
hotfix/PROJ-789-critical-security-patch
hotfix/PROJ-012-production-outage
```

**Release Branches**
```
release/v1.2.0
release/v2.0.0-beta
```

### Naming Guidelines

* Use lowercase letters and hyphens
* Keep descriptions concise but descriptive
* Include ticket/issue ID when available
* Avoid special characters and spaces
* Use present tense for actions (e.g., `add-feature` not `added-feature`)

## Commit Conventions

Follow conventional commit format for clear, searchable commit history:

**Format:** `type(scope): description`

### Commit Types

* **feat**: New feature or functionality
* **fix**: Bug fix or error correction
* **docs**: Documentation changes only
* **style**: Code formatting, missing semicolons (no logic change)
* **refactor**: Code restructuring without feature changes
* **test**: Adding or updating tests
* **chore**: Maintenance tasks, dependency updates
* **perf**: Performance improvements
* **ci**: Continuous integration changes
* **build**: Build system or external dependency changes

### Commit Examples

```bash
feat(auth): add JWT token validation
fix(api): resolve null pointer in user service
docs(readme): update installation instructions
style(components): format code according to prettier rules
refactor(database): extract query logic into separate service
test(auth): add unit tests for login functionality
chore(deps): update react to version 18.2.0
perf(queries): optimize database query performance
ci(github): add automated testing workflow
build(webpack): update build configuration for production
```

### Commit Message Guidelines

* Use imperative mood ("add feature" not "added feature")
* Keep first line under 50 characters
* Capitalize first letter of description
* No period at end of subject line
* Include detailed body for complex changes
* Reference issue numbers when applicable

**Multi-line Commit Example:**
```
feat(payment): integrate Stripe payment processing

- Add Stripe SDK integration
- Implement payment form validation
- Add error handling for failed transactions
- Update user interface for payment flow

Closes #PROJ-123
```

## Pull Request Guidelines

### PR Naming Convention

**Format:** `[TICKET-ID] (type) brief description`

**Examples:**
* `[PROJ-123] (feat) Add user authentication system`
* `[PROJ-456] (fix) Resolve payment validation error`
* `[PROJ-789] (task) Update API documentation`

### PR Process

1. **Create Branch** from appropriate base branch (usually development)
2. **Make Changes** following coding standards and conventions
3. **Commit Changes** using conventional commit format
4. **Push Branch** to remote repository
5. **Open Pull Request** with descriptive title and template
6. **Request Reviews** from relevant team members
7. **Address Feedback** through additional commits
8. **Merge** after approval and passing CI checks

### PR Description Template

```markdown
## What
[Describe the changes made in this PR]

## Why
[Explain the business reason or problem being solved]

## How
[Describe the technical approach and implementation details]

## Testing
[Describe testing performed and any special testing instructions]

## Screenshots/Demo
[Include visual evidence of changes when applicable]

## Checklist
- [ ] Code follows project coding standards
- [ ] Tests added or updated for new functionality
- [ ] Documentation updated if necessary
- [ ] No breaking changes introduced
- [ ] CI/CD pipeline passes
```

## Workflow Best Practices

### Before Starting Work
* Pull latest changes from development branch
* Create feature branch with descriptive name
* Ensure local environment is properly configured

### During Development
* Make small, focused commits with clear messages
* Push changes regularly to backup work
* Rebase feature branch periodically to stay current
* Write tests for new functionality

### Before Submitting PR
* Ensure all tests pass locally
* Review your own code for quality and standards
* Update documentation if necessary
* Squash commits if requested by team conventions

### After PR Approval
* Merge using appropriate strategy (merge commit, squash, or rebase)
* Delete feature branch after successful merge
* Verify deployment in staging environment
* Update project management tools with completion status

## Branch Protection Rules

Configure repository settings to enforce workflow:

* **main branch**: Require PR reviews, status checks, and up-to-date branches
* **development branch**: Require status checks and linear history
* **staging branch**: Require PR reviews and successful deployments

## Git Commands Reference

### Common Workflow Commands
```bash
# Start new feature
git checkout development
git pull origin development
git checkout -b feature/PROJ-123-new-feature

# Regular development cycle
git add .
git commit -m "feat(feature): implement new functionality"
git push origin feature/PROJ-123-new-feature

# Update feature branch with latest development
git checkout development
git pull origin development
git checkout feature/PROJ-123-new-feature
git rebase development

# Clean up after merge
git checkout development
git pull origin development
git branch -d feature/PROJ-123-new-feature
```

### Useful Git Aliases
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

This workflow ensures consistent, traceable, and collaborative development across all projects while maintaining code quality and deployment reliability.
