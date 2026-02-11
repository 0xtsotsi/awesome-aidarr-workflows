# test-runner

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cmanfre7/test-runner/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cmanfre7/test-runner/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run test-runner`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the test-runner workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: test-runner
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# test-runner

Write and run tests across languages and frameworks.

## Framework Selection

| Language | Unit Tests | Integration | E2E |
|----------|-----------|-------------|-----|
| TypeScript/JS | Vitest (preferred), Jest | Supertest | Playwright |
| Python | pytest | pytest + httpx | Playwright |
| Swift | XCTest | XCTest | XCUITest |

## Quick Start by Framework

### Vitest (TypeScript / JavaScript)
```bash
npm install -D vitest @testing-library/react @testing-library/jest-dom
```

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config'
export default defineConfig({
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './tests/setup.ts',
  },
})
```

```bash
npx vitest              # Watch mode
npx vitest run          # Single run
npx vitest --coverage   # With coverage
```

### Jest
```bash
npm install -D jest @types/jest ts-jest
```

```bash
npx jest                # Run all
npx jest --watch        # Watch mode
npx jest --coverage     # With coverage
npx jest path/to/test   # Single file
```

### pytest (Python)
```bash
uv pip install pytest pytest-cov pytest-asyncio httpx
```

```bash
pytest                          # Run all
pytest -v                       # Verbose
pytest -x                       # Stop on first failure
pytest --cov=app                # With coverage
pytest tests/test_api.py -k "test_login"  # Specific test
pytest --tb=short               # Short tracebacks
```

### XCTest (Swift)
```bash
swift test                      # Run all tests
swift test --filter MyTests     # Specific test suite
swift test --parallel           # Parallel execution
```

### Playwright (E2E)
```bash
npm install -D @playwright/test
npx playwright install
```

```bash
npx playwright test                    # Run all
npx playwright test --headed           # With browser visible
npx playwright test --debug            # Debug mode
npx playwright test --project=chromium # Specific browser
npx playwright show-report             # View HTML report
```

## TDD Workflow

1. **Red** — Write a failing test that describes the desired behavior.
2. **Green** — Write the minimum code to make the test pass.
3. **Refactor** — Clean up the code while keeping tests green.

```
┌─────────┐     ┌─────────┐     ┌──────────┐
│  Write   │────▶│  Write  │────▶│ Refactor │──┐
│  Test    │     │  Code   │     │  Code    │  │
│  (Red)   │     │ (Green) │     │          │  │
└─────────┘     └─────────┘     └──────────┘  │
     ▲                                          │
     └──────────────────────────────────────────┘
```

## Test Patterns

### Arrange-Act-Assert
```typescript
test('calculates total with tax', () => {
  // Arrange
  const cart = new Cart([{ price: 100, qty: 2 }]);

  // Act
  const total = cart.totalWithTax(0.08);

  // Assert
  expect(total).toBe(216);
});
```

### Testing Async Code
```typescript
test('fetches user data', async () => {
  const user = await getUser('123');
  expect(user.name).toBe('Colt');
});
```

### Mocking
```typescript
import { vi } from 'vitest';

const mockFetch = vi.fn().mockResolvedValue({
  json: () => Promise.resolve({ id: 1, name: 'Test' }),
});
vi.stubGlobal('fetch', mockFetch);
```

### Testing API Endpoints (Python)
```python
import pytest
from httpx import AsyncClient
from app.main import app

@pytest.mark.asyncio
async def test_get_users():
    async with AsyncClient(app=app, base_url="http://test") as client:
        response = await client.get("/users")
    assert response.status_code == 200
    assert isinstance(response.json(), list)
```

### Testing React Components
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

test('calls onClick when clicked', () => {
  const handleClick = vi.fn();
  render(<Button onClick={handleClick}>Click me</Button>);
  fireEvent.click(screen.getByText('Click me'));
  expect(handleClick).toHaveBeenCalledOnce();
});
```

## Coverage Commands

```bash
# JavaScript/TypeScript
npx vitest --coverage          # Vitest (uses v8 or istanbul)
npx jest --coverage            # Jest

# Python
pytest --cov=app --cov-report=html    # HTML report
pytest --cov=app --cov-report=term    # Terminal output
pytest --cov=app --cov-fail-under=80  # Fail if < 80%

# View HTML coverage report
open coverage/index.html       # macOS
open htmlcov/index.html        # Python
```

## What to Test

**Always test:**
- Public API / exported functions
- Edge cases: empty input, null, boundary values
- Error handling: invalid input, network failures
- Business logic: calculations, state transitions

**Don't bother testing:**
- Private implementation details
- Framework internals (React rendering, Express routing)
- Trivial getters/setters
- Third-party library behavior

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
