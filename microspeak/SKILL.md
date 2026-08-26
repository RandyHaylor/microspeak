---
name: microspeak
description: |
  Dense lossless output format
      - Nested fragments
      - Zero filler
      - Zero facts lost

  Trigger: Apply it to whatever was asked for, nothing else
      - "Use microspeak"/"brief bullets"/etc. -> your replies, until told otherwise
      - "Use microspeak for X" -> that X only (may be a specific reply, a doc, or other)
          * Your replies stay normal prose

  Prose converted to microspeak
      - "I merged in a couple prs for the api-gateway and admin-portal repos"
      - Becomes:
          * I merged prs
              - api-gateway
              - admin-portal

  Rules for shaping a response
      - Base items at column 0
          * Blank line between
          * Each a phrase clear on its own
          * Children may be terse
              - Parents supply the subject
      - Bullets alternate - then * by depth
      - Capitalize each line
      - Quoted strings and identifiers verbatim
      - Over 3 base items
          * Wrap each area in === Header ===
          * Close with === Response summary ===
              - Areas only

  Never lose a detail
      - Keep
          * Qualifiers
          * Hedges
          * Negations
          * Who did it, including I / we / you
          * Attribution
          * Numbers
          * Quoted strings
          * Unfinished work
      - Long line = two ideas
          * Split to parent + child
---

# MicroSpeak

## Format

```
=== Subject Header ===

Base item one
    - Phrase here
    - Another update
        * Its detail
        * Another detail
            - Deeper still

Base item two
    - Detail

=== Response summary ===

- Base item one
- Base item two
```

## Rules

```
Every fact survives
    - Never cut one to shorten

Base items sit at column 0
    - No bullet
    - Blank line between
    - A phrase clear with nothing else on screen
        * "Output" says nothing
        * "Dense lossless output format" does
    - A run of bare labels means it is a list
        * Put it under one parent

Children are read with their ancestors
    - And with their own siblings
        * A list or a sequence reads as a set
    - NOT with aunts and uncles
    - NOT with any other branch
    - Terse is correct
        * The parent supplies the subject

Bullets alternate by depth
    - Depth 1 dash
    - Depth 2 asterisk
    - Depth 3 dash, and so on

Capitalize each line
    - Quoted strings and identifiers stay verbatim

Headers group a long response
    - Over 3 base items only
    - Blank line before and after
    - Names the area, not the findings
    - Adds no indent level
    - Close with === Response summary ===
        * Areas only, never findings
```

## Nesting is a claim

```
An indent asserts the child is
    - Part of the parent
    - Or caused by it
    - Or a detail of it
    - Or evidence for it

Read every indent aloud
    - "<child> is part of <parent>"
    - False or unsupported -> re-parent it
    - Unsure -> make it a sibling

A false parent is fabrication
    - Run the indent test, proofreading will not catch it

A detail belongs to what it is ABOUT
    - Not what it was mentioned NEAR

Name the parent to fit its children
    - "EU rollout" cannot hold "US still on old index"
    - Widen the name, or split into siblings

Peers never parent each other
    - Two facts at the same level of detail are siblings
    - Promoting one to hold the other is a false claim
    - Name the state they share, or make both base items
    - Source: "US is still on the old index and I have not scheduled the cutover"
        * Wrong - "US still on old index" holding "Cutover NOT scheduled"
        * Wrong - "US region", a bare label
        * Right - "US cutover still pending" holding both
    - Source: "finished on time but silently skipped 40 rows"
        * Wrong - "Finished on time" holding "Silently skipped 40 rows"
            - Success does not contain failure
        * Right - both as base items under === Nightly export ===

A parent may be invented to name a topic
    - It must add no claim of its own
    - Build it from the source's own words
        * Source said "cutover", so use cutover
        * "Not yet migrated" imports a word the source never used
    - If no source word names the shared state, do NOT invent one
        * Source: "on the old schema version and nobody has planned the upgrade"
        * Wrong - "Schema upgrade pending", source never said pending
        * Right - two base items, no parent invented

Orphan check, after placing every detail
    - Read each base item alone
    - Does it still carry its own open work
    - Thinner than the source means a detail went elsewhere
```

## Cut only filler

```
The structure already states
    - Ownership, so drop "of" and "'s"
    - Causality, so drop "because" and "so"
    - Order, so drop "then" and "after that"

Always drop
    - "Basically"
    - "Just"
    - "Simply"
    - "It turns out that"
    - Vague counts of things you then list
    - Articles when unambiguous

Never drop
    - Who did it
        * Including I / we / you
        * "I rewrote it" -> "I rewrote it", not "it was rewritten"
    - A qualifier
        * "some"
        * "most"
        * "partially"
    - A hedge
        * "probably"
        * "not verified"
    - Half of a contrast
        * "his call, not mine"
    - A fact that only looks redundant
        * "not done" and "still needed" differ
    - Anything unfinished or untouched

A comma-separated list is three ideas
    - Split it into bulleted children
```

## Worked example

Prose

```
I bumped the S3 retry count from 3 to 5 on the platform team's
suggestion, though I doubt it fixes the timeouts since the failures we
saw were permission errors rather than load. I did not touch the parquet
writer, which is still the slowest step.
```

MicroSpeak

```
I raised the S3 retry count 3 -> 5
    - Platform team's call, not mine
    - I doubt it fixes the timeouts
    - Failures were permission errors
        * Not load

Parquet writer NOT touched
    - Still the slowest step
```

What survives that usually does not

```
"not mine"
    - Kept, not collapsed to "platform team's call"

The doubt and its reason
    - Both, not just the doubt

The untouched item
    - Its own base item
    - NOT a child of the retry change
```

## Before sending

```
Every base item clear alone?
Every indent true?
Every fact from the source present?
Every hedge and qualifier intact?
Any comma-run left to split?
No preamble, no sign-off?
```
