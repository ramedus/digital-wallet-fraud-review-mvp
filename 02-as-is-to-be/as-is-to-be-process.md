# 2. AS-IS / TO-BE Fraud Review Process

## AS-IS (Current State)

### Background
Fraud review activities are handled manually by fraud analysts using multiple disconnected tools.
As transaction volume increases, this approach becomes difficult to scale and manage.

### AS-IS Process Flow
1. Transactions are flagged as suspicious by rule-based monitoring systems.
2. Suspicious transactions are shared with fraud teams via email, spreadsheets, or internal ticketing tools.
3. Fraud analysts pick transactions to review without a standardized prioritization logic.
4. Transaction and customer details are collected manually from multiple systems.
5. Fraud decisions are recorded inconsistently or outside a centralized system.
6. Review duration and SLA compliance are not tracked systematically.
7. Decision history and investigation reasons are difficult to access for audits or reporting.

### Key Issues in AS-IS
- No centralized fraud review queue
- Lack of clear prioritization for high-risk transactions
- Missing SLA definitions and tracking
- Inconsistent documentation of fraud decisions
- Limited visibility into analyst workload and performance

---

## TO-BE (Target State – MVP)

### TO-BE Process Flow
1. All suspicious transactions are routed to a centralized Fraud Review Queue.
2. Transactions are automatically prioritized based on risk level, transaction amount, and transaction type.
3. Fraud analysts review transactions in priority order through a single interface.
4. All required transaction and customer information is available on a single review screen.
5. Fraud analysts take one of the following actions:
   - Approve
   - Block
   - Escalate
6. Each decision is logged with a decision reason and review duration.
7. SLA timers start automatically when a transaction enters the review queue.
8. Basic operational and performance reports are generated for fraud and management teams.

### Expected Outcomes
- Faster handling of high-risk suspicious transactions
- Reduced fraud decision turnaround time
- Standardized and auditable fraud review workflow
- Improved productivity and efficiency of fraud analysts
- Clear visibility into fraud operations and performance
