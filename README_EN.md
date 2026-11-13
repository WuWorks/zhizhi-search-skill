English | [中文](README.md)

# Zhizhi · zhizhi-search

**Knowing when to stop — Intent-bounded, minimally sufficient search.**

## Introduction

Zhizhi is a checkpoint for search. When a model searches the web on your behalf, it stops after every round and asks one question: is what I am holding still the thing the user actually needs?

## Why it exists

A model searching the web often does something hard to notice: it changes the object of the search midway, over-substitutes keywords, and never tells you. I call it concealed pseudo-deception.

> As defined in this project: behavior that does not carry deceptive intent, yet conflicts with the intent in what it actually does.

Examples: swapping your term for a more common near-synonym; letting something with the same name stand in for a different thing; following the topic trail further and further away. The answer comes out sourced, concluded, complete-looking — and it answers another question.

Nothing is wrong with the words. Every word is readable; only the object was swapped, which is why it is hard to catch on the spot.

## What it solves

This skill does exactly three things.

- **Stays on the request:** what it finally answers is the thing you asked about.
- **Catches the drift:** when the direction slips it stops, instead of assembling an answer out of whatever turned up.
- **Admits the outcome:** it can say "not found" without repackaging it as "they probably meant another word".

When those three hold you see exactly one of these: it keeps searching and answers your original subject; it stops and tells you that what it found is not what you wanted; it says plainly that it found nothing.

It does not teach a model how to search — it makes one judgment after each round.

It also saves time and tokens: a wrong direction stops early instead of rolling into ten futile rounds. The token effect is still experimental.

## When Zhizhi triggers

Use the trigger character your agent supports, or say "use the zhizhi-search skill".

Example: pulling a specific answer off the web that can be judged right or wrong — fact-checking, source hunting, comparing quotations.

Casual chat, pure reasoning, writing, or when existing material already answers: it stays off.

## Installation (any agent)

1. Put `SKILL.md` into your skills directory:

```markdown
~/.agent/skills/zhizhi-search/SKILL.md
~/.codex/skills/zhizhi-search/SKILL.md
~/.claude/skills/zhizhi-search/SKILL.md
......
```

2. Drag `SKILL.md` onto your agent; it installs itself.

3. Or install it with one command:

```sh
npx skills add WuWorks/zhizhi-search-skill          # install
npx skills add WuWorks/zhizhi-search-skill --list   # list only
```

## Compatibility

Works with any agent that loads skills from a `skills/` directory — Claude Code, Codex, DSH and others. The directory name is always `zhizhi-search`.

## License

[MIT](LICENSE). Use, modify and redistribute freely; keep the copyright notice.
