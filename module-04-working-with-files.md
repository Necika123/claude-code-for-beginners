# Module 4: Working with Files and Code

**Goal:** Learn how to effectively read, write, and modify code with Claude Code

**Estimated Time:** 40-50 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Read and understand existing codebases effectively
- Write clean, well-structured code with AI assistance
- Make precise edits without breaking existing functionality
- Refactor code to improve quality
- Navigate large codebases efficiently
- Learn from existing code patterns

---

## Lesson 1: Reading and Understanding Code

### Why Reading Code Matters

**80% of programming is reading code, not writing it.**

You'll need to read code to:
- Understand how existing features work
- Find bugs
- Add new features
- Learn patterns and best practices
- Review others' code

### Reading Single Files

**Ask Claude Code to read and explain:**

```
Read server.js and explain what it does
```

**Claude Code will:**
- Show you the file contents
- Explain the main purpose
- Highlight key functions
- Point out important patterns

**For specific parts:**
```
Read the login function in auth.js and explain how it works
```

**For understanding structure:**
```
Read package.json and tell me:
- What dependencies are used
- What scripts are available
- What's the entry point
```

---

### Reading Multiple Related Files

**Understanding a feature across files:**

```
I want to understand how user authentication works.
Please read:
- routes/auth.js
- middleware/auth.js
- models/user.js
And explain the complete authentication flow
```

**Claude Code will:**
- Read all specified files
- Trace the execution flow
- Explain how they work together
- Show the data flow

---

### Understanding Project Structure

**Get the big picture:**

```
Help me understand this project's structure.
Show me:
- The directory layout
- What each folder contains
- The entry point
- How the code is organized
```

**Or use the Explore agent:**
```
Use the Explore agent to analyze this codebase and give me:
1. Overall architecture
2. Main components
3. Technology stack
4. How data flows through the system
```

---

### Reading Patterns and Conventions

**Learn how the codebase does things:**

```
Show me how error handling is done in this project
Find examples of API endpoints and show me the pattern
How are database queries organized?
```

**Benefits:**
- Learn project conventions
- Follow existing patterns
- Maintain consistency
- Avoid reinventing solutions

---

## Lesson 2: Writing New Code

### Following Project Conventions

**Before writing, understand conventions:**

```
Before I add a new feature, show me:
- How routes are structured
- How controllers are organized
- Error handling patterns
- Naming conventions used
```

**Then write following patterns:**
```
Add a new route for /api/products following the same pattern as /api/users
```

---

### Writing Clean Code

**Request clean code explicitly:**

```
Create a function to validate email addresses with:
- Clear variable names
- Input validation
- Error messages
- JSDoc comments
- Unit testable structure
```

**Claude Code will write:**
```javascript
/**
 * Validates an email address format
 * @param {string} email - The email address to validate
 * @returns {boolean} True if valid, false otherwise
 * @throws {TypeError} If email is not a string
 */
function validateEmail(email) {
  if (typeof email !== 'string') {
    throw new TypeError('Email must be a string');
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}
```

---

### Writing Modular Code

**Request separation of concerns:**

```
Create a user service module that handles:
- Creating users
- Finding users
- Updating users
- Deleting users

Keep database logic separate from business logic
Export all functions
```

**Result:**
```
services/
  └── userService.js  (business logic)
database/
  └── userRepository.js  (database operations)
```

---

### Adding Documentation

**Request docs as you write:**

```
Create a calculateTax function and include:
- JSDoc comments
- Parameter descriptions
- Return value description
- Example usage in comments
```

---

## Lesson 3: Editing Existing Code

### Making Precise Changes

The **Edit tool** is Claude Code's most powerful feature for modifications.

**Simple change:**
```
In config.js, change the database port from 5432 to 3306
```

**Claude Code shows:**
```diff
Old:
const DB_PORT = 5432;

New:
const DB_PORT = 3306;
```

**Adding to existing code:**
```
In the login function, add validation to check if the password is at least 8 characters
```

**Removing code:**
```
Remove the console.log statements from auth.js
```

---

### Preserving Existing Patterns

**Follow existing style:**

```
Add a new endpoint for deleting users.
Follow the same pattern as the existing endpoints in routes/users.js
```

**Claude Code will:**
- Read existing endpoints
- Match the structure
- Use same error handling
- Follow naming conventions

---

### Making Safe Edits

**Review before applying:**

```
Show me what you would change to add error handling to the database connection, but don't make the changes yet
```

**After reviewing:**
```
That looks good, please apply the changes
```

---

### Editing Multiple Files

**For changes across files:**

```
Add TypeScript types for the User model.
Update:
- models/user.js (rename to user.ts)
- All files that import User
- Type definitions
```

**Claude Code will:**
- Make changes in correct order
- Update all imports
- Ensure consistency
- Test that nothing breaks

---

## Lesson 4: Refactoring Code

### What is Refactoring?

**Refactoring** = Improving code structure without changing functionality

**Goals:**
- Improve readability
- Reduce complexity
- Remove duplication
- Enhance maintainability

---

### Removing Code Duplication

**Find duplication:**
```
Look for duplicate code in the routes files and suggest refactoring
```

**Refactor it:**
```
I see the validation logic is duplicated in routes/users.js and routes/posts.js.
Extract it into a reusable validation module.
```

**Result:**
```
Before:
routes/users.js - validation logic
routes/posts.js - same validation logic

After:
middleware/validation.js - shared validation
routes/users.js - uses validation middleware
routes/posts.js - uses validation middleware
```

---

### Improving Function Structure

**Break down large functions:**

```
The processOrder function is 150 lines long.
Refactor it into smaller, focused functions.
```

**Claude Code will:**
- Identify logical sections
- Extract into separate functions
- Keep same functionality
- Add clear names

---

### Renaming for Clarity

```
The variable 'x' in calculateTotal is unclear.
Rename it to something descriptive.
```

```javascript
// Before
function calculateTotal(x) {
  return x * 1.08;
}

// After
function calculateTotal(subtotal) {
  const TAX_RATE = 1.08;
  return subtotal * TAX_RATE;
}
```

---

### Modernizing Code

**Update to modern syntax:**

```
Refactor auth.js to use:
- async/await instead of callbacks
- const/let instead of var
- Arrow functions where appropriate
- Template literals instead of concatenation
```

---

### Optimizing Performance

```
The search function is slow with large datasets.
Optimize it for better performance.
```

**Claude Code might:**
- Add caching
- Use more efficient algorithms
- Add indexes
- Implement pagination

---

## Lesson 5: Navigating Large Codebases

### Finding Specific Code

**Use Grep to search:**

```
Find all places where the sendEmail function is called
```

```
Search for all TODO comments in the codebase
```

```
Find all database queries that use the users table
```

---

### Finding Files

**Use Glob for files:**

```
Find all test files
```

```
Find all TypeScript files in the src directory
```

```
Show me all configuration files
```

---

### Understanding Code Flow

**Trace execution:**

```
Trace the execution flow when a user logs in.
Start from the API endpoint and show me each step.
```

**Claude Code will:**
- Find the endpoint
- Show middleware chain
- Follow function calls
- Show database queries
- Explain the complete flow

---

### Finding Dependencies

**Understand what uses what:**

```
What files depend on the User model?
```

```
Show me all components that import the API service
```

**With LSP tool:**
```
Find all references to the authenticateUser function
```

---

## Lesson 6: Learning from Existing Code

### Pattern Recognition

**Learn by example:**

```
Show me 3 examples of how API endpoints are structured in this project
```

**Then apply:**
```
Now create a new endpoint following that same pattern
```

---

### Understanding Best Practices

```
Analyze the error handling in this codebase and explain:
- What patterns are used
- Why they work well
- How I should handle errors in my new code
```

---

### Code Review for Learning

```
Review the authentication module and teach me:
- What security measures are in place
- Why each is important
- What I should do in similar code
```

---

## Lesson 7: File Organization Strategies

### Creating Logical Structure

**Ask for project structure:**

```
I'm building a REST API.
Create a project structure with:
- Clear separation of concerns
- Routes, controllers, services, models
- Test files organized with source files
- Configuration in separate folder
```

---

### Organizing by Feature

```
Reorganize this codebase from:
- Files by type (all controllers together)
To:
- Files by feature (user feature has its own folder with controller, service, model, tests)
```

---

### Managing Large Files

```
This server.js file is 500 lines.
Help me split it into logical modules.
```

---

## Hands-On Practice

### Exercise 1: Reading Code

**Task:** Understand an unfamiliar codebase

**Choose any open source project and:**

1. Clone it
2. Ask: "Explain what this project does and how it's structured"
3. Ask: "Show me the main entry point and explain the initialization"
4. Ask: "Find the core business logic and explain how it works"

---

### Exercise 2: Writing Clean Code

**Task:** Create a well-structured module

```
Create a blog post service module with:
- createPost(title, content, authorId)
- getPostById(id)
- updatePost(id, updates)
- deletePost(id)
- listPosts(options) with pagination

Requirements:
- Input validation for all functions
- Descriptive variable names
- JSDoc comments
- Error handling
- Return consistent response format
```

---

### Exercise 3: Refactoring

**Task:** Improve existing code

**First, create messy code:**
```
Create a function that calculates shipping cost.
Make it poorly structured with unclear variable names.
```

**Then refactor:**
```
Refactor the calculateShipping function to:
- Use descriptive variable names
- Extract magic numbers to constants
- Add comments
- Improve readability
- Handle edge cases
```

---

### Exercise 4: Navigating Code

**Task:** Find specific functionality

**In a project with multiple files:**

1. "Find all database query functions"
2. "Show me where the User model is defined"
3. "Find all API routes"
4. "Trace what happens when POST /api/login is called"

---

## Module 4 Checklist

Before moving to Module 5, make sure you can:

- [ ] Read and understand existing code
- [ ] Write clean, well-structured new code
- [ ] Make precise edits using the Edit tool
- [ ] Refactor code to improve quality
- [ ] Navigate large codebases efficiently
- [ ] Find specific code using Grep and Glob
- [ ] Follow and apply existing code patterns
- [ ] Organize code logically

---

## Best Practices

### Reading Code

✅ Start with README and package.json
✅ Understand structure before details
✅ Trace execution flows
✅ Look for patterns
✅ Ask for explanations of unclear parts

### Writing Code

✅ Follow existing conventions
✅ Use descriptive names
✅ Add comments for complex logic
✅ Keep functions focused and small
✅ Validate inputs
✅ Handle errors properly

### Editing Code

✅ Review changes before applying
✅ Make small, focused changes
✅ Test after each change
✅ Preserve existing patterns
✅ Don't break existing functionality

### Refactoring

✅ Test before refactoring
✅ Make one change at a time
✅ Keep functionality identical
✅ Test after each refactor
✅ Commit working code before big refactors

---

## Common Questions (FAQ)

### Q: How do I know if my code is "clean"?
**A:** Ask Claude Code! "Review this code for clarity and suggest improvements"

### Q: When should I refactor?
**A:** When code is hard to understand, duplicated, or becoming difficult to modify.

### Q: How do I learn coding patterns?
**A:** Read good code, ask Claude Code to explain patterns, and practice implementing them.

### Q: What if I break something while editing?
**A:** Use Git! Commit before making changes so you can always revert.

### Q: How detailed should my edit requests be?
**A:** Be specific about what to change, but let Claude Code handle the implementation details.

---

## What's Next?

Excellent work! You now know how to:
- Read and understand code effectively
- Write clean, maintainable code
- Make safe, precise edits
- Refactor for better quality
- Navigate large codebases

**Ready for Module 5?** In the next module, we'll master prompt engineering - how to communicate coding tasks effectively to get the best results!

---

## Pro Tips

1. **Always read before modifying** - Understand the code first

2. **Follow the principle of least surprise** - Match existing patterns

3. **Refactor in small steps** - Don't try to perfect everything at once

4. **Use meaningful names** - Code is read more than written

5. **Ask Claude Code to explain** - Learn from the code you're working with

6. **Test incrementally** - Verify changes work before moving on

7. **Git commit frequently** - Safety net for experiments

---

*Module 4 Complete!*
