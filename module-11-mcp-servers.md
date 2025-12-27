# Module 11: MCP Servers - Extending Claude Code

**Goal:** Learn to use and create Model Context Protocol (MCP) servers to extend Claude Code's capabilities

**Estimated Time:** 40-50 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand what MCP is and why it's powerful
- Know how to install and configure MCP servers
- Use common MCP servers (filesystem, database, etc.)
- Create your own custom MCP server
- Integrate third-party services with MCP

---

## Lesson 1: Understanding MCP

### What is MCP?

**Model Context Protocol (MCP)** is a standard way to give Claude Code access to external data and services.

**Think of MCP servers as plugins that:**
- Give Claude Code new capabilities
- Connect to databases, APIs, file systems
- Provide domain-specific knowledge
- Extend what Claude Code can do

---

### Why Use MCP?

**Without MCP:**
- Limited to built-in tools
- Can't access your databases directly
- Can't integrate with your services
- Limited context about your systems

**With MCP:**
- Access databases directly
- Connect to your tools (GitHub, Notion, etc.)
- Custom integrations
- Unlimited extensibility

---

## Lesson 2: Installing MCP Servers

### Configuration File

**MCP servers are configured in:**
```
~/.config/claude/config.json
```

**Example configuration:**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/directory"]
    }
  }
}
```

---

### Installing Your First MCP Server

**Ask Claude Code to help:**

```
Help me install the filesystem MCP server.
I want to give you access to my /home/user/projects directory.
```

**Claude Code will:**
1. Show you the configuration to add
2. Help you edit the config file
3. Verify the setup works

---

## Lesson 3: Common MCP Servers

### Filesystem MCP Server

**Purpose:** Access files and directories

**Configuration:**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/allowed/path"]
    }
  }
}
```

**Usage:**
```
Using the filesystem MCP server, list all Python files in my projects directory
```

---

### PostgreSQL MCP Server

**Purpose:** Query and manage PostgreSQL databases

**Configuration:**
```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "POSTGRES_URL": "postgresql://user:pass@localhost:5432/dbname"
      }
    }
  }
}
```

**Usage:**
```
Using the postgres MCP server, show me all tables in the database
Query the users table and show me the schema
```

---

### SQLite MCP Server

**Purpose:** Work with SQLite databases

**Configuration:**
```json
{
  "mcpServers": {
    "sqlite": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sqlite", "/path/to/database.db"]
    }
  }
}
```

**Usage:**
```
Using the sqlite MCP server, analyze the database schema
Find all tables with user data
```

---

### GitHub MCP Server

**Purpose:** Interact with GitHub repositories

**Configuration:**
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

**Usage:**
```
Using the GitHub MCP server:
- List my repositories
- Show open issues in my-repo
- Create an issue for the bug I just found
```

---

## Lesson 4: Creating a Custom MCP Server

### Why Create Custom Servers?

**Create custom MCP servers for:**
- Your company's internal APIs
- Custom databases or data stores
- Specialized tools or services
- Domain-specific knowledge

---

### MCP Server Basics

**An MCP server provides:**
- **Tools** - Functions Claude can call
- **Resources** - Data Claude can access
- **Prompts** - Predefined prompt templates

---

### Creating a Simple MCP Server

**Example: Weather API MCP Server**

```javascript
// weather-mcp-server.js
import { McpServer } from '@modelcontextprotocol/sdk';

const server = new McpServer({
  name: 'weather',
  version: '1.0.0'
});

// Define a tool
server.addTool({
  name: 'get_weather',
  description: 'Get current weather for a city',
  parameters: {
    type: 'object',
    properties: {
      city: {
        type: 'string',
        description: 'City name'
      }
    },
    required: ['city']
  },
  handler: async ({ city }) => {
    // Call weather API
    const response = await fetch(
      `https://api.weather.com/...?city=${city}`
    );
    const data = await response.json();

    return {
      temperature: data.temp,
      conditions: data.conditions,
      humidity: data.humidity
    };
  }
});

server.start();
```

---

### Configuring Your Custom Server

**Add to config.json:**
```json
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["/path/to/weather-mcp-server.js"],
      "env": {
        "WEATHER_API_KEY": "your-api-key"
      }
    }
  }
}
```

---

### Using Your Custom Server

```
Using the weather MCP server, what's the weather in San Francisco?
```

---

## Lesson 5: Advanced MCP Features

### Resources

**Provide data that Claude can read:**

```javascript
server.addResource({
  uri: 'company://employees',
  name: 'Employee Directory',
  description: 'List of all employees',
  mimeType: 'application/json',
  handler: async () => {
    const employees = await db.query('SELECT * FROM employees');
    return JSON.stringify(employees);
  }
});
```

---

### Prompts

**Predefined prompt templates:**

```javascript
server.addPrompt({
  name: 'code_review',
  description: 'Review code following company standards',
  template: async ({ filename }) => {
    const standards = await loadCompanyStandards();
    return `Review ${filename} according to these standards:\n${standards}`;
  }
});
```

---

## Lesson 6: Real-World MCP Examples

### Example 1: Company Database MCP

**Scenario:** Access your company's database

```javascript
// company-db-mcp.js
import { McpServer } from '@modelcontextprotocol/sdk';
import pg from 'pg';

const server = new McpServer({
  name: 'company-db',
  version: '1.0.0'
});

const db = new pg.Client({
  connectionString: process.env.DATABASE_URL
});

server.addTool({
  name: 'query_customers',
  description: 'Query customer data',
  parameters: {
    type: 'object',
    properties: {
      filter: { type: 'string' }
    }
  },
  handler: async ({ filter }) => {
    const result = await db.query(
      'SELECT * FROM customers WHERE $1',
      [filter]
    );
    return result.rows;
  }
});

server.start();
```

---

### Example 2: Internal API MCP

**Scenario:** Connect to your internal services

```javascript
// internal-api-mcp.js
server.addTool({
  name: 'deploy_service',
  description: 'Deploy a service to production',
  parameters: {
    type: 'object',
    properties: {
      service: { type: 'string' },
      version: { type: 'string' }
    },
    required: ['service', 'version']
  },
  handler: async ({ service, version }) => {
    const response = await fetch(
      `https://internal-api.company.com/deploy`,
      {
        method: 'POST',
        headers: {
          'Authorization': `Bearer ${process.env.API_TOKEN}`,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ service, version })
      }
    );

    return await response.json();
  }
});
```

---

## Lesson 7: Best Practices

### Security

**Protect sensitive data:**
- Use environment variables for secrets
- Validate all inputs
- Limit access to sensitive operations
- Use authentication/authorization
- Audit log all actions

---

### Error Handling

**Handle errors gracefully:**

```javascript
server.addTool({
  name: 'risky_operation',
  handler: async (params) => {
    try {
      const result = await doSomethingRisky(params);
      return result;
    } catch (error) {
      console.error('Operation failed:', error);
      throw new Error(`Failed to perform operation: ${error.message}`);
    }
  }
});
```

---

### Performance

**Optimize for speed:**
- Cache frequently accessed data
- Use connection pooling for databases
- Implement timeouts
- Limit result sizes

---

## Hands-On Practice

### Exercise 1: Install and Use MCP Servers

**Task:** Set up common MCP servers

```
1. Install the filesystem MCP server
2. Configure it for your projects directory
3. Use it to analyze your code
4. Install the GitHub MCP server
5. Use it to list your repositories
```

---

### Exercise 2: Create a Simple MCP Server

**Task:** Build a custom MCP server

```
Create an MCP server that:
- Connects to a JSON file of notes
- Provides tools to:
  * List all notes
  * Search notes by keyword
  * Add new note
  * Delete note

Test it with Claude Code
```

---

### Exercise 3: Build a Practical MCP Server

**Task:** Create a useful integration

**Choose one:**
- Todo list manager (connects to a file or database)
- Git helper (shortcuts for common git operations)
- Project template generator
- Code snippet library

---

## Module 11 Checklist

- [ ] Understand what MCP is
- [ ] Know how to configure MCP servers
- [ ] Can install common MCP servers
- [ ] Can create custom MCP servers
- [ ] Understand MCP security considerations
- [ ] Can use MCP to extend Claude Code

---

## Available MCP Servers

**Official servers:**
- @modelcontextprotocol/server-filesystem
- @modelcontextprotocol/server-postgres
- @modelcontextprotocol/server-sqlite
- @modelcontextprotocol/server-github
- @modelcontextprotocol/server-slack

**Community servers:**
- Many more on npm and GitHub
- Search for "mcp-server" on npm

---

## What's Next?

You now understand how to extend Claude Code with MCP servers! You can:
- Connect to any database
- Integrate with any API
- Create custom tools
- Build domain-specific assistants

**Ready for Module 12?** Next, we'll learn about Skills and Hooks - customizing Claude Code's behavior even further!

---

*Module 11 Complete!*
