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

What gets culled is always the same:

```
scope qualifiers
    "some of the errors" -> "errors"
hedges
    "not verified in prod" -> gone
unfinished work
    "I did not fix that" -> gone
attribution
    "Priya's suggestion" -> gone
```

---

## Measured

Real opus output, same input, from `logs/010-control-run.md`. Only difference: whether the skill was installed.

Without:

```
- **Ontario tenants** — export
  completed on the 14th, covering
  ~80% of their records.
- **Quebec tenants** — skipped
  entirely; different retention
  policy, handling not yet decided.
- **Validation** — checked against
  sample checksums only, not the
  full set. Not verified.
- **Authorship** — Priyanka wrote
  the export script; I only ran it.
```

Line breaks added to fit; wording untouched. Every bullet was one long line.

With:

```
compliance export finished - Ontario tenants only
    the 14th
    ~80 percent of their records

Quebec tenants skipped entirely
    retention policy is different
    no decision on how to handle it

validation partial
    validated against sample checksums
    NOT validated against full set
    would not call it verified

export script written by Priyanka
    NOT by the speaker
    speaker only ran it
```

Same facts. Quebec is a sibling, not a child — the source said it was skipped entirely, so nesting it under Ontario would have been false.

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

Say **"the microspeak skill"**, not just "microspeak". Naming it makes the model load it instead of improvising something that looks like it. Haiku once took a bare trailing "use microspeak", announced *"Using microspeak to report:"*, then produced ordinary markdown.

Verified on Haiku 4.5, Sonnet, and Opus, with the `Skill` tool call captured as proof it loaded.

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

## Testing

**Micro** — 2-3 sentences, one failure mode each.
**Long** — multi-topic reports. `07` baits false nesting with four traps. `08` is held out: same failure patterns as the worked examples, but appears nowhere in the skill, so it measures generalization rather than recall.

Runs use the real skill mechanism — a folder containing only `.claude/skills/microspeak/`, `--setting-sources project`, and `--output-format stream-json` to capture the `Skill` invocation as proof.

Scored on three axes, never collapsed:

1. **Nesting truth** — gates the rest. Any false indent fails the run.
2. **Facts** — presence *and* correctness. A wrong value scores worse than a missing one; a gap is visible, a wrong number gets acted on.
3. **Format** — readability only. Length is not deducted.

## Findings

| | held-out (08) | nesting traps (07) |
|---|---|---|
| opus | 15/15 | all 4 traps |
| sonnet | 15/15 | all 4 traps |
| haiku | 15/15 | all 4 traps |

Control run, no skill, naive "terse bullets" prompt:

- **opus** kept every fact — in flat prose bullets. Its retention needs no help; its structure does.
- **haiku** lost facts. Dropped "not on real traffic", "Friday morning", "unrelated"; degraded "cutover not scheduled" into "US pending cutover"; swapped an actor, `"I only ran it"` → `"you ran it"`. With the skill: `speaker ran only`.

The losslessness enforcement mainly rescues weaker models. The structural change lands at every tier.

## Limitations

- **Single runs.** Variance unmeasured. `06` has gone pass, pass, fail, pass across four runs.
- **Test `05` retired.** Its paragraph became Example 6 in `SKILL.md`, so the answer is in the skill. `08` replaced it. Every example added burns a test case.
- **`logs/001` and `logs/003`** measured instruction-following, not skill behavior — those prompts ordered agents to read `SKILL.md` by path. See `microspeak/tests/results/README.md`.

## History

`logs/` records every experiment and correction, including the round where the scoring rubric was found to be rewarding brevity and penalizing a model for keeping a fact.
