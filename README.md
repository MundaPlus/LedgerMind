# LedgerMind

**A self-hosted personal finance tracker with an AI assistant and an API for agents.** LedgerMind brings bank accounts, credit cards, loans, budgets, investments and physical assets into one private dashboard, and makes the numbers line up with what the bank says.

It runs on your own server for a single owner. An AI assistant answers questions about your finances in plain language, using a local Ollama model or a cloud model through OpenRouter.

<!-- screenshots -->

## Features

- **Transactions.** Create, edit, categorise, tag and split transactions, with templates for common entries and bulk import from CSV, OFX and QIF bank exports.
- **Revolut and bank sync.** Revolut statements import as one account covering the current account, savings vaults and pockets. Bank accounts can also be linked through GoCardless for automatic account creation, transaction sync and balance reconciliation.
- **Own transfers recognised.** Money moved between your own accounts, card payments and top-ups are matched instead of showing up as income and spending.
- **Accounts and net worth.** Bank accounts with overdraft limits, savings, credit cards, loans and assets, with a net worth trend built from month-end balances.
- **Loan repayment plans.** Import the bank's repayment plan; payments are matched to instalments and only principal lowers the balance. The debt planner shows remaining interest, payoff dates, avalanche and snowball strategies, and what an extra payment would change.
- **Credit cards.** Paid-in-full cards record each payment as that month's spending; revolving cards track the amount owed from entered statements.
- **Recurring payments.** Expected bills, subscriptions and salary are suggested from history and matched against each import, with a notice when a payment is missing or its amount changes. They feed a cashflow calendar and a forecast.
- **Budgets, goals and spending.** Monthly category budgets with alerts, savings goals with milestones, and a spending page with a category-by-month table that drills down to merchants and transactions.
- **Analytics.** Spending by category and merchant, income against expenses, savings rate, trends and runway, filterable by period.
- **AI assistant and advisor.** A chat that answers questions about your data, a proactive advisor that points out spending patterns and budget risks, and AI suggestions for category rules.
- **Investments.** Holdings, value, gain on cost and contributions against growth, read from a local FinBellTower instance (a separate project). The last good snapshot is kept and shown as stale if FinBellTower is unreachable.
- **Assets.** Vehicles, property, collectibles and electronics at cost and current value; Magic: The Gathering collections can be valued from EchoMTG.
- **Shared expenses** with per-participant settlement status.
- **Monthly reports.** A PDF digest of income, expenses, budgets and net worth change, sent by email.
- **Agent API.** A bearer-token REST API so external AI agents and scripts can read and write the ledger, plus a machine-readable API manual designed to be pasted into an agent's system prompt.
- **Security and housekeeping.** Password login with TOTP two-factor authentication, encrypted storage for third-party credentials, an audit log, backup and restore, and an in-app changelog.
- **Installable PWA** with a layout for phone and tablet.

## Tech stack

Python · FastAPI · SQLAlchemy 2 · Alembic · SQLite · React 18 · Vite · Ollama · OpenRouter · GoCardless Bank Account Data · SMTP / Mailgun · Docker or systemd + nginx

## How it works

```
bank exports / Revolut / GoCardless ──> import + matching ──> SQLite ledger
                                          (transfers, cards,      │
                                           loans, recurring)      │
FinBellTower (local, read-only) ──> investment snapshot ─────────┤
                                                                  v
                         React PWA  <──  FastAPI  ──>  Agent API, AI chat, advisor,
                                                        monthly PDF report
```

The backend is a FastAPI service over a SQLite database, and the frontend is a React app served as a PWA. A scheduler heartbeat runs the periodic checks: budget alerts, recurring-payment matching, milestones and the investment refresh. Settings can come from the environment or be changed in the UI, where stored values take precedence.

## Availability

The source code is not public. LedgerMind is available for licensing, custom deployment or white-label adaptation. Get in touch via [munda.si](https://www.munda.si/#contact).

## License

Proprietary. © 2026 MUNDA PLUS d.o.o. All rights reserved. See [LICENSE](LICENSE).

## Author

Built by [Marko Munda](https://www.munda.si/) · [Munda Plus](https://github.com/MundaPlus)
