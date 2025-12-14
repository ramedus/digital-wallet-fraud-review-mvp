# 6. Data Model & API Design

## Data Model Overview

This section describes the core data entities and API design for the **Suspicious Transaction & Fraud Review MVP**
in digital wallets.

The purpose of this data model is to:
- Support centralized fraud investigation workflows
- Enable traceable and auditable fraud decisions
- Measure SLA compliance and operational performance

---

## Core Entities

### User
Represents system users who perform fraud reviews.

Fields:
- user_id (PK)
- name
- email
- role (Fraud Analyst, Senior Analyst, Admin)
- created_at

A user can review multiple suspicious transactions.

---

### Wallet
Represents a digital wallet account.

Fields:
- wallet_id (PK)
- user_id (FK)
- status (Active, Suspended)
- created_at

A wallet can have multiple transactions.

---

### Transaction
Represents financial transactions performed through wallets.

Fields:
- transaction_id (PK)
- wallet_id (FK)
- amount
- currency
- transaction_type (Transfer, Payment, Top-up)
- country
- channel (Mobile, Web, API)
- transaction_date

A transaction may be flagged as suspicious.

---

### SuspiciousTransaction
Represents transactions that require manual fraud investigation.

Fields:
- suspicious_id (PK)
- transaction_id (FK)
- risk_score
- risk_reason
- status (New, In Review, Approved, Blocked, Escalated)
- sla_deadline
- created_at

Each suspicious transaction is linked to exactly one transaction.

---

### FraudDecision
Stores fraud investigation decisions made by analysts.

Fields:
- decision_id (PK)
- suspicious_id (FK)
- analyst_id (FK → User)
- decision (Approve, Block, Escalate)
- decision_reason
- decision_time
- created_at

A suspicious transaction may have multiple decisions in escalation scenarios.

---

## Entity Relationship Summary

- User → FraudDecision (1:N)
- Wallet → Transaction (1:N)
- Transaction → SuspiciousTransaction (1:1)
- SuspiciousTransaction → FraudDecision (1:N)

This structure enables full traceability of fraud investigations and decisions.

---

## API Design (MVP Scope)

The following API endpoints support the core fraud review flow in the MVP.

---

### Get Suspicious Transaction Queue
**GET** `/suspicious-transactions`

**Purpose:** Returns a prioritized list of suspicious transactions for fraud analysts.

**Example Response:**
```json
{
  "suspicious_id": "st_123",
  "transaction_id": "tx_789",
  "amount": 2500,
  "currency": "TRY",
  "risk_score": 92,
  "status": "NEW",
  "sla_deadline": "2025-09-10T12:00:00Z"
}

...

### Get Suspicious Transaction Details
**GET** `/suspicious-transactions/{id}`

**Purpose:**  
Returns detailed information for a selected suspicious transaction.

---

### Submit Fraud Decision
**POST** `/fraud-decisions`

**Purpose:**  
Stores the fraud analyst’s decision and reasoning.

**Example Request:**
```json
{
  "suspicious_id": "st_123",
  "analyst_id": "u_456",
  "decision": "BLOCK",
  "decision_reason": "Unusual country and high transaction amount"
}

**Example Response:**
```json
{
  "decision_id": "fd_101",
  "status": "BLOCKED",
  "message": "Fraud decision successfully recorded."
}

---

### Get SLA Violations Report
**GET** `/reports/sla-violations`

**Purpose:**  
Returns a list of suspicious transactions that exceeded defined SLA thresholds.

**Description:**  
This endpoint is used for operational monitoring and reporting.  
It helps identify bottlenecks in fraud review processes and measure SLA compliance.

**Example Response:**
```json
{
  "report_generated_at": "2025-09-11T10:30:00Z",
  "total_violations": 2,
  "violations": [
    {
      "suspicious_id": "st_201",
      "transaction_id": "tx_901",
      "risk_score": 88,
      "status": "IN_REVIEW",
      "sla_deadline": "2025-09-10T12:00:00Z",
      "actual_decision_time": "2025-09-10T15:45:00Z",
      "sla_breached_by_minutes": 225
    },
    {
      "suspicious_id": "st_202",
      "transaction_id": "tx_902",
      "risk_score": 95,
      "status": "NEW",
      "sla_deadline": "2025-09-10T14:00:00Z",
      "actual_decision_time": null,
      "sla_breached_by_minutes": 180
    }
  ]
}

