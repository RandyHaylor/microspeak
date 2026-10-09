---
name: microspeak
description: |
  Dense lossless output format
      - Nested fragments
      - Zero filler
      - Zero facts lost
      - Bullets and headers: the destination's standard syntax
      - Generous blank lines, like a textbook

  Trigger: Apply it to whatever was asked for, nothing else
      - "Use microspeak"/"brief bullets"/etc. -> your replies, until told otherwise
      - "Use microspeak for X" -> that X only (may be a specific reply, a doc, or other)
          - Your replies stay normal prose

---

Bullet syntax in this file is illustrative
	- NOT a required format
	- Use the standard list syntax of wherever the output goes
		- Rendered markdown -> markdown lists and headings
		- Slack, email, code comments -> their own conventions
	- Nothing specified -> the plain default below
		- Base item at column 0
		- Tab + "-" per depth


MicroSpeak AI agent skill
	- Guides efficient output
	- Prevents loss of
		- Nuance
		- Detail


Prose converted to microspeak
	- "I merged in a couple prs for the api-gateway and admin-portal repos"
	- Becomes:
		- I merged prs
			- api-gateway
			- admin-portal


Rules for shaping a response
	- Base items at column 0
		- Each a phrase clear on its own
		- Children may be terse
			- Parents supply the subject
	- Whitespace is for the human reader
		- Blank line between base items
		- Two blank lines between sections
	- Capitalize each line
	- Quoted strings and identifiers verbatim
	- Over 3 base items
		- Group areas under headers
		- Close with a "Response summary" header
			- Areas only


Never lose a detail
	- Keep
		- Qualifiers
		- Hedges
		- Negations
		- Who did it, including I / we / you
		- Attribution
		- Numbers
		- Quoted strings
		- Unfinished work
	- Long line = two ideas
		- Split to parent + child


## Format

Plain default, when the destination sets no syntax

```
=== Subject Header ===

Base item one
	- Phrase here
	- Another update
		- Its detail
		- Another detail
			- Deeper still

Base item two
	- Detail


=== Response summary ===

- Subject Header
```

Same shape in rendered markdown

```markdown
## Subject Header

Base item one
- Phrase here
- Another update
  - Its detail
  - Another detail
    - Deeper still

Base item two
- Detail


## Response summary

- Subject Header
```

## Rules

```
Every fact survives
	- Never cut one to shorten

Base items sit at column 0
	- No bullet
	- A phrase clear with nothing else on screen
		- "Output" says nothing
		- "Dense lossless output format" does
	- A run of bare labels means it is a list
		- Put it under one parent

Children are read with their ancestors
	- And with their own siblings
		- A list or a sequence reads as a set
	- NOT with aunts and uncles
	- NOT with any other branch
	- Terse is correct
		- The parent supplies the subject

Bullets match the destination
	- Markdown, Slack, a code comment -> its standard list syntax
	- No exotic markers
	- Nothing specified -> tab + "-" per depth

Whitespace makes it scannable
	- Picture a textbook page
	- Blank line between base items
	- Blank line after a header
	- Two blank lines before the next header
	- Never pack sections edge to edge

Capitalize each line
	- Quoted strings and identifiers stay verbatim

Headers group a long response
	- Over 3 base items only
	- The destination's heading syntax
		- Markdown -> ##
		- Plain text -> === Header ===
	- Names the area, not the findings
	- Adds no indent level
	- Close with a "Response summary" header
		- Areas only, never findings
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
	- Name the state they share, or make both base items
	- Wrong - "US still on old index" holding "Cutover NOT scheduled"
	- Wrong - "US region", a bare label
	- Right - "US cutover still pending" holding both
	- Wrong - "Finished on time" holding "Silently skipped 40 rows"
		- Success does not contain failure

A parent may be invented to name a topic
	- It must add no claim of its own
	- Build it from the source's own words
		- Source said "cutover", so not "migrated"
	- No source word for the state? Do not invent one
		- Source said "planned", so not "pending"
		- Use two base items instead

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
		- Including I / we / you
		- "I rewrote it" -> "I rewrote it", not "it was rewritten"
	- A qualifier
		- "some"
		- "most"
		- "partially"
	- A hedge
		- "probably"
		- "not verified"
	- Half of a contrast
		- "his call, not mine"
	- A fact that only looks redundant
		- "not done" and "still needed" differ
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
		- Not load

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

## Worked example, long response

Prose

```
Quick update on the release. The payments service migration to the new
queue is done in staging and I've run the load test twice; p95 latency
dropped from 420ms to 180ms, but the second run had three timeouts I
haven't explained yet. Production cutover is scheduled for Thursday
pending Dana's sign-off. On the mobile side, the iOS build is blocked on
the expired signing certificate. Marco said he'd renew it today but I
haven't heard back. Android is fine. For docs, I updated the API
reference for the two new endpoints but not the migration guide, which
still describes the old queue.
```

MicroSpeak, plain default

```
=== Payments ===

Queue migration done in staging
	- I ran the load test twice
	- p95 latency 420ms -> 180ms

Second load test run had 3 timeouts
	- I have NOT explained them yet

Production cutover scheduled Thursday
	- Pending Dana's sign-off


=== Mobile ===

iOS build blocked
	- Signing certificate expired
	- Marco said he'd renew it today
		- I have not heard back

Android fine


=== Docs ===

I updated the API reference
	- Two new endpoints

Migration guide NOT updated
	- Still describes the old queue


=== Response summary ===

- Payments
- Mobile
- Docs
```

One section of it in rendered markdown

```markdown
## Mobile

iOS build blocked
- Signing certificate expired
- Marco said he'd renew it today
  - I have not heard back

Android fine
```

What survives that usually does not

```
"I haven't explained yet"
	- The timeouts stay open work, not a footnote

"pending Dana's sign-off"
	- Thursday is conditional

"I haven't heard back"
	- Renewal promised, NOT confirmed

The migration guide
	- Untouched work gets its own base item
```

## Before sending

```
Every base item clear alone?
Every indent true?
Every fact from the source present?
Every hedge and qualifier intact?
Any comma-run left to split?
Bullets in the destination's syntax?
Blank lines between items and sections?
No preamble, no sign-off?
```
