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

Standard prose output:

```
I bumped the S3 retry count from 3 to
5 on the platform team's suggestion,
though I doubt it fixes the timeouts
since the failures we saw were
permission errors rather than load.
```

Six details: what changed, the old value, the new value, whose call it was, the doubt that it helps, and why.

Asked for terse bullets:

```
- Bumped S3 retry count from 3 to 5
```

**4 of 6 details lost.**

Asked to use the microspeak skill:

```
S3 retry count 3 -> 5
    platform team's suggestion
    may not fix timeouts
    errors were permission, not load
```

**0 of 6 details lost.**

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

**Losslessness.** A KEEP list guards scope qualifiers, hedges, negations, attribution, quoted strings, and facts that only look redundant. `"not done"` and `"still needed"` are two facts — work can be undone *and* cancelled.

**Nesting truth.** Every indent asserts the child is *part of / caused by / a detail of / evidence for* the parent. A wrong parent makes a document where every line is true and the document is false — worse than an omission, which at least leaves a visible gap. The check: read each indent as `"<child> is part of <parent>"`. False or unsupported, re-parent it.

**Detail placement.** A detail belongs to what it is *about*, not what it was mentioned *near*. Prose runs in one line; adjacency is sentence order, not relationship.

**Split, don't trim.** Line length is not scored. A long line means two ideas jammed together — fix with a parent and a child, not fewer words. Shorter is explicitly not the goal.

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
