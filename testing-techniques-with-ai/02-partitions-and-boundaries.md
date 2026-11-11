# Prompt 2: Equivalence partitioning and boundary value analysis

**Technique:** Equivalence partitioning, boundary value analysis

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Apply equivalence partitioning and boundary value analysis to the age field of a sign-up form.
The rule: users aged 18 to 65 can register, and both 18 and 65 are allowed.
Give me a table with these columns: test value, partition or boundary, expected result.
```

## What we found when we reviewed the answer

- **Correct:** one representative from each partition (15, 30, 70) and all six boundary values (17, 18, 19, 64, 65, 66), each with the right expected result. Nine tests in total.
- **Why it's better than prompt 1:** the rule about 65 is stated in the prompt instead of guessed, and nine rows can be checked against the number line in seconds.
- **How to review it:** count the partitions, check both edges, and look for the value on each side of each edge.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

The valid age range is 18 to 65 inclusive. Therefore, ages below 18 and above 65 are invalid.

### 1. Equivalence Partitioning (EP)

Divide the age field into three equivalence partitions.

| Test value | Partition or boundary    | Expected result       |
| ---------- | ------------------------ | --------------------- |
| 15         | Invalid: Below 18        | Registration rejected |
| 30         | Valid: Between 18 and 65 | Registration accepted |
| 70         | Invalid: Above 65        | Registration rejected |

### 2. Boundary Value Analysis (BVA)

Test values at and immediately around the minimum and maximum boundaries.

| Test value | Partition or boundary | Expected result       |
| ---------- | --------------------- | --------------------- |
| 17         | Minimum - 1           | Registration rejected |
| 18         | Minimum boundary      | Registration accepted |
| 19         | Minimum + 1           | Registration accepted |
| 64         | Maximum - 1           | Registration accepted |
| 65         | Maximum boundary      | Registration accepted |
| 66         | Maximum + 1           | Registration rejected |

### 3. Summary



Valid range: 18–65

Invalid range: Below 18 or above 65



Key testing takeaway:

- Equivalence Partitioning reduces the number of test cases by selecting representative values from each partition.
- Boundary Value Analysis focuses on values at and immediately around the limits, where defects are more likely to occur.

Total: 9 test cases, with 3 for EP and 6 for BVA.

---

[Back to all eight prompts](./README.md)
