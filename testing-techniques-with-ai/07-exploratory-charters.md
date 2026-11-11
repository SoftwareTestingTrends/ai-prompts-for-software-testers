# Prompt 7: Exploratory testing charters

**Technique:** Exploratory testing

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Write three exploratory testing charters for a sign-up form with name, email, age and password fields. Use the format "Explore <target> with <resources> to discover <information>".
```

## What we found when we reviewed the answer

- **Result:** three charters in the requested format, but each one is broad. The first covers input validation across all four fields with every kind of test data, which is more than one session can cover.
- **A narrowed version (written by us, not ChatGPT):** "Explore the age field with pasted and autofilled values to discover how the form handles them."
- **The session itself stays with the tester,** because the unexpected shows up while someone is using the product and paying attention.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

1\. Explore input validation and boundary conditions with valid, invalid, empty, malformed, and boundary-value test data to discover how the name, email, age, and password fields handle unexpected or invalid inputs.

2\. Explore field interactions and data combinations with different combinations of names, email formats, age values, and password patterns to discover inconsistencies, unexpected dependencies, and validation gaps between fields.

3\. Explore security and error handling with special characters, extremely long inputs, SQL injection strings, HTML/JavaScript payloads, and repeated submission attempts to discover security vulnerabilities, application crashes, and improper error handling.

---

[Back to all eight prompts](./README.md)
