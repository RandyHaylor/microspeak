# MicroSpeak

A Claude Code skill for dense, lossless reporting — nested fragments with no filler and no dropped information.

```
fragments over sentences
indentation over connectives
zero words dropped that carry meaning
zero words kept that do not
```

---

## The problem this solves

Ask an LLM for a status update and you get prose. Ask it to be brief and it drops facts. There is no prompt in between that reliably gives you both.

The casualties are always the same, and always the ones that matter most:

```
scope qualifiers   "some of the errors"  ->  "errors"
hedges             "not verified in prod" -> gone
unfinished work    "I did not fix that"   -> gone
attribution        "Priya's suggestion"   -> gone
```

Losing "some of" turns a partial fix into a complete one. Losing "I did not fix that" turns an open bug into a closed one. The reader has no way to notice, because everything still on the page reads as true.

## The example

prose

```
I merged in a couple prs for the api-gateway and admin-portal repos
```

microspeak

```
merged prs
    api-gateway
    admin-portal
```

"a couple" is gone because the list carries the count. Nothing else is.

---

## Before and after, measured

Both of these are real opus output on the same input, from `logs/010-control-run.md`. The only difference is whether the skill was installed.

**Without the skill**, prompted "condense this into terse bullets":

```
**Compliance export status**

- **Ontario tenants** — export completed on the 14th, covering ~80% of their records.
- **Quebec tenants** — skipped entirely; different retention policy, handling not yet decided.
- **Validation** — checked against sample checksums only, not the full set. Not verified.
- **Authorship** — Priyanka wrote the export script; I only ran it.
```

Every fact is present. It is also full sentences with periods, semicolons joining two ideas per line, and no hierarchy at all.

**With the skill**, prompted "convert this to microspeak":

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

Same facts. Scannable in two seconds. Quebec is a sibling of the Ontario export, not a child of it — the source said it was skipped entirely, so nesting it under Ontario would have been a lie.

---

## Install

```
cp -r microspeak ~/.claude/skills/
```

or per-project

```
cp -r microspeak .claude/skills/
```

Then just say it:

```
convert this to microspeak
```

Verified on Claude Haiku 4.5, Sonnet, and Opus — all three discover and invoke the skill from that phrase alone, with the `Skill` tool call captured in the transcript as proof.

The trailing form `use microspeak` appended to a work request is less reliable. Haiku once ignored it entirely, announced "Using microspeak to report:", and then produced ordinary markdown. That was against an early version of the skill and has not been re-tested since. Lead with the phrase rather than tacking it on the end.

---

## What the skill enforces

**Losslessness.** An explicit KEEP list guards scope qualifiers, hedges, negations, attribution, quoted strings, and anything that looks redundant but is not. `"not done"` and `"still needed"` are two different facts — work can be undone *and* cancelled.

**Nesting truth.** Every indent asserts that the child is *part of / caused by / a detail of / evidence for* the parent. That assertion has to be true. A wrong parent produces a document where every line is true and the document is false, which is worse than an omission — an omission leaves a visible gap.

The check is mechanical: read each indent aloud as `"<child> is part of <parent>"`. False or unsupported, re-parent it. Unsure, make it a sibling.

**Split, don't trim.** Line length is deliberately not scored. A long line usually means two ideas jammed together, and the fix is a parent and a child, not fewer words. Shorter is explicitly not the goal.

---

## Repo layout

```
microspeak/SKILL.md          the skill
microspeak/tests/            test inputs and scoring keys
    micro/                   4 short tests, one failure mode each
    long/                    multi-topic tests, incl. nesting traps
    results/                 raw model output, verbatim
    SCORING.md               how to score a run
logs/                        breadcrumb history, 000 through 010
CLAUDE.md                    the original project brief
```

## Testing

Two suites, both scored against fixed keys.

**Micro** — 2-3 sentences, one failure mode apiece: scope qualifier, state-vs-requirement, unrelated topics, hedge and attribution. Fast to iterate on.

**Long** — multi-topic reports. `07` is built to bait false nesting with four specific traps. `08` is held out: it carries the same failure patterns as the worked examples in `SKILL.md` but appears nowhere in the skill, so it measures generalization rather than recall.

Runs go through the real skill mechanism — a folder containing only `.claude/skills/microspeak/`, `--setting-sources project` to exclude user-level skills, and `--output-format stream-json` to capture the `Skill` tool invocation as proof the skill actually loaded rather than the model improvising from the word "microspeak."

### Scoring

Three independent scores, never collapsed into one number.

1. **Nesting truth**, scored first and gates the rest. Any FALSE indent fails the run outright.
2. **Facts** — presence *and* correctness. A present fact with a wrong value scores worse than a missing one; a missing fact leaves a gap the reader can see, a wrong one gets acted on.
3. **Format** — deductions only for things that hurt readability. Length is not among them.

---

## Findings

| | held-out test (08) | nesting traps (07) |
|---|---|---|
| opus | pass 15/15 | pass, all 4 traps |
| sonnet | pass 15/15 | pass, all 4 traps |
| haiku | pass 15/15 | pass, all 4 traps |

**The control run is the honest part.** With no skill installed and a naive "terse bullets" prompt:

- **opus kept every fact** on both tests — but in flat prose bullets. Its fact-retention needs no help; its *structure* does.
- **haiku lost facts.** It dropped "not on real traffic", "Friday morning", and "unrelated", degraded "cutover not scheduled" into "US pending cutover", and swapped an actor — `"I only ran it"` became `"you ran it"`. With the skill it wrote `speaker ran only`, correctly.

So the value splits: the losslessness enforcement mainly rescues weaker models, while the structural change lands at every tier.

## Known limitations

- **Haiku regresses on one long input** (`06`), nesting `"most workloads moved"` under `"completed"`. Judged a haiku limitation rather than chased further.
- **Test `05` is retired.** Its paragraph became Example 6 in `SKILL.md`, so the answer is now in the skill. `08` replaced it. This is a standing cost of the add-an-example approach: every example burns a test case, so each one needs a fresh held-out replacement.
- **Single runs.** No repetition, so run-to-run variance is unmeasured. The control used one naive phrasing on two models and two tests.
- Early results in `logs/001` and `logs/003` came from prompts that ordered agents to read `SKILL.md` by path. Those measure instruction-following, not skill behavior. `microspeak/tests/results/README.md` says which files are which.

## History

`logs/` is a full breadcrumb trail — every experiment, every wrong turn, and the corrections. Including the round where the scoring rubric was found to be rewarding brevity, and penalized a model for keeping a fact.
