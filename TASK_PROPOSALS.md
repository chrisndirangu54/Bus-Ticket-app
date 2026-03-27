# Codebase Task Proposals

## 1) Typo fix task
**Task:** Rename the `HISTROY_FRAG_ACTIVE` flag to `HISTORY_FRAG_ACTIVE` and update all references.

**Why:** The current identifier contains a typo and is referenced from multiple files, which makes the code harder to read/search and increases the chance of introducing additional naming mistakes.

**Evidence:**
- `Utils` declares `HISTROY_FRAG_ACTIVE`.
- `HistoryFragment`, `OrdersFragment`, and `OrderDetailsActivity` all use the same misspelled field.

## 2) Bug fix task
**Task:** Fix signup validation so the email-required check validates `emailAddress` instead of `address`.

**Why:** The current logic checks `TextUtils.isEmpty(address)` twice; the second check sets an error on the email field. This can allow empty email values to pass while incorrectly coupling validation behavior to the address field.

**Evidence:**
- In `SignUpActivity.attemptLogin()`, both the address validation and email-field validation condition use `TextUtils.isEmpty(address)`.

## 3) Comment/documentation discrepancy task
**Task:** Update misleading inline comments in `SignUpActivity` to describe signup behavior accurately (replace login wording with signup wording).

**Why:** Comments currently say "attempt login" and "user login attempt" inside signup flow. This is documentation drift that can confuse maintainers.

**Evidence:**
- In `SignUpActivity`, comments near submit logic refer to "login" even though the class and flow are signup.

## 4) Test improvement task
**Task:** Replace brittle date-format test in `GeneralUnitTest` with deterministic assertions that verify behavior for known inputs and edge cases.

**Why:** `testFormatDate()` currently depends on `new Date().toString()` matching a hard-coded weekday/month/day string, which is time-dependent and will fail on most dates. This creates non-actionable CI noise.

**Evidence:**
- `GeneralUnitTest.testFormatDate()` asserts `"Wed Aug 30"` against `Utils.formatDateString(new Date().toString())`.
