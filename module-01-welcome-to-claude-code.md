# Module 1: Welcome to Claude Code - Your First Steps

**Goal:** Get comfortable with Claude Code and understand what it can do

**Estimated Time:** 20-30 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand what "AI Pair Programming" is and why it's revolutionary
- Know how to install Claude Code on your system
- Be familiar with the command-line interface
- Understand the basic conversation flow
- Know the essential terminology you need

---

## Lesson 1: What is "AI Pair Programming"?

### Understanding the Concept

**AI Pair Programming** is a revolutionary approach to software development. Let's break this down in the simplest way possible:

**Traditional Programming (The Old Way):**
- You write every line of code yourself
- You search documentation for hours
- You manually debug errors
- You need to remember syntax and APIs
- Small mistakes can take hours to find

**AI Pair Programming (The Claude Code Way):**
- You describe what you want to accomplish
- AI helps you implement it step-by-step
- AI can read your code, understand context, and make changes
- AI explains what it's doing so you learn
- Debugging is collaborative and faster

### Real-World Example

**Instead of doing this manually:**
```bash
# Search Google for "how to create HTTP server in Node.js"
# Read documentation
# Copy-paste examples
# Debug why it's not working
# Fix syntax errors
# Test manually
```

**You simply say:**
> "Create a simple HTTP server in Node.js that returns 'Hello World' on port 3000"

And Claude Code:
1. Creates the file
2. Writes the code
3. Explains what it did
4. Can even run it for you!

That's the power of AI Pair Programming.

---

## Lesson 2: Installing Claude Code

### System Requirements

Before installing, make sure you have:
- A computer running macOS, Linux, or Windows (WSL)
- Internet connection
- Terminal/command-line access
- A Claude API key (we'll get this)

**Beginner Tip:** If you're on Windows, you'll need WSL (Windows Subsystem for Linux). Don't worry - we'll guide you!

### Step-by-Step Installation

#### Step 1: Install Node.js (if you don't have it)

Claude Code requires Node.js version 18 or higher.

**Check if you have Node.js:**
```bash
node --version
```

**If you see a version number like `v18.x.x` or higher, you're good!**

**If not, install Node.js:**
1. Go to [nodejs.org](https://nodejs.org)
2. Download the LTS (Long Term Support) version
3. Run the installer
4. Follow the installation prompts

#### Step 2: Get Your Claude API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up or log in
3. Navigate to "API Keys"
4. Click "Create Key"
5. Copy your API key (starts with `sk-ant-...`)
6. **Keep this safe!** Don't share it with anyone

**Beginner Tip:** Your API key is like a password - keep it secret and secure!

#### Step 3: Install Claude Code

Open your terminal and run:

```bash
npm install -g claude-code
```

**What's happening:**
- `npm` is the Node Package Manager (it installs software)
- `install` tells npm to install something
- `-g` means "globally" (available everywhere)
- `claude-code` is the package name

**Wait for installation to complete.** You'll see a progress indicator.

#### Step 4: Set Up Your API Key

You need to tell Claude Code your API key. There are two ways:

**Option A: Set it as an environment variable (recommended)**

**On macOS/Linux:**
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

**On Windows (PowerShell):**
```powershell
$env:ANTHROPIC_API_KEY="your-api-key-here"
```

To make it permanent, add it to your shell configuration file (`.bashrc`, `.zshrc`, etc.)

**Option B: Create a config file**

Claude Code can also read from a config file:
```bash
claude config set apiKey "your-api-key-here"
```

#### Step 5: Verify Installation

Run this command to make sure everything works:

```bash
claude --version
```

You should see the Claude Code version number!

**Beginner Tip:** If you get an error, make sure you restarted your terminal after installation.

---

## Lesson 3: Understanding the Claude Code Interface

### What is a CLI (Command Line Interface)?

A **CLI** is a text-based way to interact with software. Instead of clicking buttons, you type commands.

**Don't be intimidated!** Claude Code makes the CLI friendly and conversational.

### Your First Look at Claude Code

#### Starting Claude Code

In your terminal, simply type:

```bash
claude
```

**What you'll see:**
```
╭───────────────────────────────────────────────────╮
│                                                   │
│   Claude Code v1.0.0                             │
│   AI-powered development assistant               │
│                                                   │
╰───────────────────────────────────────────────────╯

Working directory: /home/user/projects

How can I help you today?
>
```

**This is your conversation interface!** The `>` is where you type.

### Understanding the Interface

#### The Header
Shows:
- Claude Code version
- Your current working directory
- Status information

#### The Prompt (`>`)
This is where you type your requests, just like chatting with a friend.

#### Response Area
Above the prompt, you'll see:
- Claude's responses
- Tool usage (when Claude reads files, runs commands, etc.)
- Results and output

### Your First Conversation

Let's try something simple. At the `>` prompt, type:

```
Hello! Can you explain what you can do?
```

Press Enter and watch Claude Code respond!

**You'll see:**
- A friendly greeting
- An explanation of capabilities
- Suggestions for what to try

**Beginner Tip:** Claude Code is conversational. You can ask questions in plain English!

---

## Lesson 4: Basic Terminology You Need to Know

Let's learn the essential words you'll see in Claude Code. Don't worry - we'll explain everything in simple terms!

### Essential Terms

**Session**
- **What it means:** One conversation with Claude Code, from start to end
- **Think of it like:** A chat conversation that ends when you close the terminal
- **Example:** You start Claude Code, ask it to help build a website, then exit

**Working Directory**
- **What it means:** The folder Claude Code is currently working in
- **Think of it like:** Your current location on your computer
- **Example:** `/home/user/my-project` is where your project files are

**Tool**
- **What it means:** A capability Claude Code has (like reading files, running commands)
- **Think of it like:** Different skills or abilities
- **Example:** The "Read" tool lets Claude read your code files

**Prompt**
- **What it means:** Your message or request to Claude Code
- **Think of it like:** An instruction or question you ask
- **Example:** "Create a Python script that prints Hello World"

**Tool Use / Tool Call**
- **What it means:** When Claude Code uses one of its tools to do something
- **Think of it like:** Claude performing an action
- **Example:** Using the Write tool to create a new file

**Agent**
- **What it means:** A specialized AI helper for complex tasks
- **Think of it like:** Calling in an expert for a specific job
- **Example:** The "Explore" agent helps you understand large codebases

**Context**
- **What it means:** The information Claude Code has about your project
- **Think of it like:** What Claude "knows" about your code
- **Example:** Files it has read, commands it has run

**MCP Server**
- **What it means:** An extension that gives Claude Code new capabilities
- **Think of it like:** A plugin or add-on
- **Example:** A database MCP server lets Claude Code work with databases

**Beginner Tip:** Don't try to memorize all of these right now! You'll learn them naturally as you use Claude Code. Just refer back to this list if you see a word you don't understand.

---

## Hands-On Practice: Your First Claude Code Session

Now let's actually build something! This will be very simple - we're just getting you comfortable with the process.

### Practice Project: A Simple Python Script

#### Step 1: Create a Project Directory

First, let's create a folder for your project. In your terminal (before starting Claude Code):

```bash
mkdir hello-claude
cd hello-claude
```

**What you did:**
- `mkdir` = make directory (create a folder)
- `cd` = change directory (go into the folder)

#### Step 2: Start Claude Code

Now start Claude Code in this directory:

```bash
claude
```

You're now in a Claude Code session!

#### Step 3: Your First Request

At the `>` prompt, type:

```
Create a Python script called hello.py that asks for the user's name and greets them
```

Press Enter.

**What you'll see:**
- Claude Code acknowledging your request
- It using the Write tool to create the file
- The code being written
- Confirmation that it's done

#### Step 4: Check What Was Created

Let's see the file. Type:

```
Can you show me what's in hello.py?
```

Claude Code will use the Read tool and display the contents!

#### Step 5: Run the Program

Now let's run it! Type:

```
Run the hello.py script
```

Claude Code will:
- Use the Bash tool to run `python hello.py`
- The script will ask for your name
- Type your name and press Enter
- See the greeting!

#### Step 6: Make a Change

Let's practice making changes. Type:

```
Make the greeting more enthusiastic with exclamation marks
```

Watch as Claude Code:
- Uses the Edit tool
- Shows you the change
- Updates the file

**Congratulations!** You just:
- Created a file with AI
- Ran a program
- Made modifications
- All through conversation!

---

## Understanding What Just Happened

Let's break down what Claude Code did:

### When you asked to create a script:
1. **Understood your request** - Parsed what you wanted
2. **Chose the right tool** - Decided to use Write
3. **Created the file** - Wrote the Python code
4. **Confirmed completion** - Let you know it was done

### When you asked to see the file:
1. **Used the Read tool** - Opened and read the file
2. **Displayed contents** - Showed you the code
3. **Explained what it does** - Helped you understand

### When you asked to run it:
1. **Used the Bash tool** - Ran the command
2. **Showed output** - Displayed the results
3. **Handled interaction** - Let you type your name

### When you asked for changes:
1. **Used the Edit tool** - Made precise modifications
2. **Showed the diff** - Highlighted what changed
3. **Preserved other code** - Only changed what was needed

This is the basic workflow you'll use for all Claude Code tasks!

---

## Module 1 Checklist

Before moving to Module 2, make sure you can:

- [ ] Explain what "AI Pair Programming" is in your own words
- [ ] Successfully install Claude Code on your system
- [ ] Start a Claude Code session in your terminal
- [ ] Understand basic terms like "tool," "prompt," and "session"
- [ ] Create a simple file using Claude Code
- [ ] Make changes to a file
- [ ] Run a program with Claude Code's help

---

## Common Questions (FAQ)

### Q: Do I need to know how to code?
**A:** No! Claude Code can help you learn programming. However, some basic understanding helps you guide Claude Code better.

### Q: Is Claude Code free?
**A:** Claude Code itself is free, but you need a Claude API key which has usage costs. New users typically get free credits to start.

### Q: What if I make a mistake in my request?
**A:** No problem! You can clarify, ask Claude Code to undo changes, or simply make a new request. Nothing is permanent.

### Q: Can Claude Code work with any programming language?
**A:** Yes! Claude Code can help with Python, JavaScript, Java, Go, Rust, and many more languages.

### Q: What if Claude Code does something wrong?
**A:** You're always in control. Review changes before accepting them, and you can always ask Claude Code to fix or revert things.

### Q: How do I exit Claude Code?
**A:** Type `/exit` or press Ctrl+C. Your files are saved automatically.

---

## What's Next?

Great job completing Module 1! You now understand:
- What Claude Code is and how it works
- How to install and set it up
- How to start a session and have a conversation
- How to create and modify files

**Ready for Module 2?** In the next module, we'll learn different ways to start projects with Claude Code - from scratch, from templates, and from existing codebases!

---

## Pro Tips for Beginners

1. **Be conversational** - Talk to Claude Code naturally, like a colleague

2. **Be specific** - The more details you provide, the better the results

3. **Ask questions** - If you don't understand something, ask Claude Code to explain

4. **Review changes** - Always check what Claude Code does so you learn

5. **Experiment** - Try different requests and see what happens. You can't break anything!

6. **Save your work** - Use Git (we'll learn this later) to track changes

7. **Read the output** - Claude Code explains what it's doing - this helps you learn

---

## Troubleshooting Common Issues

### "Command not found: claude"
**Solution:** Make sure you installed globally with `-g` and restarted your terminal.

### "API key not found"
**Solution:** Set your `ANTHROPIC_API_KEY` environment variable or use `claude config set apiKey`.

### "Permission denied"
**Solution:** You might need to use `sudo` on macOS/Linux: `sudo npm install -g claude-code`

### Claude Code seems slow
**Solution:** This is normal. AI processing takes time. Complex requests take longer than simple ones.

### I don't see any output
**Solution:** Make sure you pressed Enter after typing your request. Check your internet connection.

---

*Module 1 Complete!*
