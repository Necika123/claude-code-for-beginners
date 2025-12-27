# Module 12: Skills and Hooks - Customizing Claude Code

**Goal:** Customize Claude Code's behavior with skills and hooks

**Estimated Time:** 30-40 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand what skills and hooks are
- Create custom slash commands (skills)
- Set up hooks for automation
- Customize Claude Code settings
- Integrate with your IDE
- Create custom workflows

---

## Lesson 1: Understanding Skills

### What are Skills?

**Skills** are custom slash commands you can create to automate common tasks.

**Example built-in skills:**
- `/commit` - Create a git commit
- `/review-pr` - Review a pull request
- `/help` - Show help information

**You can create your own:**
- `/deploy` - Deploy your application
- `/test-all` - Run all tests and show results
- `/review-code` - Review code with your team's standards

---

### Creating Your First Skill

**Skills are defined in:**
```
~/.config/claude/skills/
```

**Create a simple skill:**

```typescript
// ~/.config/claude/skills/hello.ts
export default {
  name: 'hello',
  description: 'Say hello',
  run: async (context) => {
    return 'Hello from my custom skill!';
  }
};
```

**Use it:**
```
/hello
```

---

### Practical Skill Examples

**Example 1: Deploy Skill**

```typescript
// ~/.config/claude/skills/deploy.ts
export default {
  name: 'deploy',
  description: 'Deploy application to production',
  run: async (context) => {
    // Run deployment script
    await context.bash('npm run build');
    await context.bash('./scripts/deploy.sh');

    return 'Deployment complete!';
  }
};
```

---

**Example 2: Code Review Skill**

```typescript
// ~/.config/claude/skills/review.ts
export default {
  name: 'review',
  description: 'Review code against team standards',
  run: async (context) => {
    // Get current git diff
    const diff = await context.bash('git diff');

    // Review against standards
    const review = await context.agent({
      type: 'general',
      prompt: `Review this code against our standards:\n${diff}\n\nCheck for:
      - Security issues
      - Performance problems
      - Code style violations
      - Missing tests`
    });

    return review;
  }
};
```

---

## Lesson 2: Understanding Hooks

### What are Hooks?

**Hooks** are scripts that run automatically when certain events happen.

**Available hooks:**
- `user-prompt-submit-hook` - Before sending your message
- `tool-use-hook` - Before using a tool
- `response-hook` - After Claude responds

---

### Creating Hooks

**Hooks are defined in config.json:**

```json
{
  "hooks": {
    "user-prompt-submit-hook": "~/.config/claude/hooks/before-prompt.sh",
    "tool-use-hook": "~/.config/claude/hooks/before-tool.sh"
  }
}
```

---

### Practical Hook Examples

**Example 1: Auto-format Before Commit**

```bash
#!/bin/bash
# ~/.config/claude/hooks/before-tool.sh

# If the tool is Edit or Write, format the file
if [ "$TOOL_NAME" = "Edit" ] || [ "$TOOL_NAME" = "Write" ]; then
  # Run prettier on JavaScript files
  if [[ "$FILE_PATH" == *.js ]] || [[ "$FILE_PATH" == *.ts ]]; then
    npx prettier --write "$FILE_PATH"
  fi
fi
```

---

**Example 2: Security Check Hook**

```bash
#!/bin/bash
# ~/.config/claude/hooks/security-check.sh

# Check for sensitive data before committing
if [[ "$PROMPT" == *"commit"* ]]; then
  # Check for API keys, passwords, etc.
  if git diff | grep -i "api_key\|password\|secret"; then
    echo "WARNING: Potential sensitive data found!"
    exit 1  # Block the action
  fi
fi
```

---

## Lesson 3: Customizing Settings

### Claude Code Configuration

**Main config file:**
```
~/.config/claude/config.json
```

**Example configuration:**

```json
{
  "apiKey": "your-api-key",
  "model": "claude-sonnet-4.5-20250929",
  "mcpServers": {
    ...
  },
  "hooks": {
    ...
  },
  "settings": {
    "autoCommit": false,
    "defaultBranch": "main",
    "editor": "code",
    "theme": "dark"
  }
}
```

---

### Customizing Behavior

**Ask Claude Code to help:**

```
Help me customize my Claude Code settings:
- Change default model to Haiku for simple tasks
- Set up auto-formatting before commits
- Configure my preferred editor
- Set custom working directory
```

---

## Lesson 4: IDE Integration

### VS Code Integration

**Install Claude Code extension:**
1. Open VS Code
2. Search for "Claude Code"
3. Install the extension

**Features:**
- Inline code assistance
- Quick fixes
- Code explanations
- Refactoring suggestions

---

### Keyboard Shortcuts

**Set up custom shortcuts:**

**In VS Code:**
```json
// keybindings.json
[
  {
    "key": "ctrl+shift+c",
    "command": "claude.explain"
  },
  {
    "key": "ctrl+shift+r",
    "command": "claude.refactor"
  }
]
```

---

## Lesson 5: Custom Workflows

### Creating Project-Specific Workflows

**Example: Feature Development Workflow**

```typescript
// ~/.config/claude/skills/new-feature.ts
export default {
  name: 'new-feature',
  description: 'Start new feature with full workflow',
  run: async (context, featureName) => {
    // 1. Create feature branch
    await context.bash(`git checkout -b feature/${featureName}`);

    // 2. Create todo list
    await context.todo([
      { content: 'Write tests', status: 'pending' },
      { content: 'Implement feature', status: 'pending' },
      { content: 'Update documentation', status: 'pending' },
      { content: 'Create PR', status: 'pending' }
    ]);

    // 3. Set up feature structure
    await context.bash(`mkdir -p src/features/${featureName}`);

    return `Feature ${featureName} initialized! Ready to start development.`;
  }
};
```

**Use it:**
```
/new-feature user-authentication
```

---

### Testing Workflow

```typescript
// ~/.config/claude/skills/test-all.ts
export default {
  name: 'test-all',
  description: 'Run all tests and checks',
  run: async (context) => {
    const results = [];

    // Run unit tests
    results.push(await context.bash('npm test'));

    // Run linter
    results.push(await context.bash('npm run lint'));

    // Run type check
    results.push(await context.bash('npm run type-check'));

    // Run security audit
    results.push(await context.bash('npm audit'));

    return results.join('\n\n');
  }
};
```

---

## Hands-On Practice

### Exercise 1: Create a Useful Skill

**Task:** Build a custom skill for your workflow

```
Create a skill that:
1. Runs all tests
2. If tests pass, creates a commit
3. Pushes to current branch
4. Opens PR if on feature branch

Name it /ship
```

---

### Exercise 2: Set Up Automation Hooks

**Task:** Create hooks for code quality

```
Set up hooks that:
1. Auto-format code before saving
2. Run linter before committing
3. Check for TODOs before pushing
4. Prevent commits with console.log
```

---

### Exercise 3: Custom Workflow

**Task:** Create a complete workflow

```
Build a /release workflow that:
1. Checks all tests pass
2. Updates version number
3. Generates changelog
4. Creates git tag
5. Pushes to remote
6. Creates GitHub release
```

---

## Module 12 Checklist

- [ ] Understand skills and hooks
- [ ] Can create custom skills
- [ ] Can set up automation hooks
- [ ] Know how to customize settings
- [ ] Can integrate with IDE
- [ ] Can create custom workflows

---

## Best Practices

**Skills:**
- Keep skills focused on one task
- Add clear descriptions
- Handle errors gracefully
- Make them reusable

**Hooks:**
- Don't make hooks too slow
- Add error handling
- Log what hooks do
- Make them optional/configurable

**Workflows:**
- Test workflows thoroughly
- Document what they do
- Make them flexible
- Version control your configs

---

## What's Next?

You can now customize Claude Code to match your exact workflow!

**Ready for Module 13?** Next, we'll explore using Claude Code with different programming languages and frameworks!

---

*Module 12 Complete!*
