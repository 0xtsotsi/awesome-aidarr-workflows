# intelligent-budget-tracker

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/enjuguna/intelligent-budget-tracker/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/enjuguna/intelligent-budget-tracker/SKILL.md)
> Category: AI & LLMs

---

## Description

Intelligent budget tracking and financial management library for AI agents - expense tracking, income management, budgets, savings goals, and LLM-powered insights

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Intelligent budget tracking and financial management library for AI agents - expense tracking, income management, budgets, savings goals, and LLM-powered insights

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run intelligent-budget-tracker`)
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
You are executing the intelligent-budget-tracker workflow. Use the following context:

Description: Intelligent budget tracking and financial management library for AI agents - expense tracking, income management, budgets, savings goals, and LLM-powered insights

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: intelligent-budget-tracker
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Agent Money Tracker

A TypeScript library for AI agents to track expenses, income, budgets, and savings goals with LLM-powered natural language parsing. **No frontend required** - designed for programmatic use by agents and bots.

## Installation

```bash
npm install agent-money-tracker
```

---

## Usage

### Initialize the Budget Tracker

```typescript
import { clawhub } from 'agent-money-tracker';

// Initialize (required before any operations)
await clawhub.initialize();

// Or with custom storage path
await clawhub.initialize('/path/to/data');
```

### Expense Tracking

```typescript
// Add an expense
await clawhub.addExpense(50, 'Food & Dining', 'Grocery shopping', {
  date: '2026-01-31',
  tags: ['weekly', 'essentials'],
  merchant: 'Whole Foods'
});

// Natural language input
await clawhub.addFromNaturalLanguage('spent $45 on uber yesterday');

// Get recent expenses
const expenses = clawhub.getExpenses({ limit: 10 });

// Filter by category and date range
const foodExpenses = clawhub.getExpenses({
  category: 'Food & Dining',
  startDate: '2026-01-01',
  endDate: '2026-01-31'
});
```

### Income Tracking

```typescript
// Add income
await clawhub.addIncome(5000, 'Salary', 'January salary', {
  date: '2026-01-15'
});

// Add freelance income
await clawhub.addIncome(500, 'Freelance', 'Website project');

// Get all income
const income = clawhub.getIncome();
```

### Budget Management

```typescript
// Create a monthly budget
await clawhub.createBudget('Food Budget', 'Food & Dining', 500, 'monthly', 0.8);

// Check budget status
const status = clawhub.getBudgetStatus();
// Returns: [{ budgetName, spent, limit, remaining, percentageUsed, status }]

// Get budget alerts
const alerts = clawhub.checkBudgetAlerts();
// Returns warnings when threshold or limit exceeded

// Get smart budget suggestions
const suggestions = clawhub.suggestBudgetLimits();
// Returns: [{ category, suggested, average, max }]
```

### Savings Goals

```typescript
// Create a savings goal
await clawhub.createGoal('Emergency Fund', 10000, {
  description: '6 months expenses',
  deadline: '2026-12-31',
  priority: 'high'
});

// Add contribution
await clawhub.contributeToGoal('goal_abc123', 500, 'January savings');

// Check progress
const progress = clawhub.getGoalProgress();
// Returns: [{ goalName, targetAmount, currentAmount, percentageComplete, daysRemaining, onTrack }]
```

### Analytics & Reports

```typescript
// Monthly spending summary
const summary = clawhub.getSpendingSummary();
// Returns: { totalExpenses, totalIncome, netSavings, expensesByCategory, incomeByCategory }

// View monthly trends
const trends = clawhub.getMonthlyTrends(12);
// Returns: [{ date, expenses, income, netSavings }]

// Full monthly report
const report = clawhub.generateMonthlyReport(2026, 1);

// Compare to last month
const comparison = clawhub.compareToLastMonth();
// Returns: { expenseChange, incomeChange, topIncreases, topDecreases }
```

### Smart Insights

```typescript
// Generate AI-powered insights
const insights = await clawhub.generateInsights();
// Returns insights like:
// - "⚠️ Your dining expenses are 3x higher than usual"
// - "💡 Cancel unused subscriptions to save $50/month"
// - "🏆 You've tracked expenses for 7 consecutive days!"

// Get unread insights
const unreadInsights = clawhub.getInsights();
```

### Recurring Transactions

```typescript
// Create recurring expense (e.g., Netflix subscription)
await clawhub.createRecurring(
  'expense', 15.99, 'Subscriptions', 'Netflix', 'monthly',
  { startDate: '2026-02-01' }
);

// Create recurring income (e.g., salary)
await clawhub.createRecurring(
  'income', 5000, 'Salary', 'Monthly salary', 'monthly'
);

// Process due recurring transactions
await clawhub.processRecurring();
```

### Data Management

```typescript
// Get statistics
const stats = clawhub.getStats();
// Returns: { totalTransactions, totalExpenses, totalIncome, netSavings, avgExpense, topCategory }

// Get available categories
const categories = clawhub.getCategories();

// Export data
const jsonData = await clawhub.exportData();

// Create backup
const backupPath = await clawhub.backup();

// Get storage location
const dataPath = clawhub.getDataPath();
```

---

## Default Categories

### Expense Categories
| Category | Icon |
|----------|------|
| Food & Dining | 🍔 |
| Transportation | 🚗 |
| Shopping | 🛍️ |
| Bills & Utilities | 💡 |
| Entertainment | 🎬 |
| Health & Fitness | 💪 |
| Education | 📚 |
| Personal Care | 💄 |
| Subscriptions | 📱 |

### Income Categories
| Category | Icon |
|----------|------|
| Salary | 💰 |
| Freelance | 💻 |
| Investments | 📈 |
| Gifts | 🎁 |

---

## Cross-Platform Storage

Data is stored in platform-specific locations:

| Platform | Default Path |
|----------|-------------|
| Windows | `%APPDATA%\clawhub` |
| macOS | `~/Library/Application Support/clawhub` |
| Linux | `~/.local/share/clawhub` |

Override with environment variable:
```bash
export CLAWHUB_DATA_PATH=/custom/path
```

---

## API Reference Summary

| Method | Description |
|--------|-------------|
| `initialize(path?)` | Initialize the budget tracker |
| `addExpense(amount, category, description, options?)` | Add expense |
| `addIncome(amount, category, description, options?)` | Add income |
| `addFromNaturalLanguage(text)` | Parse and add from natural language |
| `createBudget(name, category, limit, period, threshold?)` | Create budget |
| `getBudgetStatus()` | Get all budget statuses |
| `checkBudgetAlerts()` | Get budget warnings/alerts |
| `createGoal(name, target, options?)` | Create savings goal |
| `contributeToGoal(goalId, amount, note?)` | Add to goal |
| `getGoalProgress()` | Get all goal progress |
| `getSpendingSummary(start?, end?)` | Get spending breakdown |
| `getMonthlyTrends(months?)` | Get monthly trend data |
| `generateMonthlyReport(year?, month?)` | Generate full report |
| `generateInsights()` | Generate AI insights |
| `createRecurring(type, amount, category, desc, freq, options?)` | Create recurring |
| `processRecurring()` | Process due recurring transactions |
| `getStats()` | Get transaction statistics |
| `exportData()` | Export all data as JSON |
| `backup()` | Create timestamped backup |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
