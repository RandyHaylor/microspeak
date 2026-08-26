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
          * Merged prs
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
    - Shorter is never the goal
    - A longer correct answer beats a shorter lossy one

Base items
    - Column 0, no bullet, blank line between
    - A phrase clear with nothing else on screen
        * "Output" says nothing
        * "Dense lossless output format" does
    - A run of bare labels means it is a list
        * Put it under one parent

Children
    - Read with their ancestors, never their siblings
    - Terse is correct, the parent supplies the subject

Bullets alternate by depth
    - Depth 1 dash
    - Depth 2 asterisk
    - Depth 3 dash, and so on

Capitalize each line
    - Quoted strings and identifiers stay verbatim

Headers
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
    - Every line true, document false
    - No wrong line for proofreading to catch

A detail belongs to what it is ABOUT
    - Not what it was mentioned NEAR
    - Prose order is not a relationship

Name the parent to fit its children
    - "EU rollout" cannot hold "US still on old index"
    - Widen the name, or split into siblings
```

## Cut only filler

```
The structure already states
    - Ownership, so drop "of" and "'s"
    - Causality, so drop "because" and "so"
    - Order, so drop "then" and "after that"

Drop
    - I / we / you as subject
        * UNLESS it carries responsibility or attribution
    - "Basically", "just", "simply", "it turns out that"
    - Vague counts of things you then list
    - Articles when unambiguous

Never drop
    - A qualifier - "some", "most", "partially"
    - A hedge - "probably", "not verified"
    - Half of a contrast - "his call, not mine"
    - A fact that only looks redundant
        * "not done" and "still needed" differ
    - Anything unfinished or untouched

A comma-separated list is three ideas
    - Split it into children
    - Cramming scans worse
    - Line count is not a cost
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
