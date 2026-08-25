# MicroSpeak

A Claude Code skill that transforms this:

```
I merged in a couple prs for the
api-gateway and admin-portal repos
```

into this:

```
merged prs
    api-gateway
    admin-portal
```

Consistently, and without losing important detail.

---

## The problem

Standard output is verbose prose, which can be massive and hard to digest for complex technical topics. If you ask for terse, bulleted output, a lot of nuance and detail is culled. This skill fixes that with a proven set of examples and instructions to align the agent to use a full detailed but efficient output format.

### Example

Standard prose output:

```
I bumped the S3 retry count from 3 to
5 on the platform team's suggestion,
though I doubt it fixes the timeouts
since the failures we saw were
permission errors rather than load.
```

Asked for terse bullets:

```
- Bumped S3 retry count from 3 to 5
```

Asked to use the microspeak skill:

```
S3 retry count 3 -> 5
    platform team's suggestion
    may not fix timeouts
    errors were permission, not load
```

Details lost without microspeak:

```
whose call it was
the doubt it helps
why it may not
```

---

## Install

```
cp -r microspeak ~/.claude/skills/
```

or per-project

```
cp -r microspeak .claude/skills/
```

Ask for it by name:

```
use the microspeak skill
convert this to microspeak
```

Say **"the microspeak skill"**, not just "microspeak" — naming it makes the model load the skill rather than improvise something that looks like it.

---

## What it enforces

- **Losslessness.** Qualifiers, hedges, negations, attribution and verbatim strings are preserved, as are facts that appear redundant but aren't — "not done" and "still needed" are distinct claims, since work can be both undone and cancelled.
- **Nesting is semantic.** An indent asserts the child is part of, caused by, a detail of, or evidence for its parent. A false parent produces a document in which every line is individually true and the whole is false — a failure that survives proofreading, because there is no incorrect line to find.
- **Attachment follows subject, not proximity.** Prose serialises everything onto one line, so a detail routinely sits adjacent to a topic it does not belong to. Placement is decided by what the detail is about.
- **Length is not a target.** A long line means two ideas sharing one line, resolved by splitting into parent and child. Connectives and filler fall away, because the structure already encodes ownership, causality and order. Facts do not.

---

## Layout

```
microspeak/SKILL.md
    the skill
microspeak/tests/
    inputs, keys, raw output
logs/
    history, 000-011
CLAUDE.md
    original brief
```

## Model support

Verified on Claude Haiku 4.5, Sonnet, and Opus.

Test inputs and scoring keys are in `microspeak/tests/`. `logs/` records the development history — every experiment, result, and revision.
