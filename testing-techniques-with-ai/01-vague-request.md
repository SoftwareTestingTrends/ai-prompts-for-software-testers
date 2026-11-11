# Prompt 1: A vague request

**Technique:** None named. This is the starting point the other prompts improve on.

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Write test cases for a sign-up form. Users must be between 18 and 65 years old to register.
```

## What we found when we reviewed the answer

- **Done without being asked:** it applied boundary value analysis (17, 18, 19, 64, 65, 66) and added representative ages, negative cases, date-of-birth cases and more: about 35 test cases in six sections.
- **Decided on its own:** the prompt says "between 18 and 65", which doesn't say whether 65 is allowed. The answer turned it into "18 to 65 inclusive" and never asked. That question belongs to the product owner.
- **One wrong expected result:** in the date-of-birth table ("Assuming today's date is November 8, 2026"), it lists **November 7, 1960 as age 65, Accept**. Someone born on that date turned 66 the day before, so the expected result should be Reject. The last birth date that should be accepted, **November 9, 1960**, isn't in the table. (We checked the ages with a script.)
- **The lesson:** a long answer looks thorough, and that makes a mistake inside it easier to miss.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

# Test Cases: Sign-Up Form with Age Validation

Requirement: Users must be at least 18 years old and no older than 65 years old to register.

Business rule:

- Minimum eligible age: 18 years.
- Maximum eligible age: 65 years.
- Eligible age range: 18 to 65 inclusive.
- Users younger than 18 or older than 65 must not be allowed to register.

## 1. Functional test cases

| TC ID  | Test Scenario                           | Test Data / Age | Expected Result                                  | Priority |
| ------ | --------------------------------------- | --------------- | ------------------------------------------------ | -------- |
| TC_001 | Register with minimum eligible age      | 18              | Registration succeeds                            | High     |
| TC_002 | Register with maximum eligible age      | 65              | Registration succeeds                            | High     |
| TC_003 | Register with age within eligible range | 25              | Registration succeeds                            | High     |
| TC_004 | Register with age just below minimum    | 17              | Registration is rejected with validation message | High     |
| TC_005 | Register with age just above maximum    | 66              | Registration is rejected with validation message | High     |
| TC_006 | Register with age below minimum         | 10              | Registration is rejected                         | High     |
| TC_007 | Register with age above maximum         | 80              | Registration is rejected                         | High     |
| TC_008 | Register with middle eligible age       | 40              | Registration succeeds                            | Medium   |
| TC_009 | Submit form without date of birth       | Empty           | Required field validation is displayed           | High     |
| TC_010 | Enter invalid date of birth             | Invalid date    | Appropriate validation message is displayed      | High     |

## 2. Boundary value analysis

Boundary testing is particularly important because the requirement defines minimum and maximum age limits.

| Test Case              | Age | Expected Result |
| ---------------------- | --- | --------------- |
| Below minimum boundary | 17  | Reject          |
| Minimum boundary       | 18  | Accept          |
| Above minimum boundary | 19  | Accept          |
| Below maximum boundary | 64  | Accept          |
| Maximum boundary       | 65  | Accept          |
| Above maximum boundary | 66  | Reject          |

Valid range: 18–65 inclusive

## 3. Negative and edge test cases

| TC ID  | Test Scenario                                                     | Expected Result                              |
| ------ | ----------------------------------------------------------------- | -------------------------------------------- |
| TC_011 | Enter a future date of birth                                      | Registration is rejected                     |
| TC_012 | Enter a date of birth in an invalid format                        | Validation error is displayed                |
| TC_013 | Enter an impossible date (e.g., February 30)                      | Validation error is displayed                |
| TC_014 | Enter a date of birth with a leap-year date (February 29)         | Correct age calculation is performed         |
| TC_015 | Change the system date and recalculate eligibility                | Age validation uses the correct current date |
| TC_016 | Attempt registration by bypassing frontend validation through API | Backend rejects ineligible users             |
| TC_017 | Modify date of birth using browser developer tools                | Backend independently validates eligibility  |
| TC_018 | Submit the form multiple times with an invalid age                | No account is created                        |

## 4. Date-of-birth boundary scenarios

If the sign-up form uses Date of Birth rather than an age field, test the actual date boundaries.

Assuming today's date is November 8, 2026:

| Date of Birth    | Calculated Age | Expected Result |
| ---------------- | -------------- | --------------- |
| November 9, 2008 | 17             | Reject          |
| November 8, 2008 | 18             | Accept          |
| November 7, 2008 | 18             | Accept          |
| November 8, 1961 | 65             | Accept          |
| November 7, 1961 | 65             | Accept          |
| November 6, 1961 | 65             | Accept          |
| November 7, 1960 | 65             | Accept          |
| November 8, 1960 | 66             | Reject          |

Note: The DOB boundaries should be calculated dynamically based on the current date. The table illustrates the age-calculation principle.

## 5. Additional validation checks

| Area               | Validation                                                                 |
| ------------------ | -------------------------------------------------------------------------- |
| Error messages     | Clearly explain that users must be between 18 and 65 years old.            |
| Field highlighting | Invalid DOB field is visually highlighted.                                 |
| Form submission    | Registration is blocked when age validation fails.                         |
| Data persistence   | Invalid registrations do not create user records.                          |
| API validation     | Age restrictions are enforced on the backend.                              |
| Security           | Client-side validation cannot be bypassed to create an ineligible account. |
| Accessibility      | Validation messages are accessible to screen readers.                      |

## 6. Recommended automation scenarios

For automated testing, I would prioritize these scenarios:

1. User aged 17 attempts registration and is rejected.
2. User aged 18 successfully registers.
3. User aged 19 successfully registers.
4. User aged 64 successfully registers.
5. User aged 65 successfully registers.
6. User aged 66 attempts registration and is rejected.
7. User submits registration without DOB.
8. User attempts to bypass frontend validation through an API request.

QA recommendation: Implement age validation using the full date of birth, not simply the difference between birth year and current year. The calculation must account for whether the user's birthday has occurred in the current year. Also, validate on both frontend and backend.

This set provides good coverage using equivalence partitioning, boundary value analysis, negative testing, and security testing.

---

[Back to all eight prompts](./README.md)
