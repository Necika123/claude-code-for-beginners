# Module 6: Using Background Agents

**Goal:** Learn to use specialized agents for complex, multi-step tasks

**Estimated Time:** 35-45 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand what agents are and when to use them
- Know the different types of specialized agents
- Learn to use the Explore agent for codebase navigation
- Master the Plan agent for implementation design
- Use general-purpose agents for complex tasks
- Run agents in parallel for efficiency
- Interpret and act on agent results

---

## Lesson 1: What Are Agents?

### Understanding Agents

**Agents** are specialized AI assistants that work autonomously to complete complex tasks. Think of them as experts you can call in for specific jobs.

**Key differences from regular conversation:**

**Regular Claude Code:**
- You guide each step
- Interactive back-and-forth
- You make decisions

**Agent Mode:**
- Works autonomously
- Makes its own decisions
- Completes multi-step tasks independently
- Reports back when done

---

### When to Use Agents

**Use agents for:**
- Complex tasks requiring multiple steps
- Exploring unfamiliar codebases
- Planning implementations
- Research tasks
- Tasks that need decision-making

**Use regular conversation for:**
- Simple, single-step tasks
- When you want to guide each step
- Learning (seeing each tool use)
- Quick modifications

---

## Lesson 2: The Explore Agent

### What is the Explore Agent?

**Purpose:** Navigate and understand codebases quickly

**Best for:**
- Understanding how a project works
- Finding where functionality is implemented
- Analyzing architecture
- Learning from unfamiliar code

---

### Using the Explore Agent

**Basic usage:**
```
Use the Explore agent to understand how authentication works in this codebase
```

**What the agent does:**
1. Searches for auth-related files
2. Reads relevant code
3. Analyzes the implementation
4. Traces the flow
5. Returns comprehensive explanation

---

### Explore Agent Examples

**Example 1: Understanding a Feature**
```
Use the Explore agent to explain how the payment processing works.
I need to know:
- What payment providers are supported
- How transactions are stored
- What security measures are in place
- The complete flow from checkout to confirmation
```

**The agent will:**
- Find all payment-related files
- Read configuration
- Trace the payment flow
- Analyze security implementations
- Provide detailed report

---

**Example 2: Finding API Endpoints**
```
Explore the codebase and list all API endpoints with:
- HTTP method
- Route path
- What each endpoint does
- Required parameters
```

**The agent returns:**
```
API Endpoints Found:

POST /api/auth/login
- Authenticates user with email/password
- Requires: email, password
- Returns: JWT token

GET /api/users
- Lists all users
- Requires: Admin authentication
- Returns: Array of user objects

POST /api/users
- Creates new user
- Requires: name, email, password
- Returns: Created user object

... (and so on)
```

---

**Example 3: Understanding Architecture**
```
Use the Explore agent to analyze this codebase and explain:
- Overall architecture pattern (MVC, layered, etc.)
- How different parts communicate
- Database structure
- External dependencies
```

---

### Specifying Thoroughness

**You can control how deep the agent explores:**

**Quick exploration:**
```
Use the Explore agent with quick thoroughness to give me an overview of this project
```

**Medium exploration:**
```
Use the Explore agent with medium thoroughness to understand the authentication system
```

**Thorough exploration:**
```
Use the Explore agent with very thorough analysis to document the entire API
```

---

## Lesson 3: The Plan Agent

### What is the Plan Agent?

**Purpose:** Design implementation strategies before coding

**Best for:**
- Planning new features
- Designing system architecture
- Thinking through complex changes
- Avoiding mistakes before they happen

---

### Using the Plan Agent

**Basic usage:**
```
Use the Plan agent to create an implementation plan for adding user roles and permissions
```

**What the agent does:**
1. Analyzes current codebase
2. Identifies what needs to change
3. Plans the steps
4. Considers edge cases
5. Returns detailed plan

---

### Plan Agent Examples

**Example 1: Adding a Feature**
```
I want to add email notifications when users receive messages.

Use the Plan agent to create an implementation plan including:
- Database changes needed
- New code to write
- Existing code to modify
- Testing strategy
- Potential issues to watch for
```

**Agent returns:**
```
Implementation Plan: Email Notifications for Messages

1. Database Schema Changes
   - Add notifications table:
     * id, user_id, message_id, sent_at, status
   - Add email_notifications_enabled to users table

2. New Code to Create
   - services/emailService.js
     * sendMessageNotification(user, message)
     * Uses configured email provider
   - jobs/emailNotificationJob.js
     * Background job for sending emails
     * Handles retries and failures

3. Existing Code to Modify
   - routes/messages.js
     * After creating message, queue notification
   - models/User.js
     * Add preference methods

4. Configuration
   - Add email provider settings to config
   - Environment variables for email credentials

5. Testing Strategy
   - Unit tests for emailService
   - Integration tests for notification flow
   - Test email preferences
   - Test failure scenarios

6. Potential Issues
   - Email provider rate limits
   - Handling bounced emails
   - User privacy concerns
   - Performance impact on message creation

7. Implementation Order
   Step 1: Database migrations
   Step 2: Email service (isolated)
   Step 3: Background job
   Step 4: Integration with messages
   Step 5: Tests
   Step 6: Configuration and deployment

Estimated complexity: Medium
Estimated time: 4-6 hours for basic implementation
```

---

**Example 2: Refactoring**
```
Use the Plan agent to plan refactoring the database queries from callbacks to async/await
```

---

**Example 3: Performance Optimization**
```
The app is slow when loading the dashboard with lots of data.

Use the Plan agent to create an optimization strategy.
```

---

## Lesson 4: General-Purpose Agent

### What is the General-Purpose Agent?

**Purpose:** Handle complex, multi-step tasks that don't fit specific categories

**Best for:**
- Research and implementation combined
- Tasks requiring web search
- Complex debugging
- Comprehensive updates

---

### General-Purpose Agent Examples

**Example 1: Research and Implement**
```
Use an agent to:
1. Research current best practices for rate limiting APIs
2. Implement rate limiting on our API endpoints
3. Add tests for the rate limiting
4. Document how it works
```

**What the agent does:**
- Searches web for best practices
- Reads your current code
- Implements rate limiting
- Creates tests
- Writes documentation
- All autonomously!

---

**Example 2: Find and Fix Issues**
```
Use an agent to:
- Find all potential security vulnerabilities in the authentication system
- Fix each issue found
- Add tests to prevent regression
- Document the changes
```

---

**Example 3: Update Dependencies**
```
Use an agent to:
1. Check which dependencies are outdated
2. Research breaking changes for major updates
3. Update dependencies safely
4. Fix any code that breaks
5. Run tests to verify everything works
```

---

## Lesson 5: Running Agents in Parallel

### Why Use Parallel Agents?

**Speed:** Multiple tasks complete simultaneously
**Efficiency:** Maximize use of time
**Independence:** Tasks don't depend on each other

---

### How to Run Agents in Parallel

**Request parallel execution:**
```
Please run these tasks in parallel using agents:

Agent 1: Explore the authentication system
Agent 2: Explore the payment processing
Agent 3: Create a list of all API endpoints
```

**Or:**
```
I need to understand three parts of this codebase simultaneously.
Use parallel agents to:
- Explore how data validation works
- Explore how errors are handled
- Explore how logging is implemented
```

---

### Practical Parallel Use Cases

**Example: Multiple features**
```
Run in parallel:
1. Agent to plan implementing user roles
2. Agent to plan implementing email notifications
3. Agent to plan implementing audit logging
```

**Example: Research**
```
Research in parallel:
1. Best practices for REST API design
2. Best practices for database indexing
3. Best practices for caching strategies

Then summarize findings
```

---

## Lesson 6: Working with Agent Results

### Understanding Agent Output

**Agents return:**
- Comprehensive reports
- Detailed explanations
- File locations and code snippets
- Recommendations
- Warnings about potential issues

---

### Acting on Agent Plans

**After agent creates a plan:**

**Option 1: Implement the plan**
```
That plan looks good. Let's implement step 1: database migrations
```

**Option 2: Modify the plan**
```
The plan looks good, but instead of using a background job,
let's send emails synchronously for now. Update the plan.
```

**Option 3: Ask questions**
```
I don't understand step 3. Can you explain in more detail?
```

---

### Using Explore Results

**After agent explores code:**

**Make informed changes:**
```
Now that you've explained how auth works,
add two-factor authentication following the same patterns
```

**Ask follow-up questions:**
```
You mentioned the auth tokens expire after 24 hours.
Where is that configured?
```

---

## Lesson 7: Agent Best Practices

### Be Specific About What You Want

❌ **Vague:**
```
Explore the codebase
```

✅ **Specific:**
```
Explore the codebase to find and explain all database queries,
focusing on performance and potential N+1 query problems
```

---

### Set Clear Goals

❌ **Unclear:**
```
Plan some improvements
```

✅ **Clear:**
```
Create a plan to add caching to the API to reduce database load,
targeting the 5 most frequently called endpoints
```

---

### Specify Constraints

**Include limitations:**
```
Plan implementing real-time notifications, but:
- Cannot use WebSockets (firewall restrictions)
- Must work with current database (SQLite)
- Should be simple to deploy
```

---

### Ask for Different Perspectives

```
Use the Plan agent to create 3 different approaches for adding search:
1. Simple SQL LIKE queries
2. Full-text search with database
3. External search service (like Elasticsearch)

For each, list pros, cons, and complexity
```

---

## Hands-On Practice

### Exercise 1: Explore a Codebase

**Task:** Use Explore agent to understand a project

**Find an open source project (or use one of yours) and:**

```
Use the Explore agent to:
1. Explain what this project does
2. Identify the main components
3. Show me the data flow
4. List potential areas for improvement
```

**Review the results and ask follow-up questions:**
```
You mentioned [component]. Can you show me where it's defined?
```

---

### Exercise 2: Plan a Feature

**Task:** Use Plan agent to design an implementation

**In a project:**

```
I want to add user profile pictures.

Use the Plan agent to create an implementation plan for:
- Uploading images
- Storing images
- Serving images
- Updating user profiles
- Image validation and security

Consider:
- File size limits
- Image formats allowed
- Where to store (local vs cloud)
- Performance implications
```

**Review the plan and refine:**
```
The plan suggests local storage, but I prefer cloud storage.
Update the plan to use AWS S3.
```

---

### Exercise 3: Parallel Research

**Task:** Research multiple topics simultaneously

```
I'm deciding how to implement search functionality.

Use parallel agents to research:
1. PostgreSQL full-text search capabilities and setup
2. Elasticsearch integration with Node.js
3. Simple LIKE query performance at scale

For each, provide:
- Setup complexity
- Performance characteristics
- Maintenance requirements
- Costs
```

---

### Exercise 4: Complex Autonomous Task

**Task:** Let an agent complete a complex task

```
Use an agent to:
1. Find all console.log statements in the codebase
2. Replace them with a proper logging library (Winston)
3. Set up log levels (error, warn, info, debug)
4. Configure log output to file and console
5. Update all existing logs to use appropriate levels
6. Test that logging works
```

**This would take you hours manually, but the agent can do it autonomously!**

---

## Module 6 Checklist

Before moving to Module 7, make sure you understand:

- [ ] What agents are and when to use them
- [ ] How to use the Explore agent to navigate codebases
- [ ] How to use the Plan agent to design implementations
- [ ] When to use general-purpose agents
- [ ] How to run agents in parallel
- [ ] How to interpret and act on agent results
- [ ] Best practices for working with agents

---

## Common Questions (FAQ)

### Q: How long do agents take?
**A:** Depends on task complexity. Simple exploration: 30 seconds. Complex planning: 1-2 minutes.

### Q: Can I stop an agent mid-task?
**A:** Yes! Press Ctrl+C or use the /tasks command to manage running agents.

### Q: Do agents make changes to my code?
**A:** Only if you ask them to implement. Explore and Plan agents only analyze and suggest.

### Q: Can agents make mistakes?
**A:** Yes, like any AI. Always review agent output before acting on it.

### Q: Should I use agents for simple tasks?
**A:** No. Agents add overhead. Use regular conversation for simple, quick tasks.

### Q: Can multiple agents work on the same files?
**A:** Be careful with this. If agents modify the same files, conflicts can occur.

---

## Agent Comparison Table

| Agent Type | Best For | Speed | Autonomy |
|------------|----------|-------|----------|
| **Explore** | Understanding code | Fast | High |
| **Plan** | Designing implementations | Medium | High |
| **General** | Complex multi-step tasks | Varies | Very High |
| **Regular Chat** | Simple tasks, learning | Fastest | Low |

---

## What's Next?

Great work! You now understand how to:
- Use specialized agents for complex tasks
- Explore codebases efficiently
- Plan implementations before coding
- Run multiple agents in parallel
- Work with agent results effectively

**Ready for Module 7?** In the next module, we'll master Git operations and version control with Claude Code's help!

---

## Pro Tips

1. **Use Explore before modifying** - Understand the code first

2. **Use Plan for complex features** - Think before coding

3. **Be specific** - Clear goals = better results

4. **Review agent output** - Don't blindly trust, verify

5. **Parallel for independent tasks** - Save time when tasks don't depend on each other

6. **Ask follow-up questions** - Agents can clarify their findings

7. **Iterate on plans** - Refine until you're confident

---

*Module 6 Complete!*
