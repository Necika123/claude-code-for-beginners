# Module 7: Git Operations and Version Control

**Goal:** Master Git workflows with Claude Code's assistance

**Estimated Time:** 40-50 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand Git basics and why version control matters
- Know how to create meaningful commits with Claude Code
- Learn to work with branches effectively
- Master creating pull requests with AI-generated descriptions
- Understand how to review code before committing
- Learn to resolve merge conflicts with Claude Code's help
- Know how to use GitHub CLI integration

---

## Lesson 1: Why Version Control Matters

### What is Version Control?

**Version control** is a system that tracks changes to your code over time. Think of it as:
- **Unlimited undo** - Go back to any previous version
- **Collaboration** - Work with others without conflicts
- **History** - See what changed, when, and why
- **Safety net** - Experiment without fear of breaking things

### Git Basics

**Key concepts:**

**Repository (Repo)**
- A project tracked by Git
- Contains all files and history
- Can be local or remote (GitHub, GitLab, etc.)

**Commit**
- A snapshot of your code at a point in time
- Has a message describing what changed
- Creates a permanent record

**Branch**
- A parallel version of your code
- Lets you work on features without affecting main code
- Can be merged back later

**Remote**
- A version of your repo on a server (like GitHub)
- Lets you backup and collaborate
- Usually called "origin"

---

## Lesson 2: Basic Git Operations with Claude Code

### Checking Status

**See what's changed:**
```
Show me git status
What files have I modified?
```

Claude Code will run:
```bash
git status
```

**Output shows:**
- Modified files
- New files (untracked)
- Deleted files
- Files staged for commit

---

### Viewing Changes

**See what you've changed:**
```
Show me the git diff
What changes have I made to auth.js?
```

Claude Code will show:
- Lines added (green, with +)
- Lines removed (red, with -)
- Context around changes

**Example output:**
```diff
- const PORT = 3000;
+ const PORT = 8080;
```

---

### Creating Commits with Claude Code

This is where Claude Code really shines!

**Manual way (old):**
```bash
git add .
git commit -m "Updated the thing"  # Vague, unhelpful
```

**With Claude Code (new):**
```
Please create a commit with my current changes
```

**What Claude Code does:**
1. Runs `git status` to see changes
2. Runs `git diff` to see what changed
3. Analyzes the changes
4. Writes a meaningful commit message
5. Creates the commit with proper formatting

**Example commit message Claude Code might write:**
```
Add user authentication with JWT tokens

- Implement login and register endpoints
- Add bcrypt for password hashing
- Create JWT middleware for protected routes
- Add user model and database schema
- Include input validation for auth requests

This provides secure user authentication for the API.
```

**Much better than "fixed stuff"!**

---

### Commit Message Best Practices

**Claude Code follows these conventions:**

**Structure:**
```
Brief summary (50 chars or less)

Longer description if needed:
- What changed
- Why it changed
- Any important details

Issue references: #123
```

**Good vs Bad:**

❌ **Bad:**
```
- "fixed bug"
- "updated code"
- "changes"
- "asdfasdf"
```

✅ **Good:**
```
- "Fix login error when password is empty"
- "Add email validation to user registration"
- "Refactor database connection for better error handling"
- "Update API endpoints to use async/await"
```

---

## Lesson 3: Working with Branches

### Why Use Branches?

**Branches let you:**
- Work on features without breaking main code
- Try experiments safely
- Collaborate without conflicts
- Organize different types of work

### Creating Branches with Claude Code

**Create a new branch:**
```
Create a new branch called feature/user-dashboard
```

Claude Code will:
```bash
git checkout -b feature/user-dashboard
```

**Or:**
```
Create a feature branch for adding password reset
```

Claude Code might create:
```bash
git checkout -b feature/password-reset
```

### Branch Naming Conventions

**Common patterns:**
```
feature/feature-name    # New features
bugfix/bug-description  # Bug fixes
hotfix/critical-fix     # Urgent fixes
refactor/what-refactor  # Code improvements
docs/what-documentation # Documentation
```

**Examples:**
```
feature/user-authentication
bugfix/login-validation-error
hotfix/security-vulnerability
refactor/database-queries
docs/api-endpoints
```

### Switching Branches

**Switch to existing branch:**
```
Switch to the main branch
```

```bash
git checkout main
```

**Or:**
```
Switch back to my feature branch
```

---

### Merging Branches

**Merge feature into main:**
```
Merge the feature/user-dashboard branch into main
```

Claude Code will:
1. Switch to main
2. Pull latest changes
3. Merge the feature branch
4. Handle any conflicts (more on this later)

---

## Lesson 4: Creating Pull Requests

### What is a Pull Request (PR)?

A **Pull Request** is:
- A request to merge your code into another branch
- Used for code review
- Discussion platform for changes
- Quality control mechanism

### Creating PRs with Claude Code

**This is incredibly powerful!**

**Simple request:**
```
Create a pull request for my changes
```

**What Claude Code does:**

1. **Analyzes all commits** in your branch
2. **Reviews the code changes**
3. **Generates a comprehensive PR description:**
   - Summary of changes
   - List of modifications
   - Test plan
   - Screenshots (if applicable)
4. **Uses GitHub CLI to create the PR**

**Example PR description Claude Code might generate:**

```markdown
## Summary

This PR adds user authentication to the application using JWT tokens.

## Changes

- ✨ Add login and registration endpoints
- 🔒 Implement JWT token generation and validation
- 🛡️ Add password hashing with bcrypt
- ✅ Create authentication middleware
- 📝 Add user model and database schema
- ✔️ Include comprehensive input validation

## Implementation Details

### Authentication Flow
1. User registers with email/password
2. Password is hashed using bcrypt (10 rounds)
3. User credentials stored in database
4. On login, credentials are verified
5. JWT token generated and returned
6. Token required for protected routes

### Security Measures
- Passwords hashed before storage
- JWT tokens expire after 24 hours
- Input validation on all auth endpoints
- SQL injection prevention with prepared statements

## Test Plan

- [ ] Test user registration with valid data
- [ ] Test registration with invalid email
- [ ] Test registration with weak password
- [ ] Test login with correct credentials
- [ ] Test login with wrong password
- [ ] Test protected routes without token
- [ ] Test protected routes with valid token
- [ ] Test protected routes with expired token

## Database Changes

Added `users` table:
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  password TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

## Dependencies Added

- jsonwebtoken: JWT creation and verification
- bcrypt: Password hashing
- express-validator: Input validation

---

Generated with Claude Code
```

**That's way better than manually writing all that!**

---

### Customizing PR Creation

**Be specific about what you want:**

```
Create a pull request with:
- Title: "Add user authentication"
- Target branch: develop (not main)
- Include screenshots from /screenshots folder
- Mark as draft
```

---

## Lesson 5: Code Review Before Committing

### Why Review First?

**Benefits:**
- Catch mistakes before they're committed
- Understand what you're committing
- Learn from the changes
- Verify quality

### Review Workflow with Claude Code

**Step 1: See what changed**
```
Show me all the changes I'm about to commit
```

**Step 2: Review specific files**
```
Show me the diff for auth.js
Explain what changed in the database schema
```

**Step 3: Check for issues**
```
Review my changes and check for:
- Security vulnerabilities
- Code quality issues
- Missing error handling
- Inconsistent style
```

**Step 4: Make fixes if needed**
```
Fix the security issue you found in login.js
```

**Step 5: Commit when ready**
```
Now create a commit with these changes
```

---

## Lesson 6: Resolving Merge Conflicts

### What are Merge Conflicts?

**Conflicts occur when:**
- Two branches change the same line
- Git doesn't know which change to keep
- You must manually decide

**Example conflict:**
```javascript
<<<<<<< HEAD
const PORT = 3000;
=======
const PORT = 8080;
>>>>>>> feature/new-port
```

### Resolving Conflicts with Claude Code

**When you get a conflict:**
```
I have a merge conflict in server.js. Help me resolve it.
```

**Claude Code will:**
1. Show you the conflict
2. Explain both versions
3. Ask which to keep (or suggest combining)
4. Resolve the conflict
5. Mark as resolved

**Example dialogue:**
```
Claude Code: I see a conflict in server.js with the PORT value.
- HEAD (main branch): PORT = 3000
- feature/new-port: PORT = 8080

Which would you like to keep? Or should we make it configurable with an environment variable?

You: Make it configurable

Claude Code: I'll update it to use process.env.PORT with 8080 as default.
```

---

## Lesson 7: GitHub CLI Integration

### What is GitHub CLI (gh)?

**gh** is GitHub's official command-line tool. Claude Code can use it to:
- Create pull requests
- List issues
- View PR status
- Check CI/CD results
- Manage releases

### Common gh Operations

**View PRs:**
```
Show me all open pull requests
```

**Create issue:**
```
Create a GitHub issue for the bug I just found:
Title: Login fails with empty password
Description: [your description]
```

**Check PR status:**
```
What's the status of PR #42?
Has it passed all checks?
```

**Merge PR:**
```
Merge pull request #42
```

---

## Lesson 8: Complete Git Workflow Example

### Scenario: Adding a New Feature

**Step 1: Create feature branch**
```
Create a new branch for adding password reset feature
```

**Step 2: Make changes**
```
Implement password reset functionality with:
- Request reset endpoint
- Reset token generation
- Password update endpoint
- Email sending (simulated)
```

**Step 3: Test your changes**
```
Run the tests
```

**Step 4: Review changes**
```
Show me all changes I made
Review for any security issues
```

**Step 5: Commit**
```
Create a commit for the password reset feature
```

**Step 6: Push to remote**
```
Push this branch to GitHub
```

**Step 7: Create PR**
```
Create a pull request for this feature
Target: main branch
Include:
- Summary of functionality
- Testing steps
- Security considerations
```

**Step 8: Address review comments**
```
The PR review asked to add rate limiting to prevent abuse.
Add rate limiting to the reset endpoints.
```

**Step 9: Update PR**
```
Add a commit with the rate limiting changes
Push the update
```

**Step 10: Merge**
```
Merge the pull request
```

**Step 11: Clean up**
```
Delete the feature branch locally and remotely
Switch back to main
Pull the latest changes
```

---

## Hands-On Practice

### Exercise 1: Basic Git Workflow

**Task:** Make a change and commit it properly

**Steps:**
1. Create a test file: "Create a file called test.js with a hello function"
2. Check status: "Show me git status"
3. Review changes: "Show me the diff"
4. Commit: "Create a commit with this change"
5. View history: "Show me the git log"

---

### Exercise 2: Feature Branch Workflow

**Task:** Create a feature on a branch

**Steps:**
1. "Create a new branch called feature/add-tests"
2. "Create a test file for the hello function"
3. "Show me what I've changed"
4. "Commit the test file"
5. "Switch back to main"
6. "Merge the feature branch"

---

### Exercise 3: Pull Request Workflow

**Task:** Create a proper pull request

**Steps:**
1. "Create a branch for adding documentation"
2. "Create a README.md for this project"
3. "Review my changes"
4. "Commit the README"
5. "Push to GitHub"
6. "Create a pull request"

---

## Module 7 Checklist

Before moving to Module 8, make sure you can:

- [ ] Check Git status and view changes
- [ ] Create meaningful commits with Claude Code
- [ ] Work with branches (create, switch, merge)
- [ ] Generate good commit messages
- [ ] Create pull requests with comprehensive descriptions
- [ ] Review code before committing
- [ ] Resolve merge conflicts
- [ ] Use GitHub CLI through Claude Code

---

## Git Safety Tips

### Do's

✅ **Commit working code** - Make sure it works before committing
✅ **Write clear messages** - Let Claude Code help
✅ **Review before committing** - Check what you're committing
✅ **Use branches** - Keep main branch stable
✅ **Pull before push** - Get latest changes first
✅ **Push regularly** - Backup your work

### Don'ts

❌ **Don't commit broken code** - Test first
❌ **Don't commit secrets** - API keys, passwords, etc.
❌ **Don't force push to main** - Dangerous!
❌ **Don't skip commit messages** - Future you will thank you
❌ **Don't commit large files** - Use .gitignore
❌ **Don't edit history on shared branches** - Creates conflicts

---

## Common Questions (FAQ)

### Q: Should I commit after every small change?
**A:** Commit when you have a logical, working unit of functionality. Not too small (every line) or too big (entire feature).

### Q: How often should I push to GitHub?
**A:** At least daily, and always when you have working features. More frequent is better for backup.

### Q: Can Claude Code write commit messages for any project?
**A:** Yes! It analyzes your actual code changes, not just your description.

### Q: What if I accidentally committed something I shouldn't have?
**A:** Tell Claude Code: "I accidentally committed [file]. Help me remove it from the last commit"

### Q: How do I see old commits?
**A:** "Show me the git log" or "Show me commits from the last week"

---

## What's Next?

Excellent work! You now know how to:
- Use Git effectively with Claude Code
- Create meaningful commits
- Work with branches
- Generate comprehensive pull requests
- Review code before committing
- Resolve conflicts

**Ready for Module 8?** In the next module, we'll learn about debugging and testing with Claude Code!

---

## Pro Tips

1. **Always review before committing** - Understand what's being committed

2. **Use Claude Code for commit messages** - They'll be better than yours (no offense!)

3. **Create small, focused commits** - Easier to understand and revert if needed

4. **Branch for every feature** - Keep work isolated

5. **Use descriptive branch names** - feature/what-it-does

6. **Let Claude Code write PR descriptions** - Saves time, more comprehensive

7. **Commit working code** - Don't commit broken features

---

*Module 7 Complete!*
