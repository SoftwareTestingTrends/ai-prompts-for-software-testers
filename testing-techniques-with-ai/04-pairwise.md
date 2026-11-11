# Prompt 4: Pairwise testing

**Technique:** Pairwise (all-pairs) testing

**Run:** ChatGPT, default model, Thinking off, 8 November 2026. A fresh chat, and the first answer, unedited.

## The prompt

```
Our sign-up form must work in Chrome, Safari and Firefox, on desktop, tablet and phone, in English and French.
First, how many tests would every combination need?
Then give me a pairwise test set that covers every pair of values at least once, using as few tests as possible.
```

## What we found when we reviewed the answer

- **Correct:** every combination needs 18 tests, and its pairwise set has 9, which is the minimum here (browser × device alone has 9 pairs). A script confirmed that all browser–device, browser–language and device–language pairs are covered: 0 missing pairs.
- **Good:** it noted that pairwise testing can miss defects that need three settings together.
- **How to review it:** don't trust a pairwise set by eye. Check it with a script or a pairwise tool, because a missing pair is easy to overlook.

## ChatGPT's answer (unedited)

Everything between the two lines below is ChatGPT's answer exactly as it was returned.

---

You have 3 testing dimensions:

1. Browser: Chrome, Safari, Firefox (3 values).
2. Device: Desktop, Tablet, Phone (3 values).
3. Language: English, French (2 values).

## 1. Exhaustive testing: How many tests?

Exhaustive testing covers every possible combination of all three dimensions.

\\[ 3 \times 3 \times 2 = \boxed{18\text{ tests}} \\]

| Dimension          | Number of values |
| ------------------ | ---------------- |
| Browser            | 3                |
| Device             | 3                |
| Language           | 2                |
| Total combinations | 18               |

You would need 18 test cases to cover every possible combination.

## 2. Pairwise testing: Minimum test set

Pairwise testing ensures that every possible pair of values across any two dimensions appears together at least once.

For example:

- Every browser is tested with every device.
- Every browser is tested in both languages.
- Every device is tested in both languages.

9 tests required

Here is a pairwise test set that achieves complete pairwise coverage using only 9 tests.

| Test ID | Browser | Device  | Language |
| ------- | ------- | ------- | -------- |
| TC01    | Chrome  | Desktop | English  |
| TC02    | Chrome  | Tablet  | English  |
| TC03    | Chrome  | Phone   | French   |
| TC04    | Safari  | Desktop | English  |
| TC05    | Safari  | Tablet  | French   |
| TC06    | Safari  | Phone   | English  |
| TC07    | Firefox | Desktop | French   |
| TC08    | Firefox | Tablet  | English  |
| TC09    | Firefox | Phone   | English  |

## 3. Verify pairwise coverage

Let's verify that all pairs are covered.

A. Browser × Device

|         | Desktop | Tablet | Phone |
| ------- | ------- | ------ | ----- |
| Chrome  | TC01    | TC02   | TC03  |
| Safari  | TC04    | TC05   | TC06  |
| Firefox | TC07    | TC08   | TC09  |

9 of 9 pairs covered

B. Browser × Language

| Browser | English    | French |
| ------- | ---------- | ------ |
| Chrome  | TC01, TC02 | TC03   |
| Safari  | TC04, TC06 | TC05   |
| Firefox | TC08, TC09 | TC07   |

6 of 6 pairs covered

C. Device × Language

| Device  | English    | French |
| ------- | ---------- | ------ |
| Desktop | TC01, TC04 | TC07   |
| Tablet  | TC02, TC08 | TC05   |
| Phone   | TC06, TC09 | TC03   |

6 of 6 pairs covered

## 4. Exhaustive vs. Pairwise comparison

| Approach           | Number of tests |
| ------------------ | --------------- |
| Exhaustive testing | 18              |
| Pairwise testing   | 9               |
| Tests saved        | 9               |
| Reduction          | 50%             |

Why is 9 the minimum?

There are 9 unique Browser × Device combinations (3 × 3). Each test can cover only one of these combinations. Therefore, at least 9 tests are necessary.

Our proposed set achieves that lower bound while also covering every Browser × Language and Device × Language pair.

QA takeaway: Pairwise testing reduces the number of tests by 50% while maintaining complete two-way combination coverage. However, it does not guarantee detection of defects that occur only when three or more specific conditions interact.

---

[Back to all eight prompts](./README.md)
