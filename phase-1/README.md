# WholeCart – Phase 1

Testing of the WholeCart B2B marketplace against the functional design v1.0 (WC-FDD-1.0-641d).

- **Environment:** QA - http://13.200.185.1/c/purushoth-kumar-efaa03 | Chrome, macOS
- **Accounts:** buyer1 (Spice Route Kitchen), buyer2 (Café Dosa Corner), seller1 (WholeCart Direct), operator
- **Test date:** 14 Oct 2026

## Contents

| File | What it is |
|---|---|
| `WholeCart_TestCases_and_Defects.xlsx` | The workbook, with four sheets: **Summary**, **Testcases**, **Bugs** and **Questions & Assumptions**. |
| `ai-sessions/` | The AI chat sessions used during this assignment (see *Use of AI* below). |
| `evidence/` | One video or screenshot per defect, named by defect ID. Each defect's **Evidence** column links to its file. |

**Summary** shows pass/fail per module, defects by severity and priority, and the key defects.
**Testcases** holds 58 test cases grouped by feature area, each with steps, test data, expected result, actual result, status and priority.
**Questions & Assumptions** lists the questions I would ask the product owner and the assumption I used for each.
**Bugs** holds 22 defects, each with steps to reproduce, test data, expected and actual results, severity, priority, evidence and linked test cases.

## Results

**58 test cases:** 34 passed, 24 failed (59% pass rate).
**22 defects:** 2 critical, 11 major, 6 minor, 3 trivial.

| Module | Test cases | Pass | Fail |
|---|---|---|---|
| Login & Access | 2 | 2 | 0 |
| Catalogue & Search | 2 | 0 | 2 |
| Cart | 3 | 2 | 1 |
| Checkout | 12 | 8 | 4 |
| Delivery Slots | 4 | 4 | 0 |
| Order History | 3 | 1 | 2 |
| Cancellation | 5 | 4 | 1 |
| Slot Change | 2 | 1 | 1 |
| Redelivery | 1 | 1 | 0 |
| Reorder | 2 | 0 | 2 |
| Refunds & Exchanges | 3 | 2 | 1 |
| Invoices | 1 | 0 | 1 |
| Monthly Statements | 3 | 1 | 2 |
| Inquiries | 1 | 0 | 1 |
| Seller - Orders | 4 | 3 | 1 |
| Seller - Products | 1 | 0 | 1 |
| Seller - CSV Import | 3 | 1 | 2 |
| Operator | 6 | 4 | 2 |

## Key defects (critical and major)

| ID | Severity | Module | Summary |
|---|---|---|---|
| DEF-001 | Critical | Monthly Statements | Monthly statement includes a cancelled order and charges it in Amount due |
| DEF-009 | Critical | Cancellation | Seller cancellation is not shown to the buyer (BR-12) |
| DEF-006 | Major | Catalogue & Search | Category filter is ignored when combined with search text |
| DEF-010 | Major | Checkout | Minimum order per seller not enforced in a multi-seller checkout (BR-04) |
| DEF-011 | Major | Checkout | Default 'Minimum order per seller' is ₹2,000; design says ₹1,500 (BR-04) |
| DEF-014 | Major | Inquiries | Message seller button does nothing |
| DEF-015 | Major | Reorder | Reorder drops a line from the order without telling the buyer |
| DEF-016 | Major | Catalogue & Search | Out-of-stock products are displayed in the catalogue and search results |
| DEF-018 | Major | Checkout | Duplicate orders created and stock deducted twice on repeated order submission |
| DEF-019 | Major | Operator | Updated same-day cut-off time in operator settings is not reflected at checkout |
| DEF-020 | Major | Seller - CSV Import | CSV import accepts negative stock and blank category without reporting errors |
| DEF-021 | Major | Operator | Logistics export shows slot end before slot start |
| DEF-022 | Major | Invoices | Invoice is missing the delivery fee line and seller GSTIN |

## Notes

- Defect IDs are not consecutive. DEF-002 and DEF-017 were withdrawn after retesting failed to reproduce them.
- Some checks depend on operator settings. The **Test Data** column records the value in force at the time of the test, e.g. a minimum order of ₹1,000 against the default of ₹2,000 (see DEF-011).

## What I would test next

These areas are in the design but were not covered in the time available:

| Area | Why it matters |
|---|---|
| Partner API (IF-03): paging, `X-Api-Key` auth, `PUT /offers` validation | Seller systems depend on it; a paging gap or duplicate means missed or double-shipped orders. |
| Store-clock boundary tests (BR-24): cut-off at 09:59:59 and 10:00:00, month-end statements | Time rules fail at the edges; the store clock makes these exact. |
| Performance and limits (NF-01 to NF-03): 30 concurrent checkouts, search time, HTTP 429 above 50 requests/s | Duplicate orders on a double click (DEF-018) suggest concurrency issues that load would expose. |
| Scripted concurrent last-stock and slot-capacity races (BR-01, BR-05) | These were checked by hand only; parallel requests would prove stock and slot capacity can never be exceeded. |
| Server-side validation: forced requests for disabled slots, other buyers' and sellers' data by URL or API (BR-21) | UI checks can be bypassed; data isolation is a security risk. |
| Full refund and exchange flows with seller approval and statement impact (BR-17, BR-18, BR-20) | Money calculations; partly covered only. |
| CSV import edge cases (IF-01): UTF-8/Hindi names, duplicate SKU in one file, same SKU across sellers, wrong headers | Data quality for every seller catalogue. |
| Logistics export for shipped and redelivery-requested orders, and pieces = cases × case size (IF-02) | Only one accepted order was in the export during testing. |
