# 5. Test Scenarios

## Test Approach
Test scenarios are designed to validate core fraud review workflows in the MVP.
Scenarios cover positive, negative, and edge cases for critical user actions.

---

## Positive Test Scenarios

### TS-01: View Suspicious Transaction Queue
- Given the fraud analyst is logged in
- When suspicious transactions exist
- Then the system displays a prioritized transaction queue

Expected Result:
- Transactions are ordered by risk level
- SLA timers are visible for each transaction

---

### TS-02: Review Transaction Details
- Given a transaction is selected from the queue
- When the analyst opens the review screen
- Then all transaction and customer details are displayed on a single screen

Expected Result:
- No missing or inconsistent data is shown

---

### TS-03: Approve Transaction
- Given a transaction is under review
- When the analyst selects "Approve" and submits a decision reason
- Then the transaction status is updated to "Approved"

Expected Result:
- Decision reason and review time are saved

---

### TS-04: Escalate Transaction
- Given a transaction requires further investigation
- When the analyst selects "Escalate"
- Then the transaction appears in the escalation queue

Expected Result:
- Escalation reason is recorded

---

## Negative Test Scenarios

### TS-05: Submit Decision Without Reason
- Given a transaction is under review
- When the analyst attempts to submit a decision without a reason
- Then the system prevents submission and shows an error message

Expected Result:
- Decision cannot be saved without a reason

---

### TS-06: Access Unauthorized Transaction
- Given a user without fraud analyst role
- When the user attempts to access the fraud review screens
- Then access is denied

Expected Result:
- Authorization error is displayed

---

## Edge Case Scenarios

### TS-07: SLA Breach
- Given a transaction has exceeded the defined SLA
- When the analyst views the transaction
- Then the system highlights the SLA breach

Expected Result:
- SLA breach indicator is visible

---

### TS-08: High Volume Queue Load
- Given a large number of suspicious transactions exist
- When the queue is loaded
- Then the system displays the queue without performance degradation

Expected Result:
- Queue loads within acceptable response time

---

### TS-09: Concurrent Review Attempt
- Given two analysts attempt to review the same transaction
- When one analyst opens the transaction
- Then the transaction is locked for other analysts

Expected Result:
- Only one analyst can review the transaction at a time
