# Prompt 6: Error guessing

**Technique:** Error guessing

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
I'm testing the age and email fields of a sign-up form. List 15 inputs that are most likely to break these fields, with one line on why each one might fail.
```

## What we found when we reviewed the answer

- **Result:** 15 inputs plus extra checks. Four of them (17, 18, 65 and 66) repeat the boundary values that prompt 2 already covers.
- **The list is generic,** which is fine for a brainstorm. Keep the inputs that are real risks for your product, and add the ones only someone who knows the product would think of.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

Here are 15 high-risk test inputs for the age and email fields of a sign-up form. These target boundary conditions, invalid formats, edge cases, security issues, and input-handling defects.

| #  | Field | Test input               | Why it might fail                                                |
| -- | ----- | ------------------------ | ---------------------------------------------------------------- |
| 1  | Age   | `17`                     | Below the minimum allowed age.                                   |
| 2  | Age   | `18`                     | Minimum valid boundary may be incorrectly rejected.              |
| 3  | Age   | `65`                     | Maximum valid boundary may be incorrectly rejected.              |
| 4  | Age   | `66`                     | Above the maximum allowed age.                                   |
| 5  | Age   | `0`                      | Zero may be incorrectly accepted as a valid age.                 |
| 6  | Age   | `-5`                     | Negative numbers may bypass validation.                          |
| 7  | Age   | `18.5`                   | Decimal values may cause unexpected numeric validation.          |
| 8  | Age   | `abc`                    | Alphabetic characters may break numeric parsing.                 |
| 9  | Age   | `999999999999`           | Extremely large numbers may cause overflow or validation issues. |
| 10 | Age   | (Empty / NULL)           | Missing values may bypass required-field validation.             |
| 11 | Email | `userexample.com`        | Missing @ symbol may bypass format validation.                   |
| 12 | Email | `user@`                  | Missing domain may be incorrectly accepted.                      |
| 13 | Email | `@example.com`           | Missing local part may cause validation failure.                 |
| 14 | Email | `user..test@example.com` | Consecutive dots violate standard email address syntax.          |
| 15 | Email | `user@-example.com`      | A domain label beginning with a hyphen is invalid.               |

### Additional high-value checks

Beyond these 15 inputs, I recommend testing:

- Leading/trailing spaces: `"  user@example.com  "` to check trimming.
- Very long email: Test maximum supported length and database column limits.
- Unicode email: `josé@example.com` to check international character handling.
- Plus addressing: `user+test@gmail.com` to ensure valid addresses are accepted.
- Duplicate email: Register the same email twice to verify uniqueness validation.
- SQL injection: `' OR '1'='1` to check input sanitization and parameterized queries.
- XSS: `<script>alert(1)</script>` to check safe input handling and output encoding.

Testing tip: Do not focus only on rejecting invalid inputs. Equally important is verifying that valid edge cases, such as ages 18 and 65, are accepted.

---

[Back to all eight prompts](./README.md)
