# Prompt 3: Decision table

**Technique:** Decision table testing

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Build a decision table for registration on a sign-up form. Registration depends on three conditions:
1. The age is valid (18 to 65, both included).
2. The email address is not already registered.
3. The user has accepted the terms.
Show every combination of the three conditions as a column, with the expected result for each, and turn each column into one test case.
```

## What we found when we reviewed the answer

- **Correct:** all eight combinations of the three conditions, and every expected result follows the rule that registration needs all three.
- **Gap:** every failing column only says that registration is rejected. When two conditions fail (for example, the age and the terms), it doesn't say which error message the user sees. That's a question for the product owner.
- **How to review it:** check that every column is there and that each expected result follows the rules.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

A decision table for the registration form has 3 conditions, each with 2 possible outcomes. Therefore, there are:

\\[ 2^3 = 8 \text{ combinations} \\]

We need 8 test cases to cover every possible combination.

## 1. Decision table

Conditions:

- C1: Age is valid (18 to 65, inclusive).
- C2: Email address is not already registered.
- C3: User has accepted the terms.

Actions:

- A1: Allow registration.
- A2: Reject registration.

| Conditions / Actions  | TC01 | TC02 | TC03 | TC04 | TC05 | TC06 | TC07 | TC08 |
| --------------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Age is valid?         | Yes  | Yes  | Yes  | Yes  | No   | No   | No   | No   |
| Email not registered? | Yes  | Yes  | No   | No   | Yes  | Yes  | No   | No   |
| Terms accepted?       | Yes  | No   | Yes  | No   | Yes  | No   | Yes  | No   |
| Allow registration    | Yes  | No   | No   | No   | No   | No   | No   | No   |
| Reject registration   | No   | Yes  | Yes  | Yes  | Yes  | Yes  | Yes  | Yes  |

Decision rule: Registration is allowed only when all three conditions are satisfied. If even one condition fails, registration is rejected.

## 2. Test cases

Each column represents one test case.

| Test Case | Age     | Email Status       | Terms Accepted | Expected Result         |
| --------- | ------- | ------------------ | -------------- | ----------------------- |
| TC01      | Valid   | Not registered     | Yes            | Registration successful |
| TC02      | Valid   | Not registered     | No             | Registration rejected   |
| TC03      | Valid   | Already registered | Yes            | Registration rejected   |
| TC04      | Valid   | Already registered | No             | Registration rejected   |
| TC05      | Invalid | Not registered     | Yes            | Registration rejected   |
| TC06      | Invalid | Not registered     | No             | Registration rejected   |
| TC07      | Invalid | Already registered | Yes            | Registration rejected   |
| TC08      | Invalid | Already registered | No             | Registration rejected   |

## 3. Recommended test data

For meaningful execution, use representative values:

| Test Case | Age | Email              | Terms        |
| --------- | --- | ------------------ | ------------ |
| TC01      | 30  | new\@test.com      | Accepted     |
| TC02      | 30  | new\@test.com      | Not accepted |
| TC03      | 30  | existing\@test.com | Accepted     |
| TC04      | 30  | existing\@test.com | Not accepted |
| TC05      | 17  | new\@test.com      | Accepted     |
| TC06      | 17  | new\@test.com      | Not accepted |
| TC07      | 66  | existing\@test.com | Accepted     |
| TC08      | 66  | existing\@test.com | Not accepted |

For invalid age, consider testing both boundaries separately:

- 17: Below minimum age.
- 66: Above maximum age.

## 4. Testing concepts demonstrated

This exercise demonstrates two important black-box testing techniques:

1. Decision Table Testing: Covers all possible combinations of business conditions and their resulting actions.
2. Equivalence Partitioning: Groups ages into valid and invalid partitions, and emails into registered and unregistered partitions.

Key takeaway: Three binary conditions produce eight decision rules. All eight combinations should be tested to achieve complete decision-table coverage.

---

[Back to all eight prompts](./README.md)
