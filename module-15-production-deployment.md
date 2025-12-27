# Module 15: Production Deployment

**Goal:** Deploy your applications to production with Claude Code's assistance

**Estimated Time:** 60-90 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Understand deployment fundamentals
- Deploy to various platforms (Vercel, Heroku, VPS)
- Use Docker for containerization
- Set up CI/CD pipelines
- Configure production environments
- Implement monitoring and logging
- Follow security best practices
- Handle database migrations in production

---

## Lesson 1: Deployment Fundamentals

### What is Deployment?

**Deployment** means making your application available on the internet so others can use it.

**Development vs Production:**

**Development:**
- Running on your computer
- You're the only user
- Can break things and fix them
- Debug mode enabled
- Test data

**Production:**
- Running on servers
- Real users access it
- Must be reliable and fast
- No debug info exposed
- Real data

---

### Deployment Checklist

**Before deploying, ensure:**
```
Help me prepare this application for production:
1. Check all environment variables are documented
2. Verify no secrets in code
3. Ensure error handling doesn't leak sensitive info
4. Add proper logging
5. Set up health check endpoint
6. Configure CORS properly
7. Add rate limiting
8. Set up HTTPS
9. Minify/bundle code
10. Run all tests
```

---

## Lesson 2: Deploying to Vercel

### What is Vercel?

**Vercel** is a platform optimized for frontend frameworks (Next.js, React, etc.)

**Best for:**
- Next.js applications
- React/Vue/Svelte apps
- Serverless functions
- Static sites

---

### Deploying with Claude Code

```
Help me deploy this Next.js application to Vercel:
1. Install Vercel CLI
2. Configure vercel.json
3. Set up environment variables
4. Deploy to production
5. Set up custom domain
```

**Claude Code will:**

```bash
# Install Vercel CLI
npm install -g vercel

# Login
vercel login

# Deploy
vercel --prod
```

**Create vercel.json:**
```json
{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "devCommand": "npm run dev",
  "installCommand": "npm install",
  "framework": "nextjs",
  "env": {
    "DATABASE_URL": "@database-url",
    "API_KEY": "@api-key"
  }
}
```

---

## Lesson 3: Deploying to Heroku

### What is Heroku?

**Heroku** is a platform for deploying backend applications and full-stack apps.

**Best for:**
- Node.js APIs
- Python/Django apps
- Ruby on Rails
- Full-stack applications

---

### Deploying with Claude Code

```
Help me deploy this Express API to Heroku:
1. Create Procfile
2. Set up heroku.yml if needed
3. Configure environment variables
4. Add PostgreSQL database
5. Set up deployment
6. Configure logging
```

**Claude Code creates:**

**Procfile:**
```
web: node dist/server.js
```

**Deploy commands:**
```bash
# Install Heroku CLI first, then:

# Login
heroku login

# Create app
heroku create my-app-name

# Add PostgreSQL
heroku addons:create heroku-postgresql:hobby-dev

# Set environment variables
heroku config:set NODE_ENV=production
heroku config:set API_KEY=your-key

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

---

## Lesson 4: Deploying to a VPS (Virtual Private Server)

### What is a VPS?

**VPS** = Your own server (e.g., DigitalOcean, Linode, AWS EC2)

**Best for:**
- Full control needed
- Custom configurations
- Multiple applications
- Learning server management

---

### Setting Up VPS Deployment

```
Help me deploy this Node.js app to an Ubuntu VPS:
1. Set up the server (Node.js, PM2, Nginx)
2. Configure firewall
3. Set up SSL with Let's Encrypt
4. Configure Nginx reverse proxy
5. Set up PM2 for process management
6. Configure automatic restarts
7. Set up deployment script
```

**Claude Code will create deployment guide:**

**On the server:**
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

# Install PM2
sudo npm install -g pm2

# Install Nginx
sudo apt install -y nginx

# Configure firewall
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

**Nginx configuration:**
```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

**PM2 ecosystem file:**
```javascript
module.exports = {
  apps: [{
    name: 'my-app',
    script: './dist/server.js',
    instances: 'max',
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
};
```

---

## Lesson 5: Docker Deployment

### Why Docker?

**Docker** packages your app with everything it needs to run.

**Benefits:**
- Consistent across environments
- Easy to deploy anywhere
- Isolates dependencies
- Scales easily

---

### Creating Docker Configuration

```
Create Docker configuration for this Node.js API:
1. Write Dockerfile
2. Create .dockerignore
3. Write docker-compose.yml for local development
4. Add production docker-compose
5. Include health checks
```

**Dockerfile:**
```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production stage
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --from=builder /app/dist ./dist

# Security: run as non-root
USER node

# Health check
HEALTHCHECK --interval=30s --timeout=3s \
  CMD node healthcheck.js

EXPOSE 3000
CMD ["node", "dist/server.js"]
```

**.dockerignore:**
```
node_modules
npm-debug.log
.env
.git
.gitignore
README.md
.vscode
coverage
.DS_Store
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:14-alpine
    environment:
      - POSTGRES_DB=mydb
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

## Lesson 6: CI/CD Pipelines

### What is CI/CD?

**CI** = Continuous Integration (automatically test code)
**CD** = Continuous Deployment (automatically deploy code)

**Benefits:**
- Automatic testing
- Automatic deployment
- Catch bugs early
- Deploy faster and safer

---

### GitHub Actions for CI/CD

```
Create a GitHub Actions workflow that:
1. Runs on every push to main
2. Runs all tests
3. Runs linter
4. Builds the application
5. Deploys to production if tests pass
6. Sends notifications on failure
```

**.github/workflows/deploy.yml:**
```yaml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint

      - name: Run tests
        run: npm test

      - name: Build
        run: npm run build

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v3

      - name: Deploy to production
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
        run: |
          ./scripts/deploy.sh
```

---

## Lesson 7: Environment Configuration

### Managing Environment Variables

```
Help me set up proper environment configuration:
1. Create .env.example template
2. Document all environment variables
3. Set up different configs for dev/staging/prod
4. Add validation for required variables
5. Secure sensitive values
```

**config/env.ts:**
```typescript
import dotenv from 'dotenv';

dotenv.config();

interface Config {
  nodeEnv: string;
  port: number;
  databaseUrl: string;
  jwtSecret: string;
  apiKey: string;
}

function validateEnv(): Config {
  const required = [
    'DATABASE_URL',
    'JWT_SECRET',
    'API_KEY'
  ];

  for (const key of required) {
    if (!process.env[key]) {
      throw new Error(`Missing required environment variable: ${key}`);
    }
  }

  return {
    nodeEnv: process.env.NODE_ENV || 'development',
    port: parseInt(process.env.PORT || '3000'),
    databaseUrl: process.env.DATABASE_URL!,
    jwtSecret: process.env.JWT_SECRET!,
    apiKey: process.env.API_KEY!
  };
}

export const config = validateEnv();
```

---

## Lesson 8: Monitoring and Logging

### Setting Up Production Logging

```
Add production-grade logging:
1. Use structured logging (JSON format)
2. Different log levels (error, warn, info, debug)
3. Log rotation
4. Send errors to monitoring service
5. Don't log sensitive data
```

**Using Winston for logging:**
```typescript
import winston from 'winston';

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  transports: [
    // Write all logs to console
    new winston.transports.Console({
      format: winston.format.simple()
    }),
    // Write errors to error.log
    new winston.transports.File({
      filename: 'logs/error.log',
      level: 'error'
    }),
    // Write all logs to combined.log
    new winston.transports.File({
      filename: 'logs/combined.log'
    })
  ]
});

export default logger;
```

---

### Health Checks

```
Add health check endpoints:
1. /health - basic health check
2. /health/ready - readiness check (dependencies)
3. /health/live - liveness check
```

```typescript
app.get('/health', (req, res) => {
  res.json({ status: 'ok', timestamp: new Date().toISOString() });
});

app.get('/health/ready', async (req, res) => {
  try {
    // Check database
    await db.query('SELECT 1');

    res.json({
      status: 'ready',
      checks: {
        database: 'ok'
      }
    });
  } catch (error) {
    res.status(503).json({
      status: 'not ready',
      checks: {
        database: 'failed'
      }
    });
  }
});
```

---

## Lesson 9: Database Migrations in Production

### Safe Database Migrations

```
Create a safe database migration strategy:
1. Version all schema changes
2. Write up and down migrations
3. Test migrations on staging first
4. Backup before migrating
5. Have rollback plan
```

**Using a migration tool:**
```typescript
// migrations/001_create_users_table.ts
export async function up(db) {
  await db.schema.createTable('users', (table) => {
    table.increments('id').primary();
    table.string('email').notNullable().unique();
    table.string('password_hash').notNullable();
    table.timestamps(true, true);
  });
}

export async function down(db) {
  await db.schema.dropTable('users');
}
```

**Running migrations:**
```bash
# Backup database first!
pg_dump mydb > backup_$(date +%Y%m%d).sql

# Run migrations
npm run migrate:latest

# If something goes wrong, rollback
npm run migrate:rollback
```

---

## Hands-On Practice

### Exercise 1: Deploy Full-Stack App

**Task:** Deploy a complete application

```
Take the project from Module 9 and:
1. Prepare it for production
2. Set up environment configuration
3. Add health check endpoints
4. Create Docker configuration
5. Deploy to your choice of platform
6. Set up monitoring
7. Test in production
```

---

### Exercise 2: CI/CD Pipeline

**Task:** Set up automated deployment

```
Create a CI/CD pipeline that:
1. Runs tests on every PR
2. Deploys to staging on merge to develop
3. Deploys to production on merge to main
4. Sends notifications on failure
5. Includes database migrations
```

---

### Exercise 3: Zero-Downtime Deployment

**Task:** Implement rolling deployment

```
Set up deployment strategy that:
1. Keeps old version running during deploy
2. Gradually shifts traffic to new version
3. Monitors for errors
4. Automatically rolls back if issues detected
5. Ensures zero downtime
```

---

## Module 15 Checklist

Congratulations on completing the course! Make sure you can:

- [ ] Prepare applications for production
- [ ] Deploy to various platforms
- [ ] Use Docker for containerization
- [ ] Set up CI/CD pipelines
- [ ] Configure environments properly
- [ ] Implement monitoring and logging
- [ ] Handle database migrations safely
- [ ] Follow security best practices

---

## Production Deployment Best Practices

**Before Every Deployment:**
- ✅ Run all tests
- ✅ Review changes
- ✅ Backup database
- ✅ Have rollback plan
- ✅ Deploy during low-traffic times
- ✅ Monitor after deployment

**Security:**
- ✅ Use HTTPS everywhere
- ✅ Keep dependencies updated
- ✅ Don't expose error details
- ✅ Use security headers
- ✅ Rate limit APIs
- ✅ Validate all input

**Performance:**
- ✅ Minify and bundle assets
- ✅ Enable compression
- ✅ Use CDN for static files
- ✅ Cache appropriately
- ✅ Monitor performance

---

## Congratulations!

You've completed the **Claude Code for Beginners** course!

You now have the skills to:
- Build applications with Claude Code
- Write clean, professional code
- Test and debug effectively
- Deploy to production
- Follow best practices

**What's next:**
- Build real projects
- Contribute to open source
- Share your knowledge
- Keep learning!

---

*Course Complete! Happy building with Claude Code!*
