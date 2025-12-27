# Troubleshooting Guide

**Common issues and how to resolve them**

---

## Installation Issues

### Problem: "command not found: claude"

**Symptoms:**
```bash
$ claude
zsh: command not found: claude
```

**Causes:**
- Claude Code not installed globally
- Terminal not restarted after installation
- npm global bin path not in PATH

**Solutions:**

**Solution 1: Install globally**
```bash
npm install -g claude-code
```

**Solution 2: Restart your terminal**
Close and reopen your terminal application

**Solution 3: Check npm global path**
```bash
npm config get prefix
```

Add to your PATH in `.bashrc`, `.zshrc`, or similar:
```bash
export PATH="$PATH:$(npm config get prefix)/bin"
```

---

### Problem: "Permission denied" during installation

**Symptoms:**
```bash
npm install -g claude-code
# Error: EACCES: permission denied
```

**Solutions:**

**Solution 1: Use npx (recommended)**
```bash
npx claude-code
```

**Solution 2: Fix npm permissions**
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
```

Add the export line to your shell profile

**Solution 3: Use sudo (not recommended)**
```bash
sudo npm install -g claude-code
```

---

### Problem: Node.js version too old

**Symptoms:**
```
Error: Claude Code requires Node.js 18 or higher
```

**Solution:**

Update Node.js to version 18+:

**Using nvm (recommended):**
```bash
# Install nvm first if needed
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install latest Node.js
nvm install node
nvm use node
```

**Or download from nodejs.org:**
Visit [nodejs.org](https://nodejs.org) and download the LTS version

---

## API Key Issues

### Problem: "API key not found"

**Symptoms:**
```
Error: ANTHROPIC_API_KEY environment variable not set
```

**Solutions:**

**Solution 1: Set environment variable (current session)**
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

**Solution 2: Set in shell profile (persistent)**

Add to `~/.bashrc`, `~/.zshrc`, or `~/.bash_profile`:
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

Then reload:
```bash
source ~/.zshrc  # or ~/.bashrc
```

**Solution 3: Use Claude Code config**
```bash
claude config set apiKey "your-api-key-here"
```

---

### Problem: "Invalid API key"

**Symptoms:**
```
Error: Invalid API key
```

**Causes:**
- Typo in API key
- API key revoked or expired
- Wrong API key format

**Solutions:**

1. **Get a new API key:**
   - Go to [console.anthropic.com](https://console.anthropic.com)
   - Create a new API key
   - Copy the entire key (starts with `sk-ant-`)

2. **Check for typos:**
   - Keys should start with `sk-ant-`
   - No spaces before/after
   - No quote marks inside the key

3. **Verify it's set correctly:**
   ```bash
   echo $ANTHROPIC_API_KEY
   ```

---

### Problem: "Insufficient credits"

**Symptoms:**
```
Error: Insufficient credits in your account
```

**Solutions:**

1. **Check your balance:**
   - Visit [console.anthropic.com](https://console.anthropic.com)
   - Check "Usage" section

2. **Add credits:**
   - Add payment method
   - Purchase credits

3. **Wait for monthly reset:**
   - Free tier credits reset monthly
   - Check when your next reset is

---

## Runtime Issues

### Problem: Claude Code freezes or hangs

**Symptoms:**
- No response after sending prompt
- Cursor not blinking
- No output for minutes

**Solutions:**

**Solution 1: Check internet connection**
```bash
ping anthropic.com
```

**Solution 2: Increase timeout (if available)**
```bash
# In your request, specify longer timeout
claude --timeout 300
```

**Solution 3: Kill and restart**
Press `Ctrl+C` to stop, then start again

**Solution 4: Check for background processes**
```bash
# List background tasks
/tasks

# Kill if needed
```

---

### Problem: "Rate limit exceeded"

**Symptoms:**
```
Error: Rate limit exceeded. Please try again later.
```

**Causes:**
- Too many requests in short time
- API limits reached

**Solutions:**

1. **Wait and retry:**
   - Wait 60 seconds
   - Try again

2. **Reduce request frequency:**
   - Combine multiple small requests
   - Make larger, less frequent requests

3. **Check your usage:**
   - Visit console.anthropic.com
   - Review usage limits

---

### Problem: Changes not being saved

**Symptoms:**
- Files show as modified but aren't actually changed
- Code disappears after closing

**Solutions:**

**Solution 1: Check file permissions**
```bash
ls -la [filename]
```

If you don't have write permission:
```bash
chmod u+w [filename]
```

**Solution 2: Verify working directory**
```
Show me the current working directory
List all files here
```

**Solution 3: Explicitly save**
```
Please write the changes to [filename]
Show me [filename] to verify
```

---

### Problem: Tools not working

**Symptoms:**
- Read/Write/Edit tools fail
- Bash commands don't execute
- Error: "Tool execution failed"

**Solutions:**

**For file tools (Read/Write/Edit):**
1. **Check file paths:**
   - Use absolute paths: `/home/user/project/file.js`
   - Or ensure you're in the right directory

2. **Check permissions:**
   ```bash
   ls -la
   ```

3. **Check disk space:**
   ```bash
   df -h
   ```

**For Bash tool:**
1. **Check command syntax:**
   ```
   Please explain this command before running it
   ```

2. **Test command manually:**
   ```bash
   # Exit Claude Code and test
   [your command]
   ```

3. **Check for required programs:**
   ```bash
   which [program]
   ```

---

## Code Execution Issues

### Problem: "Module not found" errors

**Symptoms:**
```
Error: Cannot find module 'express'
```

**Solutions:**

**Solution 1: Install dependencies**
```
Install all dependencies from package.json
```

Or manually:
```bash
npm install
# or
pip install -r requirements.txt
```

**Solution 2: Check node_modules**
```bash
ls node_modules/
```

If empty or missing:
```bash
rm -rf node_modules package-lock.json
npm install
```

**Solution 3: Check import paths**
```
Check all import statements in [file]
Fix any incorrect paths
```

---

### Problem: Syntax errors after Claude Code changes

**Symptoms:**
```
SyntaxError: Unexpected token
```

**Solutions:**

**Solution 1: Review the changes**
```
Show me what you changed in [file]
```

**Solution 2: Revert changes**
```
Please undo the changes to [file]
```

Or with Git:
```bash
git checkout [file]
```

**Solution 3: Fix the syntax**
```
There's a syntax error in [file] at line [X]. Please fix it.
```

---

### Problem: Tests failing after changes

**Symptoms:**
- Tests passed before
- Tests fail after Claude Code modifications

**Solutions:**

**Solution 1: Check what changed**
```
Show me the git diff
What files did you modify?
```

**Solution 2: Review test failures**
```
Run the tests and show me the output
Explain why these tests are failing
```

**Solution 3: Fix the tests**
```
Fix the code to make the tests pass
```

Or:
```
Update the tests to match the new implementation
```

---

## Git Integration Issues

### Problem: Git commands failing

**Symptoms:**
```
Error: fatal: not a git repository
```

**Solutions:**

**Solution 1: Initialize Git**
```
Initialize a git repository in this directory
```

Or manually:
```bash
git init
```

**Solution 2: Check Git installation**
```bash
git --version
```

If not installed, install Git:
- **macOS:** `brew install git`
- **Ubuntu:** `sudo apt-get install git`
- **Windows:** Download from git-scm.com

**Solution 3: Verify you're in right directory**
```bash
pwd
ls -la .git
```

---

### Problem: Cannot commit changes

**Symptoms:**
```
Error: Please tell me who you are
```

**Solutions:**

**Configure Git identity:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Or ask Claude Code:
```
Configure git with my name and email
```

---

## Performance Issues

### Problem: Claude Code is slow

**Symptoms:**
- Long delays between request and response
- Tools take forever to execute

**Solutions:**

**Solution 1: Check internet speed**
```bash
speedtest-cli
# or visit fast.com
```

**Solution 2: Simplify requests**
- Break complex tasks into smaller ones
- Be more specific to reduce thinking time

**Solution 3: Use agents for complex tasks**
```
Use an agent to [complex task]
```
Agents can be more efficient for multi-step tasks

**Solution 4: Close other applications**
- Free up memory and CPU
- Close other Claude Code sessions

---

### Problem: Large file operations are slow

**Symptoms:**
- Reading large files takes forever
- Editing large files is slow

**Solutions:**

**Solution 1: Read specific sections**
```
Read lines 100-200 of [file]
Show me just the [function/class] in [file]
```

**Solution 2: Use search instead**
```
Use grep to find [pattern] in [file]
```

**Solution 3: Split large files**
```
Help me refactor this large file into smaller modules
```

---

## MCP Server Issues

### Problem: MCP server not connecting

**Symptoms:**
```
Error: Failed to connect to MCP server
```

**Solutions:**

**Solution 1: Check server is running**
```bash
# Check if server process is running
ps aux | grep mcp
```

**Solution 2: Verify configuration**
Check `~/.config/claude/config.json`:
```json
{
  "mcpServers": {
    "server-name": {
      "command": "path-to-server",
      "args": []
    }
  }
}
```

**Solution 3: Test server manually**
```bash
# Run the MCP server command manually
/path/to/mcp-server
```

**Solution 4: Check server logs**
Look in `~/.config/claude/logs/` for error messages

---

## Getting More Help

### When to ask Claude Code for help

You can ask Claude Code itself to help troubleshoot:

```
I'm getting this error: [error message]
Can you help me understand and fix it?
```

```
Something's not working correctly. Can you help me debug?
```

```
The [feature] isn't behaving as expected. Help me troubleshoot.
```

### When to check documentation

- [Claude Code GitHub](https://github.com/anthropics/claude-code)
- [Claude API Docs](https://docs.anthropic.com)
- [GitHub Issues](https://github.com/anthropics/claude-code/issues)

### When to ask the community

- Search existing GitHub issues
- Create new issue with:
  - Clear problem description
  - Steps to reproduce
  - Error messages
  - System information

### System information to provide

When reporting issues, include:

```bash
# Claude Code version
claude --version

# Node.js version
node --version

# npm version
npm --version

# Operating system
uname -a  # macOS/Linux
# or
systeminfo  # Windows
```

---

## Prevention Tips

### Best Practices to Avoid Issues

1. **Always use version control (Git)**
   - Commit working code before making changes
   - Easy to revert if something breaks

2. **Review changes before accepting**
   - Check Edit tool outputs
   - Verify Bash commands before they run

3. **Test incrementally**
   - Test after each change
   - Catch issues early

4. **Keep backups**
   - Commit to Git regularly
   - Push to remote repositories

5. **Be specific in requests**
   - Reduces misunderstandings
   - Gets better results

6. **Ask for explanations**
   - Understand what Claude Code is doing
   - Learn to spot issues

7. **Start simple, add complexity**
   - Get basics working first
   - Add features incrementally

---

*Most issues can be solved with clear communication and systematic troubleshooting!*
