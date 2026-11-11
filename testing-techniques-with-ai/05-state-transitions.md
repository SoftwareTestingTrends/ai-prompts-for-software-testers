# Prompt 5: State transition testing

**Technique:** State transition testing

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Here are the rules for a user account after sign-up:
- A new account is Pending until the user verifies their email address. Then it becomes Active.
- Five wrong passwords in a row lock an Active account.
- A password reset unlocks a Locked account and makes it Active again.
Draw a state transition table for the account, then list test cases for the valid transitions and for invalid transitions that the system must refuse.
```

## What we found when we reviewed the answer

- **Result:** 12 transitions and 20 test cases, 10 of which check transitions the system must refuse.
- **Assumptions it added:** to fill gaps in the rules it listed "important assumptions", such as "The account cannot transition directly from Pending to Locked because login is not permitted before email verification." The prompt never said that a pending account can't log in. It's good that the assumptions are listed openly, and each one needs confirming before it becomes an expected result.
- **Minor:** TC19 is listed under the invalid transitions, but its expected state is Active (after a successful reset).
- **How to review it:** compare every transition with the rules you gave, and treat anything extra as a question, not a fact.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

## 1. Account State Transition Table

The account has three possible states:

1. Pending: Account created, but email address has not been verified.
2. Active: Email verified, and the account can be used normally.
3. Locked: Account locked after five consecutive incorrect password attempts.

### State transition table

| Current State | Event / Condition                           | Next State | Expected System Behaviour                           |
| ------------- | ------------------------------------------- | ---------- | --------------------------------------------------- |
| Pending       | User verifies email                         | Active     | Activate the account                                |
| Pending       | User enters incorrect password              | Pending    | Reject login                                        |
| Pending       | User enters correct password                | Pending    | Reject login until email is verified                |
| Active        | User enters correct password                | Active     | Allow login                                         |
| Active        | 1st to 4th consecutive wrong password       | Active     | Reject login and increment failure counter          |
| Active        | 5th consecutive wrong password              | Locked     | Lock the account                                    |
| Active        | User requests password reset                | Active     | Allow password reset without changing account state |
| Locked        | User attempts login with correct password   | Locked     | Reject login                                        |
| Locked        | User attempts login with incorrect password | Locked     | Reject login                                        |
| Locked        | User successfully resets password           | Active     | Unlock the account                                  |
| Locked        | User verifies email again                   | Locked     | Do not change account state                         |
| Pending       | User requests password reset                | Pending    | Do not activate the account                         |

Important assumptions:

- A successful login resets the consecutive failed-password counter to zero.
- Password reset only unlocks a Locked account after the reset is successfully completed.
- Password reset does not automatically verify an unverified email address.
- The account cannot transition directly from Pending to Locked because login is not permitted before email verification.

## 2. Valid Transition Test Cases

These test cases verify that the system correctly handles all permitted state transitions.

| TC ID | Initial State | Action / Event                                  | Expected State | Expected Result                               |
| ----- | ------------- | ----------------------------------------------- | -------------- | --------------------------------------------- |
| TC01  | Pending       | Verify email successfully                       | Active         | Account becomes Active                        |
| TC02  | Active        | Enter correct password                          | Active         | Login successful                              |
| TC03  | Active        | Enter 1st wrong password                        | Active         | Login rejected; counter = 1                   |
| TC04  | Active        | Enter 2nd wrong password                        | Active         | Login rejected; counter = 2                   |
| TC05  | Active        | Enter 3rd wrong password                        | Active         | Login rejected; counter = 3                   |
| TC06  | Active        | Enter 4th wrong password                        | Active         | Login rejected; counter = 4                   |
| TC07  | Active        | Enter 5th consecutive wrong password            | Locked         | Account becomes Locked                        |
| TC08  | Active        | Successfully reset password                     | Active         | Password updated; account remains Active      |
| TC09  | Locked        | Successfully reset password                     | Active         | Password updated; account unlocked            |
| TC10  | Active        | Successful login after previous failed attempts | Active         | Login successful; failure counter resets to 0 |

## 3. Invalid Transition Test Cases

These test cases verify that the system refuses transitions that are not permitted by the business rules.

| TC ID | Initial State | Action / Event                                                           | Expected State | Expected Result                                |
| ----- | ------------- | ------------------------------------------------------------------------ | -------------- | ---------------------------------------------- |
| TC11  | Pending       | Attempt login with correct password                                      | Pending        | Login rejected; email verification required    |
| TC12  | Pending       | Attempt login with incorrect password five times                         | Pending        | Login rejected; account must not become Locked |
| TC13  | Pending       | Attempt to access protected account features                             | Pending        | Access denied                                  |
| TC14  | Pending       | Complete password reset without email verification                       | Pending        | Account must not become Active                 |
| TC15  | Active        | Attempt to lock account with only four consecutive wrong passwords       | Active         | Account must remain Active                     |
| TC16  | Locked        | Attempt login with correct password                                      | Locked         | Login rejected; password reset required        |
| TC17  | Locked        | Attempt login with incorrect password                                    | Locked         | Login rejected; account remains Locked         |
| TC18  | Locked        | Attempt email verification again                                         | Locked         | Account remains Locked                         |
| TC19  | Locked        | Attempt login using the old password after password reset                | Active         | Login rejected                                 |
| TC20  | Locked        | Attempt to unlock account without successfully completing password reset | Locked         | Account remains Locked                         |

## 4. State Transition Diagram

PENDING

Email not verified

Verify email

ACTIVE

Account operational

5 consecutive wrong passwords

LOCKED

Login prohibited

Successful password reset

Returns to ACTIVE

## 5. Additional Edge Cases Worth Testing

For thorough QA coverage, I would also include:

| Scenario                                                     | Expected Behaviour                                      |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| Four wrong passwords followed by one correct password        | Login succeeds; failure counter resets                  |
| Three wrong passwords, one correct, then two wrong passwords | Account remains Active; counter = 2                     |
| Five wrong passwords across separate sessions                | Account locks after the fifth consecutive failure       |
| Password reset initiated but not completed                   | Account remains Locked                                  |
| Password reset link expired                                  | Account remains Locked                                  |
| Password reset link already used                             | Reject reuse; account state unchanged                   |
| Two simultaneous incorrect login attempts at the threshold   | Account must lock reliably without race conditions      |
| Password reset completed twice                               | Second reset must not cause an invalid state transition |

QA takeaway: This is a good example of combining state transition testing with boundary value testing. The most important boundary is the fifth consecutive failed password attempt. Test both sides of that boundary: four attempts must not lock the account, while five must.

Also, test every state against both permitted and prohibited events. This helps identify unexpected transitions, not just whether the happy path works.

---

[Back to all eight prompts](./README.md)
