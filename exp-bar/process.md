# exp bar process

This file defines the full learning loop for Kotlin and Android work.

Its job is to prevent:

- noisy note-taking
- premature edits to core skills
- duplicated rules
- random placement of new knowledge
- confusion between raw experience and stable guidance

## system roles

There are three layers in this system:

### 1. Raw experience

Location:

- `exp-bar/notes/`

Purpose:

- store solved problems
- capture mistakes, attempts, fixes, and lessons
- preserve signal from real work before it is promoted

### 2. Refined guidance

Location:

- `kotlin-core/references/`
- `android-stack/references/`

Purpose:

- store repeated and useful rules
- hold detail that is too large for `SKILL.md`
- explain patterns, edge cases, and decision logic

### 3. Core rules

Location:

- `kotlin-core/SKILL.md`
- `android-stack/SKILL.md`

Purpose:

- store only the most stable, high-frequency guidance
- define how the skill should think
- stay compact and structural

## the learning loop

### Phase 1: Solve the task

Use:

- `android-stack` for Android architecture and app implementation
- `kotlin-core` for Kotlin language and design decisions

Do not write learning notes while the task is still unresolved unless the failed path is already clearly reusable.

### Phase 2: Capture the experience

After meaningful progress, use `exp-bar`.

Create one focused note in:

- `exp-bar/notes/`

Use the note template:

- `Problem`
- `Plan`
- `Attempts`
- `Solution`
- `Result`
- `Exp Bar`
- `Lvl Up`
- `Skill +1`
- `Related Base`

### Phase 3: Index the note

Every created note must also be added to:

- `exp-bar/notes/index.md`

Each index line should remain short and answer:

- what the note is about
- which base it relates to

### Phase 4: Wait before promotion

Do not immediately edit `kotlin-core` or `android-stack` after one note.

The note should first prove that it is:

- reusable
- repeated
- general enough

## promotion rules

This system has three promotion levels.

### Level A: Note only

Keep a lesson only in `exp-bar/notes` when:

- it is tied to one project
- it is a one-off bug
- it is too specific
- it is useful history but not a general rule

### Level B: Promote to references

Promote a lesson from note to `references/` when:

- it repeated at least twice
- it is a decision pattern
- it explains an edge case well
- it is useful but too detailed for `SKILL.md`

This is the default promotion path for most good lessons.

### Level C: Promote to SKILL.md

Promote a lesson into `SKILL.md` only when:

- it repeated several times
- it changes future implementation behavior often
- it is stable across projects
- it belongs to the core way the skill should reason

Only core rules belong here.

## where new knowledge goes

Use these placement rules.

### Add to `kotlin-core/SKILL.md` only if

The lesson is about:

- Kotlin language choices
- null-safety
- coroutines and Flow at language or API level
- Kotlin API design
- serialization boundaries in a general Kotlin sense
- testing logic that applies broadly across Kotlin projects

### Add to `android-stack/SKILL.md` only if

The lesson is about:

- Compose and screen boundaries
- ViewModel and `UiState`
- repository and use case design in Android apps
- Hilt, Room, Retrofit, Navigation architecture decisions
- Android-specific layering and state flow

### Add to `references/` if

The lesson is:

- detailed
- procedural
- example-heavy
- edge-case-heavy
- useful but not core

### Keep as note only if

The lesson is:

- too narrow
- too fresh
- too project-specific
- still unproven

## anti-duplication rules

Before promoting any lesson:

1. Check if the same idea already exists in the target `SKILL.md`
2. Check if it already exists in the target `references/`
3. Check `exp-bar/notes/index.md` for earlier similar notes

If the idea already exists:

- do not add a duplicate line
- either strengthen the old wording
- or add the new note as supporting evidence only

## quality gate for promotion

Before adding any new line to a core skill, ask:

1. Did this repeat?
2. Is this reusable outside one project?
3. Is this a rule, not just an incident?
4. Is this not already covered?
5. Is this core enough for `SKILL.md` instead of `references/`?

If the answer is not clearly yes, do not promote it.

## frequency thresholds

Use this default threshold model:

- 1 useful occurrence -> note only
- 2 repeated occurrences -> candidate for `references/`
- 3 or more repeated occurrences -> candidate for `SKILL.md`

These are heuristics, not laws, but they are the default.

## what not to store in core skills

Do not push these into `SKILL.md`:

- command history
- emotional narrative
- project-specific hacks
- temporary library workarounds
- detailed debugging timeline
- long examples that belong in notes or references

## what counts as a core-skill line

A new line in `SKILL.md` should usually be one of:

- a decision rule
- an anti-pattern
- a boundary rule
- a modeling heuristic
- a stable architectural principle

If it is not one of these, it probably does not belong in `SKILL.md`.

## review rhythm

Use this maintenance rhythm:

- after each meaningful solved task -> write or update a note
- after several related notes accumulate -> review for promotion
- only then edit `references/` or `SKILL.md`

This keeps the system stable and prevents chaotic growth.

## the final principle

`exp-bar` is the intake buffer.

`references/` are the refinement layer.

`SKILL.md` is the compressed brain.

Do not skip levels unless a lesson is obviously foundational.
