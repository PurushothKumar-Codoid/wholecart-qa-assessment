# AI session 2: excerpt (test cases, bugs, questions)

This is an **excerpt** of `session-2-testcases-and-defects.md`, the full session log in this folder. It keeps only the messages about test cases, bugs and questions/assumptions, with tool calls removed. AI tool usage (including the early automated calls disclosed in the README) for results and defect evidence are covered in the full log, not here.

---
### 🤖 Assistant

Simplifying the defect numbering hack before running.

---
### 🧑 User

Remove Title and Description in testcases. I want only Test Sceanrios in detail with word Verify

---
### 🤖 Assistant

The **Test Cases** sheet in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) now has a single **Test Scenario** column (column D) where Title/Scenario and Description used to be. I checked the rebuilt file and the new header and first rows are correct.

- **Scenarios:** all 46 are full sentences starting with "Verify that…", and each names the business rule it covers. For example: *"Verify that a cancelled order does not appear in the monthly statement and is not added to Orders total or Amount due (BR-20)."*
- **Other columns:** everything else is unchanged and has shifted one column left. Status is now column P.
- **Panes:** the first four columns (ID, Module, SubModule, Test Scenario) stay frozen while you scroll.

---
### 🤖 Assistant

Last step: updating the README counts and key defects.

---
### 🤖 Assistant

I've updated the Test Cases sheet in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) and checked the rebuilt file:

- **Removed:** the SubModule and Created By columns.
- **Added:** a **User Type** column (column C), between Module and Test Scenario.

| User Type | Count | Used for |
|---|---|---|
| Buyer | 36 | Catalogue, cart, checkout, orders, cancellation, reorder, invoices, statements |
| Seller | 8 | Seller orders, seller products, CSV import, partner API |
| Buyer, Seller | 4 | Cases where both roles act: seller cancel seen by buyer; refund limits, partial refund amount and statement refunds (seller approves) |
| Buyer, Operator | 3 | Time-boundary cases that need the operator to fix the store clock: delivery date range, 10:00 cut-off, the exact 5:00 cancel window |
| Operator | 1 | Logistics export |

The columns are now: Test Case ID, Module, User Type, Test Scenario, Test Case Type, Test Type, Preconditions, Test Steps, Test Data, Expected Result, Actual Result, Application Environment, Network Type, Executed By, Bug ID / Jira ID, Status, Severity, Priority, Automation (Y/N), Created Date.

The filter row includes User Type, so you can filter to just the Buyer or just the Seller cases when running them.

---
### 🧑 User

Remove test sceanrio. I want as testcase title and testcase description

---
### 🤖 Assistant

I've replaced Test Scenario with two columns, **Test Case Title** (column D) and **Test Case Description** (column E), in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx). I checked the rebuilt file and the Status colours and filters still work.

- **Title:** a short name for each case, with the business rule it covers. For example, *"Buyer cannot open another buyer's order (BR-21)"*.
- **Description:** the detailed "Verify that…" sentence. For example, *"Verify that a buyer cannot view another buyer's order, invoice or statement by opening its URL directly, and gets access denied with no data shown (BR-21)."*

The columns are now: Test Case ID, Module, User Type, Test Case Title, Test Case Description, Test Case Type, Test Type, Preconditions, Test Steps, Test Data, Expected Result, Actual Result, Application Environment, Network Type, Executed By, Bug ID / Jira ID, Status, Severity, Priority, Automation (Y/N), Created Date.

---
### 🤖 Assistant

Adding the operator-side test cases and updating the related results and defects.

---
### 🧑 User

I want as Bug Title and Description remove the Summary

---
### 🧑 User

Bug description now very difficult to undersatnd now Bug summary is enough with some more detail

---
### 🤖 Assistant

I've replaced Bug Title and Bug Description with a single **Bug Summary** column in the Defect Log of [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx), and checked the rebuilt file.

Each summary is now one plain sentence saying what went wrong. Where it helps, it names the actual order number and amount from your test session:

- **DEF-001:** Cancelled order WC-01008-1 is shown on the October statement and its ₹2004.82 is added to Amount due (BR-20).
- **DEF-002:** Reorder of WC-01008-2 (2 cases) right after checkout puts 4 cases in the cart instead of 2 (BR-16).
- **DEF-009:** Seller cancelled WC-01012-1 and WC-01010-1, but the buyer still sees them as "accepted" / "placed" (BR-12).
- **DEF-010:** Order WC-01010-1 was placed with only ₹132.48 for WholeCart Direct because another seller in the same checkout was above the minimum (BR-04).

The full detail is still in the Steps to Reproduce, Expected Result and Actual Result columns.

---
### 🤖 Assistant

I've cut each Description in the Defect Log to one short line. Summary stays the same, and I checked the rebuilt [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx).

Examples:
- **DEF-001:** Cancelled orders should not be on the statement, but WC-01008-1 is listed and charged ₹2004.82.
- **DEF-002:** Reorder of a 2-case order adds 4 cases to the cart.
- **DEF-009:** Seller cancelled the order, but the buyer still sees "accepted" / "placed".
- **DEF-011:** Minimum order is set to ₹2,000; design says ₹1,500.

The full detail is still in Steps to Reproduce, Expected Result and Actual Result.

---
### 🧑 User

Test Case ID	Module	User Type	Test Case Title	Test Case Description	Test Case Type	Preconditions	Test Steps	Test Data	Expected Result	Actual Result	Application Environment	Status	Bug ID						

THis header required enough for testcase. Please update

---
### 🤖 Assistant

The Test Cases sheet in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) now has only your 14 columns, in this order:

Test Case ID | Module | User Type | Test Case Title | Test Case Description | Test Case Type | Preconditions | Test Steps | Test Data | Expected Result | Actual Result | Application Environment | Status | Bug ID

- **Removed:** Test Type, Network Type, Executed By, Severity, Priority, Automation (Y/N) and Created Date.
- **Unchanged:** all 57 test cases and their data. I checked the rebuilt file; the Status colours and the filter row still work.

The assignment brief lists **priority** as required for test cases ("Steps, test data, expected result, priority, and actual result"). With that column removed, reviewers may mark the submission as incomplete. Should I add a Priority column back after Status?

---
### 🤖 Assistant

Making the Defect Log's Linked Test Cases column handle a test case linked to two bugs ("DEF-002, DEF-015"), then rebuilding.

---
### 🤖 Assistant

The build worked; only my check script tripped on an empty row. Checking the Defect Log.

---
### 🤖 Assistant

Yes. [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) was last saved at **16:06 today**, and I've just reopened it to confirm the retest changes are there:

- **DEF-002:** Description reads "Reorder of WC-01008-2 (2 cases) added 4 cases. Not reproduced on retest." Status is **Open - not reproduced on retest**.
- **DEF-015:** Description reads "Reorder leaves out the last line of the order (seen on WC-01021-1, WC-01001-1, WC-01003-1) with no warning." Status is **Open**.
- **TC-10-01:** Fail, linked to DEF-002 and DEF-015.
- **TC-10-02:** Fail, linked to DEF-015.
- **Summary sheet:** 58 test cases (19 Pass, 16 Fail, 0 Blocked, 23 Not Executed).

If the file is open in Excel or WPS, close and reopen it to see these changes.

---
### 🧑 User

If bug not reproducible remove the bug and update tescases

---
### 🤖 Assistant

I'll remove DEF-002, since it didn't reproduce, and update TC-10-01 so it links only to DEF-015.

---
### 🧑 User

Remove the timing in the actual result from bug and testcases and also difficult to understand actual result

---
### 🤖 Assistant

The test case results are fixed, but the bug Actual Results weren't replaced (I used the wrong column position). Fixing that.

---
### 🧑 User

1. Testcase - Testcase description is so much descriptive
2. Testcase - Expected result should some more elborate use word should
3. Bug - Expected result should some more elborate use word should
3. Bug - Actual result is so much descriptive

---
### 🤖 Assistant

I'll rewrite those four columns. First, the current Test Case Description and Expected Result for every case.

---
### 🤖 Assistant

I've made all four changes in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) and checked the rebuilt file: every Expected Result uses "should" (all 58 test cases and all 14 bugs).

**1. Test case Description: now short (one line, at most 67 characters)**
- Before: *"Verify that a buyer cannot view another buyer's order, invoice or statement by opening its URL directly, and gets access denied with no data shown (BR-21)."*
- After: *"Verify a buyer cannot see another buyer's orders."*

**2. Test case Expected Result: fuller, using "should"**
- Before: *"403/404; no order, invoice or statement data of buyer2 is shown"*
- After: *"Access should be denied (403/404). No order, invoice or statement details of the other buyer should be shown."*

While rewriting these, I corrected two Expected Results that still described old test data. Reorder now says "every line with the same quantity as the original order" instead of naming Cardamom 2. "Seller sees only own sub-orders" now names WC-01010-1 and WC-01010-2 instead of WC-01008.

**3. Bug Expected Result: fuller, using "should"**
- Before: *"Cancelled order not listed; Orders total ₹0.00; Amount due ₹0.00 (BR-20: …)"*
- After: *"Cancelled orders should not appear on the statement. Orders total and Amount due should be ₹0.00 when no orders are delivered."*

**4. Bug Actual Result: now short (a few words each)**

| Bug | Actual Result |
|---|---|
| DEF-001 | Cancelled order is on the statement; ₹2,004.82 added to Amount due. |
| DEF-009 | Buyer still sees 'accepted' / 'placed'. |
| DEF-010 | Order placed with ₹132.48 net. |
| DEF-014 | Nothing happens. |
| DEF-015 | Last line missing from the cart. |

---
### 🧑 User

Add some detail in actual result in bug

---
### 🤖 Assistant

The bug Actual Results in [phase-1/WholeCart_TestCases.xlsx](phase-1/WholeCart_TestCases.xlsx) now give the order number, the screen and the exact message, still with no timings. Each is one or two sentences:

| Bug | Actual Result |
|---|---|
| DEF-001 | Cancelled order WC-01008-1 is listed on the October statement with status 'cancelled', and ₹2,004.82 is added to Orders total and Amount due. |
| DEF-009 | Seller's list shows WC-01012-1 and WC-01010-1 as 'cancelled', but the buyer still sees them as 'accepted' and 'placed'. Buyer's own Cancel fails with 'This order can no longer be cancelled'. |
| DEF-010 | Order WC-01010-1 for WholeCart Direct was placed with only ₹132.48 net (total ₹257.10), because the other seller in the same checkout was above the minimum. |
| DEF-014 | Clicking 'Message seller' on WC-01023-1 several times does nothing: no form, no page change and no error. |
| DEF-015 | Reorder adds all lines except the last one, with no warning: Almond seeds (WC-01021-1), Royal Moong Dal (WC-01001-1) and Chef's Cold Coffee (WC-01003-1) were missing from the cart. |

The other nine bugs follow the same style. I checked the rebuilt file and all 14 are updated.

---
### 🧑 User

Compare bug with my sheet what are missed from my end?

---
### 🧑 User

UI is not aligned in seller. So raise abug and add testcase for this

---
### 🧑 User

Now I added the the sheet(WholeCart Testing.xlsx) with manual verification and added some bugs in my end and updated sheet. First check the sheet and share you thoughts.

---
### 🤖 Assistant

I'll fill both directly in **WholeCart Testing.xlsx**. First, a fresh read, since you've updated TC-04-12.

---
### 🧑 User

I have removed the DEF-17

---
### 🧑 User

1. TC-03-03 -  I have fixed
2. TC-05-02, TC-05-03 - Fix this
3. DEF-022 - Fix this
4. No Need
5. Fix this
6. Fix this
7. Fix this
8. Fix this
9. Fix this
10. Fix this
11. Fix this
12. THis is bug only I have retested it
13. Fix this
14. Fix this
15. Fix this
16. No need

---
### 🤖 Assistant

Going ahead. First a fresh read of the sheet: you've fixed TC-03-03, and I want to check the Pass rows' Test Data against the Actual Results I wrote for item 15.

---
### 🧑 User

Needs a decision from you -  Fix this - Fail only
Test Data / Steps that don't match the Actual Result -  Fix all

Bug sheet polish 
1. Fix this
2. Fix this
3. No Need

---
### 🤖 Assistant

Making the changes in **WholeCart Testing.xlsx**:
- **TC-13-01:** set to Fail, linked to DEF-001.
- **Five mismatched test cases:** align their Test Data and Steps with the run in the Actual Result. **TC-03-03** has the same problem (its precondition and steps describe "Product X", unlike its data), so I'll align that too.
- **DEF-006:** fix the summary wording.
- **Bug modules:** set each to the module of its first linked test case.

Backing up first.

---
### 🧑 User

Go with sentence case for all bugs

---
### 🤖 Assistant

Six summaries use Title Case (DEF-016, 018, 019, 020, 022 and 024). I'll convert them to sentence case and keep acronyms like CSV and GSTIN as they are.

---
### 🤖 Assistant

I've added the **Summary** sheet as the first tab in **WholeCart Testing.xlsx**. I checked that every formula reads the right column (Module, User Type, Status, Severity, Priority) and worked out what each one will show.

**What it contains:**

| Section | Shows |
|---|---|
| Header | Project, specification, environment, accounts used, test date |
| **Overall** | 58 test cases · 34 Pass · 24 Fail · **59% pass rate** · 22 defects logged, 22 open |
| **Test execution by module** | Total / Pass / Fail / Pass % / Defects for all 18 modules, plus a total row |
| **By user type** | Buyer 37 · Seller 8 · Buyer, Operator 7 · Buyer, Seller 4 · Operator 2 |
| **Defects by severity × priority** | Critical 2 · Major 11 · Minor 6 · Trivial 3 (High 13 · Medium 3 · Low 6) |
| **Defects by module** | Count per module (14 modules have bugs) |
| **Key defects** | The 2 Critical and 11 Major bugs with summary, priority and module |

**How it updates:**
- **Counts are live formulas.** If you change a status in Testcases or add a bug in Bugs, every count updates automatically when the file is opened in WPS or Excel.
- **The Key defects list is a fixed list as of now.** If you add or remove a Critical or Major bug, ask me and I'll refresh it.

The **Defects** column in the module table counts bugs by the **bug's** module. That's why Refunds & Exchanges shows 1 Fail but 0 defects: its failing case (TC-11-01) is linked to DEF-005, whose module is Order History.

I saved a backup before adding the sheet. When you open the file, the Summary tab shows first.

---
### 🤖 Assistant

The Manual Status column is **already removed**. I deleted it in the earlier round of fixes, and the file on disk has no such column. The Testcases sheet ends with **Status | Bug ID**, as you can see here:

> Test Case ID · Module · User Type · Test Case Title · Test Case Description · Test Case Type · Preconditions · Test Steps · Test Data · Expected Result · Actual Result · Application Environment · Status · Bug ID

If you still see it, WPS probably has an **older copy of the file open**. Close that window **without saving** and reopen **WholeCart Testing.xlsx**. If you save from the old window, it will overwrite the latest changes, including the Summary sheet and the sentence-case summaries.

---
### 🤖 Assistant

Checking the result: any remaining unformatted amounts, the quoted app messages, and the edited bug rows.

---
### 🤖 Assistant

Everything is applied. One knock-on fix: DEF-016's precondition still says "Logged in as buyer1", but the new steps start as seller1. Updating it.

---
### 🤖 Assistant

I recovered all 58 priorities. The only case not in my original design is TC-19-06, which gets **High** to match its bug (DEF-019, High). Adding the column after Status now.

---
### 🤖 Assistant

The Priority column is in: 49 High, 4 Medium, 5 Low, placed after Status. The Summary formulas still point at Status, so they're unaffected. Next, the **Questions & Assumptions** sheet.

---
### 🤖 Assistant

Questions & Assumptions sheet added (16 questions). Next, `ai-sessions`: finding this chat's session log.

---
### 🤖 Assistant

Everything is in `phase-1/` (9.4 MB). Fixing one README line: it says "stock is not checked at all", which contradicts your sheet now that TC-03-03 and TC-04-12 pass and DEF-017 is withdrawn.
