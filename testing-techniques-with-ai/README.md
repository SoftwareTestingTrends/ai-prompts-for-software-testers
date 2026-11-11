# Testing Techniques with AI

Eight prompts that use testing techniques to get better tests from an AI assistant, with ChatGPT's full answers and what we found when we checked them. They go with the video *Why Testers Still Need Testing Techniques When AI Writes the Tests* (link added when the video is published).

Every prompt uses the same example: a sign-up form where users must be between 18 and 65 years old to register.

## The idea

With AI, each testing technique does two jobs:

1. **It turns a vague request into a precise prompt.** Name the technique and give the rules it needs.
2. **It gives you a checklist for reviewing what comes back.** Check the answer with the same technique.

## How the prompts were run

- **Tool:** ChatGPT, default model (the app didn't show which), Thinking off.
- **Date:** 8 November 2026.
- **Method:** each prompt in a fresh chat, pasted exactly as written. The first answer was kept, unedited and not regenerated.

Your answers will differ, because AI tools give different answers from run to run. The review notes show what to check, whatever the answer says.

## The prompts

| # | Prompt | Technique |
|---|---|---|
| 1 | [A vague request](./01-vague-request.md) | None named |
| 2 | [Equivalence partitioning and boundary value analysis](./02-partitions-and-boundaries.md) | Equivalence partitioning, boundary value analysis |
| 3 | [Decision table](./03-decision-table.md) | Decision table testing |
| 4 | [Pairwise testing](./04-pairwise.md) | Pairwise (all-pairs) testing |
| 5 | [State transition testing](./05-state-transitions.md) | State transition testing |
| 6 | [Error guessing](./06-error-guessing.md) | Error guessing |
| 7 | [Exploratory testing charters](./07-exploratory-charters.md) | Exploratory testing |
| 8 | [White-box coverage gaps](./08-white-box-coverage.md) | Statement, branch and condition coverage |

## What happened, in short

ChatGPT was correct where the task was mechanical: the boundary values (prompt 2), the decision table (3), the pairwise set (4) and the coverage gaps in the code (8). Where it had to decide something, it made assumptions (65 included in prompt 1, extra rules in prompt 5), got one birth date wrong (prompt 1), or stayed generic (prompts 6 and 7). Each file says what we found and how we checked it.
