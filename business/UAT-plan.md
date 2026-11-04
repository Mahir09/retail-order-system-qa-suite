# RetailHub – User Acceptance Testing (UAT) Plan

## 1. Document Information

| Field | Details |
|---|---|
| Document Title | RetailHub User Acceptance Testing Plan |
| Project Name | Retail Order System QA Suite |
| Document Version | 1.0 |
| Author | Mohammad Mahir Shekh |
| Date | November 4, 2026 |
| Document Status | Initial Draft |
| Testing Type | User Acceptance Testing (UAT) |
| Business Process | Buy Online, Pick Up In Store (BOPIS) |

---

## 2. Objective and Scope

### 2.1 Objective

The objective of User Acceptance Testing (UAT) is to verify that the RetailHub BOPIS system meets the defined business requirements and supports the expected retail order fulfillment processes.

UAT will involve simulated business users validating the system from their respective operational perspectives.

The testing will focus on ensuring that customers can successfully place pickup orders, inventory is reserved accurately, associates can prepare and fulfill orders, and cancellation and return processes work according to business policies.

### 2.2 UAT Scope

The following business capabilities will be validated:

1. Customer pickup order creation.
2. Store-level inventory availability.
3. Inventory reservation and accuracy.
4. Prevention of out-of-stock orders.
5. Associate access to pending pickup orders.
6. Order preparation and status updates.
7. Ready for Pickup notifications.
8. Order total and discount calculations.
9. Customer order cancellation.
10. Product return eligibility and processing.
11. Error logging and order traceability.
12. Role-based access to associate functionality.

### 2.3 Out of Scope

- Real payment gateway processing.
- Actual financial refunds.
- Shipping and home delivery.
- Loyalty points and rewards.
- Native mobile application testing.
- Third-party courier integrations.
- Production deployment validation.

---

## 3. UAT Participants and Roles

| Participant | Role | Responsibilities |
|---|---|---|
| Store Associate | Business User | Validate order visibility, preparation, status updates and customer pickup. |
| Store Manager | Business Representative | Validate operational workflows, order accuracy and fulfillment processes. |
| Business Owner | Business Approver | Confirm that the solution meets business objectives and requirements. |
| QA Lead | Test Coordinator | Prepare UAT scenarios, coordinate execution, manage defects and report results. |

### 3.1 Responsibilities

**Store Associate**
- Verify incoming pickup orders.
- Prepare customer orders.
- Update order statuses.
- Complete customer pickup workflows.

**Store Manager**
- Review order processing activities.
- Validate operational accuracy.
- Confirm that workflows support store operations.

**Business Owner**
- Review business requirements.
- Evaluate UAT outcomes.
- Approve, conditionally approve or reject the solution.

**QA Lead**
- Coordinate UAT activities.
- Maintain test documentation.
- Record and prioritize defects.
- Organize defect triage meetings.
- Prepare the final UAT summary.

---

## 4. UAT Entry Criteria

UAT can begin when all the following conditions are satisfied:

1. All Must-priority functional requirements have been implemented.
2. Functional system testing has been completed.
3. No open Critical severity defects remain.
4. The UAT environment is accessible and stable.
5. Required test accounts and user permissions are configured.
6. Test data and inventory records are prepared.
7. UAT scenarios and expected results have been reviewed.
8. Business representatives are available to participate in testing.

If any entry criterion is not satisfied, the QA Lead must assess the impact and determine whether UAT should be delayed.

---

## 5. UAT Exit Criteria

UAT will be considered complete when the following conditions are satisfied:

1. 100% of Must-priority UAT scenarios have been executed.
2. All Must-priority UAT scenarios have passed.
3. No open Critical or High severity defects remain.
4. Failed scenarios have been investigated and retested after fixes.
5. All identified defects have been documented and assigned an appropriate status.
6. UAT execution results have been recorded.
7. Business stakeholders have reviewed the final results.
8. The Business Owner has provided formal sign-off.

Should-priority scenarios must also be executed and their results documented. Any outstanding failures must be reviewed and accepted explicitly by the Business Owner before sign-off.

---

## 6. Test Environment and Test Data

### 6.1 Test Environment

| Environment Component | Configuration |
|---|---|
| Environment | Dedicated UAT environment |
| Customer Interface | Web browser |
| Associate Interface | Internal order management web interface |
| Operating System | Windows 11 |
| Browser | Google Chrome |
| Database | Simulated retail product and inventory database |
| Payment Integration | Mock payment service |
| Notifications | Simulated email/SMS notifications |
| Test Access | Customer, Associate, Manager and IT Support accounts |

The environment will use simulated data and services rather than production retail systems.

### 6.2 Test Data

The following sample data will be prepared for UAT execution.

| Test Data ID | Product | Available Stock | Unit Price |
|---|---|---:|---:|
| PROD-001 | Wireless Mouse | 10 | $25.00 |
| PROD-002 | Keyboard | 5 | $45.00 |
| PROD-003 | USB-C Cable | 0 | $15.00 |
| PROD-004 | Monitor | 3 | $199.99 |
| PROD-005 | Headphones | 20 | $79.99 |

Additional test data:

| Data Type | Sample Value |
|---|---|
| Pickup Store | RetailHub Toronto |
| Customer Account | customer_test |
| Associate Account | associate_test |
| Manager Account | manager_test |
| Business Owner Account | owner_test |
| IT Support Account | support_test |
| Valid Discount | SAVE10 |
| Invalid Discount | INVALID10 |
| Expired Discount | EXPIRED10 |
| Return Window | 30 calendar days |
| Currency | CAD |

All test accounts and sample products are fictional.

### 6.3 Test Data Preparation

- Ensure product inventory matches the initial test data.
- Create customer and employee test accounts.
- Prepare orders in different lifecycle statuses.
- Prepare valid, invalid and expired discount codes.
- Prepare historical pickup orders for return testing.
- Ensure that inventory can be reset between test executions.

---

## 7. UAT Test Scenarios

The following scenarios represent the business acceptance tests planned for RetailHub.

| ID | Scenario | Linked Story | Expected Result | Priority |
|---|---|---|---|---|
| UAT-01 | Associate views pending pickup orders | US-04 | All eligible Pending orders are listed. | Must |
| UAT-02 | Customer orders an out-of-stock item | US-03 | Order is rejected with a clear availability message. | Must |
| UAT-03 | Customer places a valid pickup order | US-01 | Order is created with a unique ID and Pending status. | Must |
| UAT-04 | Inventory is reserved after order placement | US-02 | Available stock decreases by the ordered quantity. | Must |
| UAT-05 | Associate prepares a pickup order | US-05 | Associate can update an eligible order to Ready for Pickup after preparation. | Must |
| UAT-06 | Customer receives pickup notification | US-05 | Simulated notification is generated when order becomes ready. | Must |
| UAT-07 | Customer views incorrect or expired discount | US-06 | Invalid discount is rejected and the order total remains correct. | Must |
| UAT-08 | Customer cancels an eligible order | US-07 | Order is cancelled and reserved inventory is released. | Should |
| UAT-09 | Customer attempts to cancel a ready order | US-07 | Cancellation is rejected. | Should |
| UAT-10 | Customer returns an eligible product | US-08 | Return is accepted and return status is recorded. | Should |
| UAT-11 | Customer attempts a return after 30 days | US-08 | Return request is rejected with an eligibility message. | Should |
| UAT-12 | IT Support reviews application error logs | US-09 | Error logs contain timestamps and order IDs where available. | Must |

### 7.1 Scenario Execution Rules

Each scenario will be assigned one of the following execution statuses:

| Status | Meaning |
|---|---|
| Not Run | Testing has not started. |
| Pass | Actual result matches expected result. |
| Fail | Actual result does not match expected result. |
| Blocked | Testing cannot continue because of an external dependency or environment issue. |
| Not Applicable | Scenario is excluded with documented justification and approval. |

A failed scenario must be associated with a defect ID where applicable.

### 7.2 UAT Execution Record Template

| Field | Details |
|---|---|
| UAT Scenario ID | UAT-XX |
| Executed By | Tester Name |
| Execution Date | YYYY-MM-DD |
| Expected Result | Defined expected outcome |
| Actual Result | Observed system behavior |
| Status | Pass / Fail / Blocked |
| Defect ID | BUG-XXX, if applicable |
| Comments | Additional observations |

---

## 8. Defect Handling Process

### 8.1 Defect Management Workflow

1. Tester executes a UAT scenario.
2. Tester identifies behavior that differs from the expected result.
3. Tester records the defect with reproduction steps and supporting evidence.
4. QA Lead reviews and assigns initial severity and priority.
5. Defect is discussed during defect triage.
6. Development team investigates and implements a fix.
7. QA retests the affected functionality.
8. Business representative performs additional validation when required.
9. Defect is closed after successful verification.

### 8.2 Defect Severity Definitions

| Severity | Definition | Example |
|---|---|---|
| Critical | Complete system failure or major business operation unavailable. | Customers cannot place any pickup orders. |
| High | Major functionality is broken with significant business impact. | Inventory is not reserved and multiple customers can purchase the same stock. |
| Medium | Functionality is partially affected, but a workaround exists. | Order notification is delayed while the order remains accessible. |
| Low | Minor issue with limited business impact. | Incorrect wording or minor formatting issue. |

### 8.3 Defect Priority

| Priority | Definition |
|---|---|
| P1 – Urgent | Requires immediate attention and resolution. |
| P2 – High | Should be resolved before UAT sign-off. |
| P3 – Medium | Can be scheduled for a subsequent release if approved. |
| P4 – Low | Minor improvement or cosmetic correction. |

Severity describes the impact of a defect. Priority describes how urgently it should be addressed.

### 8.4 Defect Triage Responsibilities

| Role | Responsibility |
|---|---|
| Tester | Reports defects with evidence and reproduction steps. |
| QA Lead | Reviews, classifies and coordinates defect triage. |
| Development Team | Investigates and fixes reported defects. |
| Store Manager | Evaluates operational impact. |
| Business Owner | Accepts or rejects outstanding business risks. |

No Critical or High severity defect should remain unresolved at final UAT sign-off.

---

## 9. UAT Sign-Off

### 9.1 Sign-Off Conditions

The Business Owner will review:

- UAT execution results.
- Must-priority requirement coverage.
- Outstanding defects.
- Failed and blocked scenarios.
- Business risks and proposed workarounds.
- Overall system readiness.

### 9.2 Sign-Off Template

| Field | Details |
|---|---|
| Project Name | RetailHub BOPIS |
| UAT Completion Date | YYYY-MM-DD |
| Participant Name | |
| Role | |
| UAT Scenarios Executed | |
| Passed Scenarios | |
| Failed Scenarios | |
| Outstanding Defects | |

### 9.3 Acceptance Decision

Select one:

- [ ] Approved – System meets the defined business acceptance criteria.
- [ ] Approved with Conditions – System is accepted subject to documented outstanding items and agreed actions.
- [ ] Rejected – System does not meet the required business acceptance criteria.

### 9.4 Outstanding Conditions / Comments

Document any outstanding defects, business risks, workarounds or required follow-up actions.

| Item | Description | Owner | Target Resolution Date |
|---|---|---|---|
| 1 | | | |
| 2 | | | |

### 9.5 Formal Approval

| Approval Role | Name | Signature / Approval | Date |
|---|---|---|---|
| Business Owner | | | |
| Store Manager | | | |
| QA Lead | | | |

---

## 10. UAT Deliverables

The following deliverables will be maintained as part of the UAT process:

1. Approved UAT Plan.
2. UAT Test Scenario List.
3. UAT Execution Results.
4. Defect Reports.
5. Defect Summary.
6. UAT Completion Report.
7. Business Acceptance Sign-Off.

---

## 11. Document Approval

This document defines the planned User Acceptance Testing approach for the RetailHub BOPIS system.

All UAT activities will be conducted against the approved business requirements and user stories.

**Document Version:** 1.0  
**Document Status:** Initial Draft  
**Prepared By:** Mohammad Mahir Shekh  
**Approval Status:** Pending Review

---

**End of Document**
