# 4. Wireframes & Screen Flow

## Overview
This section outlines the key screens required for the Fraud Review MVP.
The goal is to support fraud analysts with a clear, efficient, and consistent review experience.

---

## Screen 1: Suspicious Transaction Queue

### Purpose
To provide fraud analysts with a centralized and prioritized list of suspicious transactions.

### Key Elements
- Transaction ID
- Transaction amount
- Risk level (Low / Medium / High)
- Transaction type
- Queue status (New / In Review / Escalated)
- SLA timer (time since flagged)

### User Actions
- Sort transactions by risk or amount
- Select a transaction to review
- Filter transactions by status

### Notes
- Transactions are ordered by risk level by default.
- High-risk transactions are visually highlighted.

---

## Screen 2: Transaction Review Screen

### Purpose
To allow fraud analysts to review transaction details and make a decision.

### Key Elements
- Transaction details (amount, date, type)
- Customer information (masked where required)
- Risk indicators and rule triggers
- Review status
- SLA countdown timer

### User Actions
- Approve transaction
- Block transaction
- Escalate transaction
- Add decision reason

### Notes
- All required data is visible on a single screen.
- Decision actions are disabled once a final decision is submitted.

---

## Screen 3: Escalation Queue

### Purpose
To manage complex or high-risk transactions escalated by analysts.

### Key Elements
- List of escalated transactions
- Original analyst notes
- Escalation reason
- Current status

### User Actions
- Review escalated case
- Take final decision
- Add additional notes

---

## Screen 4: Fraud Performance Dashboard

### Purpose
To provide operational visibility into fraud review performance.

### Key Elements
- Average fraud decision time
- Number of reviewed transactions
- SLA compliance rate
- Escalated transaction count

### User Actions
- Filter metrics by date range
- Refresh dashboard data

### Notes
- Dashboard includes only basic metrics in MVP scope.
