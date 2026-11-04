# RetailHub – User Stories and Acceptance Criteria

**Project:** Retail Order System QA Suite  
**Business Model:** Buy Online, Pick Up In Store (BOPIS)  
**Document:** User Stories  
**Version:** 1.0  
**Author:** Mohammad Mahir Shekh  
**Date:** November 3, 2026  
**Status:** Initial Draft

---

## 1. Introduction

This document defines the user stories and acceptance criteria for the RetailHub BOPIS system.

Each user story describes a business capability from the perspective of a system user. Acceptance criteria define the expected system behavior and provide a foundation for functional testing.

The user stories are mapped to the corresponding business requirements in `BRD.md` to maintain requirements traceability.

## 2. User Stories

### US-01 (REQ-01): Place Pickup Order

**As a** customer,  
**I want to** place an order for pickup at my selected store,  
**So that** I can purchase products online and collect them without waiting for shipping.

**Acceptance Criteria**

1. Given that all requested products are in stock, when the customer submits a valid pickup order, then the system creates an order with status `Pending`.
2. Given that the customer has not selected a pickup store, when they attempt to submit an order, then the system displays a validation message and prevents submission.
3. Given that the customer provides valid order information, when the order is successfully created, then the confirmation displays a unique order ID and selected store location.
4. Given that an order submission fails, when the system processes the request, then no incomplete or duplicate order should be created.
5. Given that the customer submits an order with invalid or missing required information, when they attempt checkout, then the system displays appropriate validation messages.

**Priority:** Must  
**Requirement Reference:** REQ-01

---

### US-02 (REQ-02): Reserve Inventory

**As a** customer,  
**I want** available inventory to be reserved when my pickup order is successfully placed,  
**So that** the products I order remain available for my collection.

**Acceptance Criteria**

1. Given that a product has 10 available units, when a customer successfully orders 3 units, then the available inventory decreases to 7.
2. Given that an order contains multiple products, when the order is successfully placed, then inventory is reserved for every ordered product.
3. Given that an order submission fails, when the reservation process is unsuccessful, then inventory remains unchanged.
4. Given that two customers attempt to purchase the last available unit simultaneously, when both orders are submitted, then only one order can successfully reserve that unit.
5. Given that an order is cancelled before Ready for Pickup, when cancellation is successful, then the reserved inventory is released back to available stock.

**Priority:** Must  
**Requirement Reference:** REQ-02

---

### US-03 (REQ-03): Prevent Out-of-Stock Orders

**As a** customer,  
**I want** the system to prevent orders for unavailable products,  
**So that** I do not purchase items that cannot be fulfilled by my selected store.

**Acceptance Criteria**

1. Given that a product has zero available inventory, when a customer attempts to order it, then the system rejects the order.
2. Given that a customer requests 5 units but only 3 are available, when they submit the order, then the system prevents the order from being placed.
3. Given that a product is out of stock, when the customer views its availability, then the system displays an out-of-stock message.
4. Given that inventory changes between product selection and checkout, when the customer submits the order, then the system revalidates stock availability before confirming the order.
5. Given that an order contains multiple products and one product is unavailable, when the customer submits the order, then the system does not create a partially fulfilled order.

**Priority:** Must  
**Requirement Reference:** REQ-03

---

### US-04 (REQ-04): View Pending Pickup Orders

**As a** store associate,  
**I want to** view pending pickup orders in a centralized order queue,  
**So that** I can identify and prepare customer orders efficiently.

**Acceptance Criteria**

1. Given that an order has been successfully placed, when an authorized associate opens the order queue, then the order appears with its order ID and status.
2. Given that multiple pickup orders exist, when the associate views the queue, then all eligible pending orders are displayed.
3. Given that an order is cancelled, when the associate refreshes the order queue, then the cancelled order is no longer displayed as an active pending order.
4. Given that an unauthorized user attempts to access the associate order queue, when they request access, then the system denies access.
5. Given that an order has already been picked up, when the associate views pending orders, then the completed order is not displayed as pending.

**Priority:** Must  
**Requirement Reference:** REQ-04

---

### US-05 (REQ-05): Mark Order Ready for Pickup

**As a** store associate,  
**I want to** update an order's status to Ready for Pickup after preparing the products,  
**So that** the customer knows when to collect their order.

**Acceptance Criteria**

1. Given that an order is in the Preparing status, when the associate confirms that all products are ready, then the system updates the order status to `Ready for Pickup`.
2. Given that an order becomes Ready for Pickup, when the status update succeeds, then the customer receives a simulated pickup notification.
3. Given that an order has been cancelled, when an associate attempts to mark it Ready for Pickup, then the system rejects the status change.
4. Given that an order is already Ready for Pickup, when an associate attempts to repeat the same status update, then the system handles the duplicate request without creating an inconsistent order state.
5. Given that an unauthorized user attempts to update an order status, when the request is submitted, then the system rejects the action.

**Priority:** Must  
**Requirement Reference:** REQ-05

---

### US-06 (REQ-06): Calculate Order Total

**As a** customer,  
**I want** the system to calculate my order total accurately, including discounts and applicable taxes,  
**So that** I can understand the total value of my purchase before submitting my order.

**Acceptance Criteria**

1. Given that a customer purchases products without discounts, when the order total is calculated, then the system displays the correct subtotal, applicable taxes, and final total.
2. Given that a product has a valid discount, when the customer adds it to the order, then the system applies the correct discount.
3. Given that a discount code is invalid or expired, when the customer applies it, then the system displays an appropriate error and does not apply the discount.
4. Given that an order contains multiple products with different prices, when the total is calculated, then the system correctly adds all line-item amounts.
5. Given that the customer changes product quantities, when the order total is recalculated, then the subtotal, discounts, taxes, and final total are updated correctly.

**Priority:** Must  
**Requirement Reference:** REQ-06

---

### US-07 (REQ-07): Cancel Pickup Order

**As a** customer,  
**I want to** cancel my pickup order before it becomes Ready for Pickup,  
**So that** I can change my mind without collecting an unwanted order.

**Acceptance Criteria**

1. Given that an order is in Pending or Preparing status, when the customer requests cancellation, then the system allows the cancellation.
2. Given that an order is successfully cancelled, when the cancellation is completed, then its status changes to `Cancelled`.
3. Given that an order is cancelled, when the system processes the cancellation, then the reserved inventory is released.
4. Given that an order has already reached Ready for Pickup, when the customer requests cancellation, then the system rejects the cancellation.
5. Given that an order is already cancelled, when the customer submits another cancellation request, then the system handles the duplicate request without changing inventory incorrectly.

**Priority:** Should  
**Requirement Reference:** REQ-07

---

### US-08 (REQ-08): Return Purchased Items

**As a** customer,  
**I want to** return eligible products within 30 calendar days of pickup,  
**So that** I can return products that I no longer need or that do not meet my expectations.

**Acceptance Criteria**

1. Given that an order was successfully picked up within the last 30 calendar days, when the customer requests an eligible return, then the system accepts the return request.
2. Given that an order was picked up more than 30 calendar days ago, when the customer requests a return, then the system rejects the request and displays an eligibility message.
3. Given that an order has not yet been picked up, when the customer requests a return, then the system rejects the return request.
4. Given that a return is successfully processed, when the returned item's condition is recorded, then the system updates the return status and inventory according to the item's condition.
5. Given that a return has already been completed, when the customer submits a duplicate return request for the same item, then the system prevents duplicate processing.

**Priority:** Should  
**Requirement Reference:** REQ-08

---

### US-09 (REQ-09): Log System Errors

**As an** IT support specialist,  
**I want** the system to record application errors with timestamps and associated order IDs where available,  
**So that** I can investigate problems and troubleshoot failed order operations.

**Acceptance Criteria**

1. Given that an application error occurs during an order operation, when the error is generated, then the system records the error with a timestamp.
2. Given that an error is associated with an existing order, when the error is logged, then the log includes the corresponding order ID.
3. Given that an error occurs before an order ID is generated, when the error is logged, then the system records the error without requiring an order ID.
4. Given that multiple errors occur, when IT support reviews the logs, then each error can be distinguished using its timestamp and relevant diagnostic information.
5. Given that an error is logged, when the log entry is stored, then sensitive customer information such as passwords and payment details is not exposed.

**Priority:** Must  
**Requirement Reference:** REQ-09

---

## 3. User Story Summary

| Story ID | User Story | Requirement | Priority |
|---|---|---|---|
| US-01 | Place Pickup Order | REQ-01 | Must |
| US-02 | Reserve Inventory | REQ-02 | Must |
| US-03 | Prevent Out-of-Stock Orders | REQ-03 | Must |
| US-04 | View Pending Orders | REQ-04 | Must |
| US-05 | Mark Order Ready | REQ-05 | Must |
| US-06 | Calculate Order Total | REQ-06 | Must |
| US-07 | Cancel Pickup Order | REQ-07 | Should |
| US-08 | Return Purchased Items | REQ-08 | Should |
| US-09 | Log System Errors | REQ-09 | Must |

**Total User Stories:** 9  
**Must Priority:** 7  
**Should Priority:** 2

## 4. Traceability and QA Usage

The user story IDs will be referenced in future testing documentation.

| QA Artifact | Example Reference |
|---|---|
| User Story | US-01 |
| Test Scenario | TS-US-01-001 |
| Test Case | TC-US-01-001 |
| Defect Report | BUG-US-01-001 |
| Test Execution | US-01 – Pass/Fail |
| Requirements Traceability Matrix | REQ-01 → US-01 → Test Cases |

Each acceptance criterion should be covered by one or more test cases.

Both positive and negative acceptance criteria must be considered during test design.

## 5. Business Rules Requiring Validation

The following business rules should remain consistent throughout implementation and testing:

1. An order starts with the status `Pending` after successful creation.
2. An associate can move an eligible order from `Pending` to `Preparing`.
3. An order can move from `Preparing` to `Ready for Pickup`.
4. An order can be cancelled while it is Pending or Preparing.
5. An order cannot be cancelled through the standard cancellation workflow after it becomes Ready for Pickup.
6. An order can become `Picked Up` only after successful pickup verification.
7. A return can only be requested for an order that has been picked up.
8. The return window is 30 calendar days from the pickup date.
9. Inventory must be reserved and released accurately.
10. Inventory is restored after a return only when the returned product is classified as sellable.

These rules establish the expected business behavior for subsequent testing activities.

---

**End of Document**
