# Prompt 8: White-box coverage gaps

**Technique:** Statement, branch and condition coverage

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Here is a registration function and its current tests.

def can_register(age, email_taken, terms_accepted):
    if age < 18 or age > 65:
        return "Age must be between 18 and 65"
    if email_taken:
        return "Email already registered"
    if not terms_accepted:
        return "Accept the terms to continue"
    return "OK"

Tests:
- can_register(25, False, True) returns "OK"
- can_register(10, False, True) returns "Age must be between 18 and 65"

Which statements, branches and conditions do these tests leave uncovered? Suggest the smallest set of extra tests that gives full branch and condition coverage.
```

## What we found when we reviewed the answer

- **Correct:** it found both return statements that never run ("Email already registered" and "Accept the terms to continue"), the two branches that are never taken, and the condition `age > 65`, which is never true.
- **Correct explanation:** with the test at age 10, `age < 18` is already true, so Python never evaluates `age > 65` (short-circuit evaluation).
- **Its three extra tests** (age 70, email taken, terms not accepted) give full branch and condition coverage, which matches our own analysis.
- **Our reference answer:** the two tests never reach the email or terms returns, `email_taken` and `not terms_accepted` are never true, and `age > 65` is never true.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

The existing tests cover only the valid registration path and the invalid age path. They do not exercise the email or terms validation branches.

## 1. Current coverage analysis

The function has three decision points:

| Decision               | True branch | False branch |
| ---------------------- | ----------- | ------------ |
| `age < 18 or age > 65` | Age error   | Continue     |
| `email_taken`          | Email error | Continue     |
| `not terms_accepted`   | Terms error | Continue     |

### Coverage from existing tests

| Test                            | Age condition | Email condition | Terms condition | Result    |
| ------------------------------- | ------------- | --------------- | --------------- | --------- |
| `can_register(25, False, True)` | False         | False           | False           | OK        |
| `can_register(10, False, True)` | True          | Not evaluated   | Not evaluated   | Age error |

Uncovered items:

- Statements: The email error return and terms error return statements are never executed.
- Branches: The True branches of `email_taken` and `not terms_accepted` are not covered.
- Conditions: The `age > 65` condition has not been independently evaluated as True. The email and terms conditions have only been evaluated as False.

## 2. Smallest set of additional tests

Add these three tests:

| Test | Input                            | Expected result                   | Coverage purpose         |
| ---- | -------------------------------- | --------------------------------- | ------------------------ |
| T3   | `can_register(70, False, True)`  | `"Age must be between 18 and 65"` | Exercises `age > 65`     |
| T4   | `can_register(25, True, True)`   | `"Email already registered"`      | Covers email True branch |
| T5   | `can_register(25, False, False)` | `"Accept the terms to continue"`  | Covers terms True branch |

## 3. Final coverage



100% statement coverage

100% branch coverage

100% condition coverage



| Coverage type      | Before  | After  |
| ------------------ | ------- | ------ |
| Statement coverage | Partial | 100%   |
| Branch coverage    | 4 of 6  | 6 of 6 |
| Condition coverage | Partial | 100%   |

Total test cases: 5 (2 existing + 3 additional).

## 4. Important distinction

The age condition contains two atomic Boolean conditions:

```
age < 18age > 65
```

The existing test with age `10` evaluates the first condition as True. Because Python uses short-circuit evaluation with `or`, the second condition is not evaluated.

The new test with age `70` evaluates the second condition as True.

Together with the valid-age test, both atomic conditions have been evaluated as True and False.

Key takeaway: Branch coverage checks whether each decision outcome has been exercised. Condition coverage checks whether each individual Boolean condition has evaluated to both True and False.

---

[Back to all eight prompts](./README.md)
