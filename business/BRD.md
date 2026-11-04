# RetailHub – Business Requirements Document (BRD)

## 1. Document Information

| Field | Details |
|---|---|
| Document Title | RetailHub Business Requirements Document |
| Project Name | Retail Order System QA Suite |
| Version | 1.0 |
| Author | Mohammad Mahir Shekh |
| Date | November 3, 2026 |
| Document Status | Initial Draft |
| Business Process | Buy Online, Pick Up In Store (BOPIS) |

---

## 2. Purpose and Background

RetailHub is a fictional retail company planning to introduce a Buy Online, Pick Up In Store (BOPIS) solution.

The purpose of this project is to develop and validate a retail order management system that allows customers to check store-level inventory, place online pickup orders, and collect products from their selected store. Store associates will use an internal interface to view, prepare, and manage customer orders.

This document defines the business requirements, project boundaries, operational expectations, and quality objectives that will guide the development and testing of the proposed system.

## 3. Business Problem and Goals

### 3.1 Business Problem

The current retail process has several operational challenges:

- Customers cannot reliably determine product availability at individual stores.
- Customers lack visibility into pickup order preparation and status.
- Store associates do not have a centralized order preparation queue.
- Inventory discrepancies can result in orders being placed for unavailable products.
- Store managers have limited visibility into pickup operations.

### 3.2 Business Goals

The proposed system aims to:

1. Improve customer visibility into store-level product availability.
2. Enable customers to place convenient online pickup orders.
3. Prevent inventory overselling through inventory reservation.
4. Improve associate productivity through centralized order management.
5. Reduce customer pickup waiting times.
6. Provide accurate order status tracking.
7. Support consistent order cancellation and return processes.

## 4. Project Scope

### 4.1 In Scope

The following capabilities are included:

- Product selection and pickup store selection.
- Store-level inventory availability checks.
- Online pickup order creation.
- Inventory reservation after successful order placement.
- Order total calculation, including discounts and taxes.
- Associate order queue and order preparation.
- Order status updates.
- Ready for Pickup notifications.
- Customer pickup verification.
- Order cancellation before Ready for Pickup.
- Eligible product returns within 30 calendar days of pickup.
- Error logging and order tracking.

### 4.2 Out of Scope

The following capabilities are excluded:

- Real payment gateway integration.
- Actual financial transactions and refunds.
- Home delivery and shipping.
- Loyalty points and rewards.
- Native Android and iOS applications.
- Multi-store order fulfillment.
- Third-party courier integration.
- Integration with external ERP or POS platforms.

## 5. Stakeholders

| Stakeholder | Role and Responsibilities | Primary Concern |
|---|---|---|
| Customer | Places, tracks, cancels and collects orders | Accurate inventory and convenient pickup |
| Store Associate | Views, prepares and completes orders | Clear order queue and simple workflows |
| Store Manager | Oversees pickup operations | Operational efficiency and performance |
| Inventory Team | Maintains product inventory | Inventory accuracy and reservation |
| IT Support | Supports system operations | System reliability, errors and troubleshooting |

## 6. Assumptions and Constraints

### 6.1 Assumptions

1. Customers must select a participating store before placing an order.
2. Products must have sufficient available inventory to be ordered.
3. Inventory reservations occur when an order is successfully created.
4. Store associates have authorized access to the internal order management interface.
5. Customers receive simulated notifications when their orders become ready.
6. Order cancellations are permitted before the Ready for Pickup status.
7. Returns are permitted within 30 calendar days of successful pickup, subject to eligibility.
8. Returned products may be classified as sellable or non-sellable.

### 6.2 Constraints

1. Payment processing will be simulated; no real financial transactions will occur.
2. The initial implementation supports one selected pickup store per order.
3. The system will use a predefined product and inventory dataset.
4. The project will be developed as a QA portfolio demonstration rather than a production retail platform.
5. Email and SMS notifications will be simulated.
6. Refund calculations and payment reversals will not connect to actual payment providers.

## 7. Business Requirements

The following requirements define the expected functional behavior of the RetailHub system.

| ID | Requirement | Priority |
|---|---|---|
| REQ-01 | The system shall allow a customer to place a pickup order for in-stock items. | Must |
| REQ-02 | The system shall reserve the requested inventory when an order is successfully placed. | Must |
| REQ-03 | The system shall prevent orders for unavailable or out-of-stock items. | Must |
| REQ-04 | The system shall allow authorized store associates to view pending pickup orders. | Must |
| REQ-05 | The system shall allow associates to mark eligible orders as Ready for Pickup. | Must |
| REQ-06 | The system shall calculate the correct order total, including discounts and applicable taxes. | Must |
| REQ-07 | The system shall allow customers to cancel eligible orders before they become Ready for Pickup. | Should |
| REQ-08 | The system shall support eligible product returns within 30 calendar days of pickup. | Should |
| REQ-09 | The system shall log system errors with a timestamp and associated order ID, where available. | Must |

### 7.1 Requirement Acceptance Criteria

| Requirement ID | Acceptance Criteria |
|---|---|
| REQ-01 | A customer can successfully create an order containing available products and select a pickup store. |
| REQ-02 | Available inventory decreases by the ordered quantity after successful order creation. |
| REQ-03 | The system rejects orders when requested quantities exceed available inventory. |
| REQ-04 | Authorized associates can access and view orders awaiting preparation. |
| REQ-05 | An associate can update an eligible order to Ready for Pickup, and the updated status is visible to the customer. |
| REQ-06 | Order subtotal, discounts, taxes and final total are calculated correctly. |
| REQ-07 | An eligible order can be cancelled before Ready for Pickup, and reserved inventory is released. |
| REQ-08 | Eligible orders can be returned within 30 calendar days of pickup, and return status is recorded. |
| REQ-09 | Application errors are recorded with timestamps and order IDs when available. |

## 8. Non-Functional Requirements

Non-functional requirements define how the system should perform rather than which business functions it provides.

| ID | Category | Requirement | Target |
|---|---|---|---|
| NFR-01 | Performance | Product availability searches should return results within an acceptable time. | Within 2 seconds under normal test load |
| NFR-02 | Performance | Order submission should complete within an acceptable time. | Within 3 seconds under normal test load |
| NFR-03 | Reliability | The system should prevent inventory overselling during concurrent order attempts. | No duplicate reservation of the same stock |
| NFR-04 | Data Accuracy | Inventory quantities and order statuses must remain consistent. | 100% consistency in defined test scenarios |
| NFR-05 | Security | Only authorized associates should access internal order management functions. | Unauthorized access must be rejected |
| NFR-06 | Logging | System errors should be recorded with relevant diagnostic information. | Timestamp and order ID where available |
| NFR-07 | Usability | Customers should be able to complete the pickup ordering workflow without unnecessary complexity. | Successful completion of defined usability tests |
| NFR-08 | Availability | The demonstration system should remain accessible during planned testing. | Proposed target of 99% during scheduled test windows |

Performance targets are proposed portfolio acceptance thresholds and will be validated through testing.

## 9. Business Risks

| Risk ID | Risk Description | Potential Impact | Mitigation |
|---|---|---|---|
| RISK-01 | Inventory data becomes out of sync with actual store stock. | Customers order unavailable products. | Validate inventory during order submission and reservation. |
| RISK-02 | Multiple customers attempt to purchase the same remaining stock. | Inventory overselling. | Use atomic inventory reservation and concurrency testing. |
| RISK-03 | Associates fail to update order statuses. | Customers experience unnecessary waiting. | Provide clear status workflows and validation. |
| RISK-04 | Customer receives incorrect order notifications. | Customer confusion and failed pickups. | Validate notification triggers and order references. |
| RISK-05 | Incorrect tax or discount calculations. | Incorrect customer order totals. | Implement calculation validation and boundary testing. |
| RISK-06 | Unauthorized users access customer orders. | Exposure of customer information. | Enforce authentication and role-based authorization. |
| RISK-07 | Cancelled orders do not release reserved inventory. | Incorrect inventory availability. | Validate inventory restoration during cancellation. |
| RISK-08 | Return requests are accepted outside the permitted period. | Business policy violations. | Validate return eligibility using pickup date. |

## 10. Success Metrics

The following metrics will be used to evaluate the system against the proposed business objectives.

| Metric | Target | Measurement |
|---|---|---|
| Average customer pickup waiting time | Under 5 minutes | Time between customer arrival and order handover |
| Out-of-stock order cancellations | Below 2% | Out-of-stock cancellations divided by total orders |
| Inventory reservation accuracy | At least 99% | Correct reservations divided by reservation attempts |
| Order visibility for associates | Within 1 minute | Time between successful order creation and associate visibility |
| Order status tracking | 100% | Orders with correctly recorded lifecycle statuses |

These are proposed project targets, not measured production results or external industry benchmarks.

## 11. Requirement Traceability

Each business requirement will be referenced throughout the QA lifecycle.

The following documents will use these requirement IDs:

- Test scenarios: Map business requirements to testing scenarios.
- Test cases: Validate individual requirement behaviors.
- Defect reports: Reference the affected requirement ID.
- Test execution reports: Track pass/fail results by requirement.
- Final QA summary: Report requirement coverage and outstanding defects.

## 12. Document Approval

This Business Requirements Document establishes the initial functional and non-functional expectations for the RetailHub BOPIS system.

Changes to business requirements should be documented, reviewed and reflected in the associated testing artifacts.

| Field | Details |
|---|---|
| Prepared By | Mohammad Mahir Shekh |
| Version | 1.0 |
| Status | Initial Draft |
| Approval | Pending Review |

---

**End of Document**
