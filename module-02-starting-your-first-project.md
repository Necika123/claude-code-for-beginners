# Module 2: Starting Your First Project

**Goal:** Learn all the different ways to begin building with Claude Code

**Estimated Time:** 30-40 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Know how to start a project from scratch with prompts
- Understand how to work with existing codebases
- Learn how to use templates and scaffolding
- Know how to clone and understand repositories
- Be able to choose the best method for your needs

---

## Lesson 1: Starting from Scratch (The Most Common Way)

### What Does "From Scratch" Mean?

**From scratch** means starting with an empty directory and letting Claude Code help you build everything from the ground up.

### When to Start from Scratch

- **New projects:** You're building something brand new
- **Learning:** You want to understand how everything is built
- **Custom requirements:** You need something very specific
- **Prototyping:** Testing an idea quickly

### How to Start from Scratch

#### Step 1: Create Your Project Directory

Always start by creating a dedicated folder for your project:

```bash
mkdir my-awesome-project
cd my-awesome-project
```

**Why?** Keeps your code organized and isolated.

#### Step 2: Start Claude Code

```bash
claude
```

You're now ready to build!

#### Step 3: Describe What You Want to Build

Be as specific or as general as you like:

**Simple Approach:**
```
Create a simple todo list web app
```

**More Detailed Approach:**
```
Create a todo list web application with:
- React frontend
- Express backend with REST API
- SQLite database
- Features: add, complete, delete tasks
- Clean, modern UI
```

**Very Detailed Approach:**
```
Build a full-stack todo application with these specifications:

Frontend:
- React with TypeScript
- Tailwind CSS for styling
- React hooks for state management
- Responsive design

Backend:
- Node.js with Express
- RESTful API endpoints
- SQLite database with better-sqlite3
- Input validation

Features:
- Create tasks with title and description
- Mark tasks as complete
- Delete tasks
- Filter by status (all/active/completed)
- Task due dates

Please start with the project structure and package.json
```

**Beginner Tip:** Start simple! You can always add more features later.

#### Step 4: Let Claude Code Build

After you send your request, Claude Code will:
1. **Ask clarifying questions** (if needed)
2. **Create the project structure**
3. **Set up configuration files** (package.json, etc.)
4. **Write initial code**
5. **Explain what it created**

Watch as it uses different tools:
- **Write** - Creating new files
- **Bash** - Running commands like `npm init`
- **Read** - Checking what it created

#### Step 5: Review the Structure

Once Claude Code finishes, ask:

```
Can you show me the project structure?
```

You'll see something like:
```
my-awesome-project/
├── package.json
├── src/
│   ├── index.js
│   ├── app.js
│   └── routes/
│       └── todos.js
├── public/
│   └── index.html
└── README.md
```

#### Step 6: Test It

```
Can you run the application?
```

Claude Code will:
- Install dependencies (`npm install`)
- Start the server
- Show you how to access it

---

## Lesson 2: Working with Existing Codebases

### What is an Existing Codebase?

An **existing codebase** is a project that someone else built (or you built earlier) that you want to modify or understand.

### When to Work with Existing Code

- **Contributing to open source**
- **Joining a team project**
- **Maintaining legacy code**
- **Learning from examples**
- **Debugging someone else's code**

### How to Work with Existing Code

#### Step 1: Navigate to the Project

```bash
cd /path/to/existing-project
```

#### Step 2: Start Claude Code

```bash
claude
```

#### Step 3: Understand the Codebase

Start by asking Claude Code to explore:

```
Can you help me understand what this project does? Please explore the codebase and give me an overview.
```

Claude Code will:
- Use the **Task tool** with the **Explore agent**
- Read key files (README, package.json, main files)
- Analyze the structure
- Provide a summary

**You'll get:**
- What the project does
- Technology stack
- Main components
- Entry points
- Dependencies

#### Step 4: Find Specific Code

Need to find something? Ask:

```
Where is the user authentication logic?
```

Or:

```
Find all files that handle database operations
```

Claude Code will use **Grep** and **Glob** to search your codebase.

#### Step 5: Make Changes

Once you understand the code, make modifications:

```
Add a new endpoint to the API that returns user statistics
```

Claude Code will:
- Find the right file
- Add the code in the correct place
- Follow existing patterns
- Explain what it did

#### Step 6: Test Your Changes

```
Run the tests to make sure I didn't break anything
```

---

## Lesson 3: Using Templates and Scaffolding

### What are Templates?

**Templates** are pre-built project structures that give you a head start. Think of them as blueprints.

### Common Templates

- **create-react-app** - React applications
- **express-generator** - Express servers
- **vite** - Modern frontend projects
- **nest-cli** - NestJS applications
- **create-next-app** - Next.js projects

### How to Use Templates

#### Method 1: Ask Claude Code to Use a Template

```
Create a new React app using create-react-app
```

Claude Code will:
```bash
npx create-react-app my-app
```

Then help you customize it!

#### Method 2: Ask for a Custom Template

```
Set up a basic Express server with TypeScript, organized with:
- Controllers folder
- Routes folder
- Middleware folder
- Models folder
- Config folder
```

Claude Code will create the structure from scratch.

#### Method 3: Use Framework CLIs

```
Initialize a new Next.js project with TypeScript and Tailwind CSS
```

Claude Code will run:
```bash
npx create-next-app@latest --typescript --tailwind
```

### Customizing Templates

After scaffolding, customize:

```
Add authentication using JWT
Add a database connection using Prisma
Set up ESLint and Prettier
Add a Docker configuration
```

---

## Lesson 4: Cloning and Understanding Repositories

### What is Cloning?

**Cloning** means downloading a copy of a Git repository from GitHub, GitLab, or other platforms.

### When to Clone

- **Open source contribution**
- **Learning from examples**
- **Using starter templates**
- **Following tutorials**

### How to Clone with Claude Code

#### Step 1: Find a Repository

Let's say you want to clone: `https://github.com/user/awesome-project`

#### Step 2: Clone It

You can either clone manually:

```bash
git clone https://github.com/user/awesome-project
cd awesome-project
claude
```

Or ask Claude Code to do it:

```bash
claude
```

Then:
```
Clone the repository https://github.com/user/awesome-project and help me set it up
```

Claude Code will:
- Run `git clone`
- Read the README
- Install dependencies
- Explain how to run it

#### Step 3: Understand the Project

```
Please explore this codebase and explain:
1. What does this project do?
2. What technologies does it use?
3. How is it structured?
4. How do I run it locally?
```

#### Step 4: Set Up the Environment

```
Help me set up this project. Install dependencies and configure any necessary environment variables.
```

Claude Code will:
- Check for package.json, requirements.txt, etc.
- Install dependencies
- Look for .env.example
- Guide you through configuration

#### Step 5: Make Your First Contribution

```
I want to add a feature that [describe feature]. Where should I start?
```

Claude Code will:
- Analyze the codebase
- Suggest the right files to modify
- Help you implement the feature
- Guide you through testing

---

## Lesson 5: Choosing the Best Approach

### Decision Matrix

Here's how to choose:

| Scenario | Best Approach | Why |
|----------|---------------|-----|
| Brand new project | **From scratch** | Full control, learn everything |
| Following a tutorial | **Clone & modify** | Start with working code |
| React/Next.js app | **Use template CLI** | Industry standard setup |
| Contributing to OSS | **Clone repository** | Work with existing code |
| Learning a framework | **From scratch** | Understand fundamentals |
| Quick prototype | **Template + customize** | Fast start, then iterate |
| Joining team project | **Clone repository** | Get existing codebase |

### Tips for Choosing

**Start from scratch when:**
- You want to learn deeply
- You have unique requirements
- You're building something custom
- You're following specific architecture

**Use templates when:**
- You want to move fast
- You're using popular frameworks
- You need standard configuration
- You're prototyping

**Clone repositories when:**
- Contributing to projects
- Learning from examples
- Following tutorials
- Using starter templates

---

## Hands-On Practice: Try Each Method

### Practice 1: From Scratch - Build a Simple CLI Tool

**Task:** Create a command-line weather app

**Your prompt:**
```
Create a Node.js CLI tool that:
- Takes a city name as argument
- Fetches weather data from a free API
- Displays temperature and conditions
- Use the wttr.in API (no key needed)

Example usage: node weather.js "New York"
```

**Steps:**
1. Create directory: `mkdir weather-cli && cd weather-cli`
2. Start Claude Code: `claude`
3. Send the prompt above
4. Test the application
5. Ask for improvements (add colors, better formatting)

---

### Practice 2: Template - Create a React App

**Task:** Set up a React app with routing

**Your prompt:**
```
Create a new React application with:
- React Router for navigation
- Three pages: Home, About, Contact
- A navigation bar
- Tailwind CSS for styling

Use Vite as the build tool
```

**Steps:**
1. Create directory: `mkdir my-react-app && cd my-react-app`
2. Start Claude Code: `claude`
3. Send the prompt above
4. Explore the generated structure
5. Run the dev server
6. Make a small change (add a new page)

---

### Practice 3: Clone - Work with an Open Source Project

**Task:** Clone and understand a popular repository

**Your prompt:**
```
Clone the repository https://github.com/simple-icons/simple-icons
Then help me:
1. Understand what this project does
2. Set up my development environment
3. Find where the icon data is stored
4. Explain how I could contribute a new icon
```

**Steps:**
1. Start in your projects folder
2. Start Claude Code: `claude`
3. Send the prompt above
4. Follow Claude Code's guidance
5. Ask questions about the codebase

---

### Practice 4: Existing Code - Modify a Past Project

**Task:** Improve a project you built earlier

**Your prompt:**
```
Help me add error handling to this project.
Please:
1. Find all places that need error handling
2. Add try-catch blocks where appropriate
3. Create meaningful error messages
4. Add logging for errors
```

**Steps:**
1. Navigate to an old project
2. Start Claude Code: `claude`
3. Send the prompt above
4. Review the changes
5. Test error scenarios

---

## Module 2 Challenges

### Challenge 1: From Scratch - Build a Note-Taking API (Beginner)

**Your Task:** Create a REST API for notes

**Requirements:**
- Express.js server
- In-memory storage (no database yet)
- Endpoints: GET, POST, PUT, DELETE
- Each note has: id, title, content, createdAt
- Include input validation

**Hints:**
- Start with basic structure
- Add one endpoint at a time
- Test as you build

**Check your solution:** See [Challenge Solutions](supplement-challenge-solutions.md#module-2-challenge-1)

---

### Challenge 2: Template - Full-Stack App (Intermediate)

**Your Task:** Create a full-stack application using templates

**Requirements:**
- Next.js for frontend
- API routes for backend
- A simple contact form
- Form validation
- Success/error messages
- Responsive design

**Hints:**
- Use create-next-app
- Start with the form UI
- Then add API endpoint
- Finally add validation

**Check your solution:** See [Challenge Solutions](supplement-challenge-solutions.md#module-2-challenge-2)

---

### Challenge 3: Clone & Contribute - Real World (Advanced)

**Your Task:**
1. Find an open source project with "good first issue" tags
2. Clone it
3. Set it up locally
4. Understand the codebase
5. Implement the issue
6. Test your changes

**Requirements:**
- Must be a real GitHub repository
- Must successfully run locally
- Your change must work
- Follow the project's contribution guidelines

**Hints:**
- Check CONTRIBUTING.md first
- Read existing code for patterns
- Test thoroughly
- Ask Claude Code for guidance

**Check your solution:** See [Challenge Solutions](supplement-challenge-solutions.md#module-2-challenge-3)

---

## Module 2 Checklist

Before moving to Module 3, make sure you can:

- [ ] Create a project from scratch with Claude Code
- [ ] Work with existing codebases
- [ ] Use templates and CLIs effectively
- [ ] Clone and set up repositories
- [ ] Choose the right approach for different scenarios
- [ ] Navigate and understand unfamiliar code
- [ ] Make modifications to existing projects

---

## Common Questions (FAQ)

### Q: Should I always start from scratch?
**A:** No! Use templates for common project types. Start from scratch when learning or building something unique.

### Q: How do I know which template to use?
**A:** Ask Claude Code! "What's the best way to start a [type of project]?"

### Q: What if I don't understand the cloned code?
**A:** Ask Claude Code to explain it! That's one of its best features.

### Q: Can Claude Code help with non-JavaScript projects?
**A:** Yes! It works with Python, Go, Rust, Java, and many other languages.

### Q: How detailed should my initial prompt be?
**A:** Start with the basics, then add details iteratively. You can always refine.

---

## What's Next?

Excellent work! You now know how to:
- Start projects from scratch
- Work with existing code
- Use templates effectively
- Clone and understand repositories
- Choose the best approach

**Ready for Module 3?** In the next module, we'll dive deep into Claude Code's tools - understanding what each tool does and when to use it!

---

## Pro Tips for Beginners

1. **Start simple, iterate** - Build the basic version first, then add features

2. **Use templates for common patterns** - Don't reinvent the wheel

3. **Read before modifying** - Understand existing code before changing it

4. **Ask for explanations** - Claude Code can teach you as it builds

5. **Check the docs** - Always read README files in cloned repos

6. **Version control** - Use Git from the start (we'll cover this in Module 7)

7. **Test frequently** - Run your code often to catch issues early

---

*Module 2 Complete!*
