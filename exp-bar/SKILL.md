---
name: exp-bar
description: Use when the user wants to capture worked examples, mistakes, fixes, and lessons learned from Kotlin and Android development into a structured experience note. Apply this skill after solving a Kotlin or Android problem to summarize the problem, plan, solution, result, level-up, and extracted reusable skill in a dedicated markdown note that strengthens future work alongside android-stack and kotlin-core.
---

# Exp Bar

Use this skill after a Kotlin or Android task is solved and the user wants to turn the work into reusable experience.

This skill is intentionally short. Its job is not to solve the coding task itself. Its job is to convert the finished struggle into a clean experience note.

This skill is the learning and level-up companion to:

- `android-stack` for Android app architecture and implementation
- `kotlin-core` for Kotlin language and design decisions

`exp-bar` should not replace them. It should learn from the work done through them.

Before promoting any lesson into `references/` or `SKILL.md`, follow:

- `process.md`

That file is the source of truth for:

- where new knowledge should go
- when a lesson stays note-only
- when a lesson can be promoted
- how to avoid duplicates
- how to keep the system compact and stable

## Purpose

Capture:

- what went wrong
- what we thought we would do
- what we actually did
- what finally worked
- what changed in understanding
- what reusable rule or pattern we gained

Limit the scope to:

- Kotlin language decisions
- Android architecture decisions
- Compose / ViewModel / Flow / Hilt / Retrofit / Room / Navigation issues
- debugging lessons that will matter again in Kotlin or Android work

Do not use this skill for unrelated topics unless the user explicitly wants that.

## Output location

Write notes only inside this skill's own notes folder:

- `exp-bar/notes/`

Do not spread notes across extra learning folders. Keep the memory centralized here.

## Core workflow

### Step 0: Only run after meaningful progress

Use this skill when at least one of these is true:

- the bug is fixed
- the feature is working
- the architecture decision is settled
- a useful failed path taught us something reusable

Do not use this skill for half-formed noise.

If the experience is not reusable, do not write a note.

### Step 1: Extract the raw experience

Capture the task in this order:

1. `Problem`
2. `Plan`
3. `Attempts`
4. `Solution`
5. `Result`
6. `Exp Bar`
7. `Lvl Up`
8. `Skill +1`

### Step 2: Filter for signal

Keep:

- repeated mistakes
- non-obvious fixes
- architecture decisions
- debugging patterns
- naming or modeling lessons
- tool or workflow discoveries

Drop:

- one-off noise
- emotional filler
- command spam
- details that will not help in future work

### Step 3: Write one note per meaningful lesson

Prefer one focused note over one giant diary entry.

Good note themes:

- `flow-vs-suspend`
- `room-migration-gotcha`
- `compose-state-hoisting-rule`
- `retrofit-dto-normalization`
- `workmanager-retry-policy`

### Step 4: Connect the lesson to the existing skills

Before writing the note, decide whether the lesson belongs closer to:

- `android-stack`
- `kotlin-core`
- both
- neither, and should remain just an experience note

If the lesson clearly strengthens an existing rule from `android-stack` or `kotlin-core`, say so in the note.

Do not rewrite those skills from inside `exp-bar`. Just record the learned signal cleanly so it can later be promoted if it repeats.

### Step 5: End with reusable extraction

Every note should end with:

- what to repeat next time
- what to avoid next time
- what rule became clearer

### Step 6: Maintain one index

Keep an index file in:

- `exp-bar/notes/index.md`

Whenever a new note is added, append a short entry:

- note title
- short topic label
- which base skill it relates to: `android-stack`, `kotlin-core`, or both

The index should stay compact and scannable.

### Step 7: Do not promote casually

If the user wants to strengthen the base skills, consult:

- `process.md`

Do not add new guidance directly into `kotlin-core` or `android-stack` unless the promotion rules in `process.md` are satisfied.

## Note template

Use this markdown structure:

```md
# Title

## Problem

What was broken, unclear, or hard?

## Plan

What did we think we were going to do?

## Attempts

- Attempt 1
- Attempt 2
- Attempt 3

## Solution

What finally worked?

## Result

What is now true after the fix?

## Exp Bar

What concrete experience did we gain?

## Lvl Up

What understanding became sharper?

## Skill +1

What reusable rule, pattern, or instinct should carry into future tasks?

## Related Base

Which existing base does this reinforce?

- `android-stack`
- `kotlin-core`
- both
- note only
```

## Naming guidance

Use short descriptive filenames:

- `flow-vs-suspend.md`
- `ui-state-loading-pattern.md`
- `dto-entity-domain-boundary.md`

Avoid:

- `notes1.md`
- `misc-fix.md`
- `stuff-we-did.md`

## Quality bar

A good note should let future us answer:

- Have we seen this before?
- What worked last time?
- What mistake should we skip?
- What decision rule did we earn?

It should also answer:

- Does this strengthen `android-stack`, `kotlin-core`, or stay as local experience only?

## Output expectations

- Keep notes compact and high-signal.
- Prefer reusable insights over storytelling.
- Write in a way that makes future implementation faster.
- Keep all learning inside `exp-bar/notes`.
- Prefer Kotlin and Android experience over generic software journaling.
