# RetailHub BOPIS — Manual Test Plan

**Project:** RetailHub Buy Online, Pick Up In Store (BOPIS)  
**Version:** 1.0  
**Author:** Mohammad Mahir Shekh  
**Date:** November 4, 2026  
**Status:** Initial Draft

## 1. Objective

The objective of this test plan is to verify that the RetailHub BOPIS application behaves according to the business requirements documented in the `/business` folder.

Testing will validate the customer order journey, inventory reservation, order processing, pricing calculations, cancellations, returns, and system error logging.

The goal is to identify functional defects, validate negative scenarios, and establish a repeatable regression test suite.

Every test case must trace to at least one existing requirement (`REQ`) or user story (`US`) ID.

## 2. Scope

### In scope

Testing will cover all nine functional requirements:

- **REQ-01:** Place pickup orders for available products.
- **REQ-02:** Reserve inventory after successful order placement.
- **REQ-03:** Prevent orders for unavailable products.
- **REQ-04:** Allow authorized associates to view pending orders.
- **REQ-05:** Update eligible orders to Ready for Pickup.
- **REQ-06:** Calculate order totals, discounts, and applicable taxes.
- **REQ-07:** Cancel eligible orders and release reserved inventory.
- **REQ-08:** Process eligible returns within the 30-calendar-day window.
- **REQ-09:** Log system errors with timestamps and order IDs where available.

### Out of scope

- Real payment gateway processing.
- Performance, load, and stress testing.
- Shipping and home delivery.
- Loyalty points and rewards.
- Native mobile application testing.
- Multi-store fulfillment.

Pricing calculations remain in scope under REQ-06, but actual payment processing is excluded.

## 3. Test Types

| Test type | Purpose |
|---|---|
| Functional | Verify that features work according to requirements. |
| Negative | Verify that invalid actions and inputs are rejected correctly. |
| API | Validate request/response behavior, validation, status codes, and data integrity where APIs are available. |
| Regression | Confirm that existing functionality continues to work after changes. |
| Smoke | Verify that critical application functionality works before deeper testing. |

## 4. Test Approach

**Manual testing:** Exploratory testing and new functionality will initially be tested manually. Testers will follow documented steps, verify expected results, investigate unexpected behavior, and record defects.

**Playwright automation:** Stable, repeatable regression scenarios will be automated using Playwright. Priority will be given to critical customer and associate workflows, including order placement, inventory checks, order status updates, and cancellation.

**API testing:** API tests will validate backend behavior when the application exposes testable endpoints.

Automation will not replace exploratory testing. Tests involving unstable requirements, complex concurrency, or difficult-to-control external dependencies may remain manual until they can be reliably automated.

## 5. Test Environment

The planned test environment is:

| Component | Configuration |
|---|---|
| Application | Local RetailHub development/test application |
| Browser | Chromium |
| Automation | Playwright |
| Operating system | Windows 11 |
| Database | Dedicated test database |
| Test data | Seeded products, customers, associates, and orders |
| Payment | Mock/simulated payment behavior |
| Notifications | Simulated email/SMS notifications |

The environment and data must be reset or isolated between tests when one test could affect another.

The application does not need to be production-ready for test design, but execution requires a functioning test build.

## 6. Entry and Exit Criteria

### Entry criteria

Testing can begin when:

- Required functionality for the test cycle is available.
- System testing has been completed.
- No open Critical defects prevent testing.
- The test environment is stable and accessible.
- Test accounts and permissions are configured.
- Known test data is available.
- Test cases and expected results have been reviewed.

### Exit criteria

Testing can be considered complete when:

- 100% of Must-priority UAT scenarios have been executed.
- All Must-priority scenarios have passed.
- No Critical or High defects remain open.
- Failed and blocked tests have been investigated.
- Defects have been documented and triaged.
- Test execution results have been recorded.
- Business stakeholders have reviewed the results and provided sign-off.

Should-priority scenarios must also have their execution results documented, with unresolved failures explicitly reviewed and accepted by the appropriate stakeholder.

These criteria align with the `/business/UAT-plan.md` document.

## 7. Defect Severity and Priority

Severity describes the impact of a defect. Priority describes how urgently it should be fixed.

| Severity | Definition and example |
|---|---|
| Critical | Complete failure of a critical business workflow; for example, customers cannot place any pickup orders. |
| High | Major functionality is broken; for example, inventory is not reserved and overselling becomes possible. |
| Medium | Functionality is partially affected but a workaround exists; for example, pickup notifications are delayed. |
| Low | Minor cosmetic or usability issue; for example, incorrect spacing or a small wording issue. |

**Priority definitions:**

- **P1 — Urgent:** Must be addressed immediately because it blocks critical business operations.
- **P2 — High:** Should be fixed before the next release or test sign-off.
- **P3 — Medium:** Should be fixed in a planned maintenance or development cycle.
- **P4 — Low:** Can be scheduled for a future improvement.

Severity and priority must be assessed separately. A low-severity cosmetic issue may still have a higher priority if it affects a critical business deadline.

## 8. Risks

| Risk | Potential impact | Mitigation |
|---|---|---|
| Unstable test data | Inconsistent or unreliable results | Use controlled, repeatable seed data. |
| Shared inventory between tests | One test changes another test's expected stock | Reset data or use isolated products and test runs. |
| Environment instability | Tests cannot be completed reliably | Perform smoke checks before execution. |
| Unclear business rules | Different interpretations of expected behavior | Confirm rules with the BRD and UAT plan. |
| Notification service unavailable | Notification scenarios cannot be verified | Use a simulated notification service. |
| Concurrent order activity | Inventory overselling or inconsistent reservations | Include controlled concurrency tests. |

## 9. Deliverables

The QA portfolio project will maintain these deliverables:

- **Test plan:** Defines test objectives, scope, approach, environment, and criteria.
- **Test cases:** Documents test steps, test data, expected results, and traceability.
- **Bug reports:** Records defects with reproduction steps, evidence, severity, and priority.
- **Automation suite:** Contains repeatable Playwright regression tests.
- **Execution report:** Summarizes executed tests, results, defects, and outstanding risks.

All test artifacts must maintain traceability to the requirements and user stories in the `/business` folder.

**End of document**
