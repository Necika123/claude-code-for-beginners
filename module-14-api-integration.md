# Module 14: API Integration and Web Tasks

**Goal:** Master working with external APIs and web resources using Claude Code

**Estimated Time:** 40-50 minutes

---

## What You'll Learn in This Module

By the end of this module, you will:
- Use Claude Code's WebSearch to find documentation
- Fetch API documentation with WebFetch
- Integrate third-party APIs into your projects
- Handle different authentication methods
- Implement rate limiting and quotas
- Handle API errors gracefully
- Build complete API client wrappers

---

## Lesson 1: Using WebSearch for Development

### Finding Documentation

**Search for official docs:**
```
Search for the latest Stripe API documentation
```

```
Find the React official docs for hooks
```

```
Search for Node.js Express middleware best practices
```

---

### Finding Solutions

**Search for specific problems:**
```
Search for how to fix "CORS error in Express API"
```

```
Find solutions for "JWT token expiration handling"
```

```
Search for "preventing SQL injection in Node.js"
```

---

### Researching Libraries

```
Search for the best npm packages for:
- Sending emails
- Generating PDFs
- Processing images
- Background job queues
```

---

## Lesson 2: Using WebFetch for API Documentation

### Fetching and Understanding Docs

```
Fetch the documentation from https://docs.stripe.com/api/customers/create
and create a TypeScript function to create a customer
```

```
Fetch https://api.github.com docs
and show me how to list repositories for a user
```

---

### Generating Code from Docs

```
Fetch the SendGrid API documentation
and create a complete email service class with:
- Send email method
- Send template email method
- Proper error handling
- TypeScript types
```

---

## Lesson 3: Integrating REST APIs

### Simple API Integration

**Example: Weather API**

```
Create a weather service that integrates with OpenWeatherMap API:
- Accept city name as input
- Call the weather API
- Parse and return temperature, conditions, humidity
- Handle API errors
- Cache results for 10 minutes
- Include TypeScript types
```

**Claude Code will create:**

```typescript
//weather.service.ts
import axios from 'axios';

interface WeatherData {
  temperature: number;
  conditions: string;
  humidity: number;
  city: string;
}

class WeatherService {
  private apiKey: string;
  private cache: Map<string, { data: WeatherData; expiry: number }>;

  constructor(apiKey: string) {
    this.apiKey = apiKey;
    this.cache = new Map();
  }

  async getWeather(city: string): Promise<WeatherData> {
    // Check cache first
    const cached = this.cache.get(city);
    if (cached && cached.expiry > Date.now()) {
      return cached.data;
    }

    try {
      const response = await axios.get(
        'https://api.openweathermap.org/data/2.5/weather',
        {
          params: {
            q: city,
            appid: this.apiKey,
            units: 'metric'
          }
        }
      );

      const data: WeatherData = {
        temperature: response.data.main.temp,
        conditions: response.data.weather[0].description,
        humidity: response.data.main.humidity,
        city: response.data.name
      };

      // Cache for 10 minutes
      this.cache.set(city, {
        data,
        expiry: Date.now() + 10 * 60 * 1000
      });

      return data;
    } catch (error) {
      if (axios.isAxiosError(error)) {
        if (error.response?.status === 404) {
          throw new Error(`City "${city}" not found`);
        }
        throw new Error(`Weather API error: ${error.message}`);
      }
      throw error;
    }
  }
}

export default WeatherService;
```

---

### Complex API Integration

```
Create a GitHub API client with:
- OAuth authentication
- Methods for:
  * List user repositories
  * Get repository details
  * Create issue
  * List and create pull requests
- Pagination support
- Rate limit handling
- Comprehensive error handling
- Full TypeScript types
```

---

## Lesson 4: Authentication Methods

### API Key Authentication

**Simple API key in header:**

```
Create a SendGrid email client that:
- Uses API key from environment variable
- Has method to send email
- Has method to send with template
- Validates email addresses
- Handles SendGrid errors properly
```

---

### OAuth 2.0 Integration

```
Implement GitHub OAuth flow:
1. Generate authorization URL
2. Handle callback with auth code
3. Exchange code for access token
4. Store token securely
5. Use token for API requests
6. Handle token refresh
```

**Claude Code will create the complete OAuth flow with security best practices.**

---

### JWT Token Management

```
Create an API client for our internal service that:
- Logs in to get JWT token
- Stores token securely (not in plain text)
- Includes token in all authenticated requests
- Handles token expiration
- Refreshes token automatically
- Logs out and clears tokens
```

---

## Lesson 5: Rate Limiting

### Implementing Client-Side Rate Limiting

```
Create a rate limiter class that:
- Limits API calls to X per second
- Queues requests when limit is reached
- Processes queue automatically
- Has exponential backoff for retries
- Respects API rate limit headers
- Logs when hitting limits
```

**Example implementation:**

```typescript
class APIRateLimiter {
  private queue: Array<() => Promise<any>> = [];
  private processing = false;
  private requestsPerSecond: number;
  private lastRequestTime: number = 0;

  constructor(requestsPerSecond: number) {
    this.requestsPerSecond = requestsPerSecond;
  }

  async execute<T>(fn: () => Promise<T>): Promise<T> {
    return new Promise((resolve, reject) => {
      this.queue.push(async () => {
        try {
          const result = await fn();
          resolve(result);
        } catch (error) {
          reject(error);
        }
      });

      if (!this.processing) {
        this.processQueue();
      }
    });
  }

  private async processQueue() {
    this.processing = true;

    while (this.queue.length > 0) {
      const now = Date.now();
      const timeSinceLastRequest = now - this.lastRequestTime;
      const minInterval = 1000 / this.requestsPerSecond;

      if (timeSinceLastRequest < minInterval) {
        await this.sleep(minInterval - timeSinceLastRequest);
      }

      const request = this.queue.shift();
      if (request) {
        this.lastRequestTime = Date.now();
        await request();
      }
    }

    this.processing = false;
  }

  private sleep(ms: number): Promise<void> {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
}
```

---

## Lesson 6: Error Handling

### Robust API Error Handling

```
Create comprehensive error handling for API calls that:
- Distinguishes between error types:
  * Network errors (no connection)
  * 4xx client errors (bad request, unauthorized, etc.)
  * 5xx server errors (temporary issues)
  * Timeout errors
- Retries appropriate errors (5xx, timeouts)
- Doesn't retry client errors (4xx)
- Uses exponential backoff for retries
- Logs all errors with context
- Returns user-friendly error messages
```

---

### Retry Logic with Exponential Backoff

```typescript
async function fetchWithRetry<T>(
  url: string,
  options: RequestInit = {},
  maxRetries: number = 3
): Promise<T> {
  for (let attempt = 0; attempt < maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);

      // Don't retry client errors
      if (response.status >= 400 && response.status < 500) {
        const error = await response.text();
        throw new Error(`Client error ${response.status}: ${error}`);
      }

      // Retry server errors
      if (response.status >= 500) {
        if (attempt === maxRetries - 1) {
          throw new Error(`Server error ${response.status} after ${maxRetries} attempts`);
        }
        // Wait before retrying (exponential backoff)
        await sleep(Math.pow(2, attempt) * 1000);
        continue;
      }

      // Success
      return await response.json();

    } catch (error) {
      if (attempt === maxRetries - 1) {
        throw error;
      }
      // Network error - retry with backoff
      await sleep(Math.pow(2, attempt) * 1000);
    }
  }

  throw new Error('Max retries exceeded');
}

function sleep(ms: number): Promise<void> {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

---

## Lesson 7: Building Complete API Wrappers

### Production-Ready API Client

```
Build a complete Stripe API wrapper with:

Core Features:
- Customer management (create, get, update, delete)
- Payment processing
- Subscription handling
- Webhook verification

Infrastructure:
- TypeScript types for all endpoints
- Proper error handling with custom error classes
- Retry logic for transient failures
- Rate limiting
- Request/response logging
- Idempotency keys for safe retries
- Comprehensive tests with mocked responses

Security:
- API key from environment
- Input validation
- Webhook signature verification
```

---

## Hands-On Practice

### Exercise 1: Weather CLI App

**Task:** Build a weather command-line tool

```
Create a CLI weather app that:
1. Takes city name as argument
2. Calls OpenWeatherMap API
3. Displays current weather nicely
4. Shows 5-day forecast
5. Caches responses
6. Handles errors gracefully
7. Has colorful output

Example usage:
node weather.js "San Francisco"
```

---

### Exercise 2: GitHub CLI Tool

**Task:** Build a GitHub client

```
Create a GitHub CLI tool that:
- Authenticates with personal access token
- Lists your repositories
- Shows open issues for a repo
- Creates new issues
- Lists pull requests
- Creates pull requests
- All with proper error handling and nice formatting
```

---

### Exercise 3: Multi-API Dashboard

**Task:** Combine multiple APIs

```
Build a daily digest service that fetches:
- Weather from OpenWeatherMap
- Top news from NewsAPI
- Stock prices from Alpha Vantage
- Your GitHub activity from GitHub API

Combines all into a daily brief
Handles failure of individual APIs gracefully
Caches each appropriately
Sends as email or displays in terminal
```

---

## Module 14 Checklist

Before moving to Module 15, make sure you can:

- [ ] Use WebSearch to find documentation
- [ ] Use WebFetch to get API docs
- [ ] Integrate REST APIs
- [ ] Handle different authentication methods
- [ ] Implement rate limiting
- [ ] Handle API errors with retry logic
- [ ] Build complete API wrappers
- [ ] Test API integrations properly

---

## Best Practices

**API Integration:**
- ✅ Use environment variables for API keys
- ✅ Implement proper error handling
- ✅ Add retry logic for transient failures
- ✅ Cache when appropriate
- ✅ Respect rate limits
- ✅ Log API interactions
- ✅ Validate all inputs
- ✅ Use TypeScript for type safety

**Security:**
- ✅ Never commit API keys
- ✅ Use HTTPS only
- ✅ Validate API responses
- ✅ Sanitize before using data
- ✅ Handle tokens securely

**Testing:**
- ✅ Mock API responses in tests
- ✅ Test error scenarios
- ✅ Test rate limiting
- ✅ Test authentication flows

---

## Common Mistakes to Avoid

❌ Hardcoding API keys
❌ Not handling errors
❌ Ignoring rate limits
❌ Not using TypeScript types
❌ Exposing sensitive data in logs
❌ Not caching expensive requests
❌ Not validating API responses

---

## What's Next?

Great work! You can now integrate with any API and build powerful integrations!

**Ready for Module 15?** The final module covers deploying your applications to production!

---

*Module 14 Complete!*
