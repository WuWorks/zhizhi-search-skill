---
name: zhizhi-search
description: Use when the user needs a specific answer from the web and that answer can be judged right or wrong — fact-checking, source hunting, and looking up details all count. Also use after one or more rounds of searching when results start drifting away from what the user actually asked. Do not use for casual chat, pure reasoning, writing, or when existing material already answers.
license: MIT
version: 1.2.0
---

# Zhizhi · Drift Checkpoint for Search

**Core principle:** This is not a search method. It is a judgment you must pass after every round of searching — is what you are holding still the thing the user asked for?

## When to Use

- The user needs an answer that can be judged right or wrong, and you are about to search the web.
- You have searched one or more rounds and the results no longer match the user's original wording.
- You are about to rephrase the user's question and search again.

**Not for:** casual chat, pure reasoning, writing, or when existing material already answers.

## Core Pattern

**Before** (default behavior):

> The user asks where A comes from → you cannot find it → you swap A for a near-synonym B → you find plenty about B → you deliver an explanation of B. The user's subject was replaced, you answered a different question, and you never said so.

**After**:

> Round 1 searches A and returns only B → judge: drifted → stop and report “found B, not A itself” → end with one question asking whether to change direction.

## Quick Reference

| Verdict | Meaning | Next step |
|---|---|---|
| **Matched** | The result answers the thing the user asked | Continue |
| **Drifted** | It is not that thing | Stop; report what you found and why it is not it |
| **Not found** | No results | Say so; do not change the question |

## Implementation

Input: the user's original wording plus this round's results. Make one judgment after every round — three choices, never skipped, never merged.

### Hard constraints (violating any one voids the search)

1. **Do not change the main subject.** The main subject in the user's own wording must not be replaced. You may suggest alternatives, but a suggestion must be explicitly labeled as a suggestion and must not replace the user's direction during the search. Check: was the main subject swapped for another word or another object?
2. **Judge every round.** After each round of searching there must be one judgment — no skipping, no merging. Check: did each round leave a judgment?
3. **Do not re-search a judged path.** A path already judged “drifted” must not be walked again in an equivalent form. Check: was the same rejected path launched a second time?
4. **Say “not found” when it is not found.** Never turn “I cannot find it” into “they probably meant another word”. Check: did you report not-found as found, or substitute something else?

### Soft constraints (optional, but state in the delivery why you skipped them)

- Label second-hand sources as second-hand; open the evidence your conclusion depends on, and if you cannot open it, say so.
- Write `unknown` when you cannot judge; never “probably”.
- Stop after three equivalent rounds with no new evidence.

### Delivery

- **Matched:** one conclusion + one quotable, independently reproducible piece of evidence + source.
- **Drifted:** state what you actually found and where it differs from the request; end with one question (change direction / narrow it down) — one question, no follow-up, no answering for the user.
- **Not found:** state what you searched and where you stopped; end with the same one question.

A suggestion is only a suggestion: never let it replace the user's direction mid-search, and never deliver it as a conclusion.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Cannot find it, so swap the subject for a synonym and search again | Judge “drifted”, stop and report; if a swap is warranted, ask first |
| Treat “suggest changing direction” as the new direction and just search it | Label it as a suggestion and wait for the user |
| Judge “drifted”, then reword and walk the same path | Do not launch a rejected path again |
| Turn not-found into “they probably meant X” and answer X | Say not found; stay not found |
