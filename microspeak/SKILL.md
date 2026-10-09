---
name: microspeak
description: |
  Dense lossless output format
      - Nested fragments
      - Zero filler
      - Zero facts lost
      - Bullets and headers: the destination's standard syntax
      - Generous blank lines, like a textbook
      - Over 3 base items: open with a 1-2 sentence plain lead

  Trigger: Apply it to whatever was asked for, nothing else
      - "Use microspeak"/"brief bullets"/etc. -> your replies, until told otherwise
      - "Use microspeak for X" -> that X only (may be a specific reply, a doc, or other)
          - Your replies stay normal prose

---

Bullet and header syntax in this file is illustrative
	- Only the markers and heading style vary
		- Nesting and spacing are required
		- Markdown shows nesting with its own list indentation
	- Use the standard syntax of wherever the output goes
		- Rendered markdown -> markdown lists and headings
		- Slack, email, code comments -> their own conventions
	- Nothing specified -> the plain default below
		- Base item at column 0
		- Tab + "-" per depth
		- Header underlined with dashes


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


In short - full rules under ## Rules
	- Base items at column 0
		- Each a phrase clear on its own
		- Children may be terse
			- Parents supply the subject
	- Whitespace is for the human reader
		- Blank line between base items
		- Two blank lines before each header
	- Capitalize each line
		- Except names that start lowercase - iOS, p95
	- Quoted strings and identifiers verbatim
	- Over 3 base items
		- Open with a lead
			- 1-2 plain sentences, facts only
		- Group areas under headers


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
		- Parent is the idea they share
			- Never one peer holding another
		- Aim for 3-5 words a line
			- Longer only when it will not split


## Format

Plain default, when the destination sets no syntax

```
Lead sentence with the bottom line, in plain prose, facts only.


Subject Header
--------------

Base item one
	- Phrase here
	- Another update
		- Its detail
		- Another detail
			- Deeper still

Base item two
	- Detail


Second Subject
--------------

Base item three
	- Detail
```

Same shape in rendered markdown

```markdown
Lead sentence with the bottom line, in plain prose, facts only.


## Subject Header

Base item one
- Phrase here
- Another update
  - Its detail
  - Another detail
    - Deeper still

Base item two
- Detail


## Second Subject

Base item three
- Detail
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
	- Blank line between child groups
		- When each child carries its own details
		- Leaf-only children stay together
	- Never pack sections edge to edge

Capitalize each line
	- Quoted strings and identifiers stay verbatim
	- Names that start lowercase stay lowercase
		- iOS, p95, `--fast`

NOT in caps when the negation is the point of the line
	- "I did NOT update the migration guide"
	- "Cutover NOT scheduled"

Headers group a long response
	- Over 3 base items only
	- The destination's heading syntax
		- Markdown -> # or ##
		- Plain text -> header line, dashes underneath
			- Another plain style is fine
			- Must look different from a base item
	- Names the area, not the findings
	- Adds no indent level

A long response opens with a lead
	- Same trigger as headers
	- 1-2 sentences of plain prose
		- Never more
	- The bottom line, as facts from the details
		- What changed
		- Biggest risk or blocker
		- Anything the reader must act on
	- No verdict the source does not make
		- "Mostly on track" is your judgment, not a fact
		- Source says it -> keep it
	- Friendly through plain wording, not pleasantries
		- "Great week!" is filler
	- Qualifiers match the details below
		- Details say "some" -> lead says "some"
	- No fact that is absent below
	- No link between facts the source does not make
		- Review is Tuesday + threat model NOT sent
		- NOT "threat model needed before Tuesday"
	- Leaving areas out is fine
		- Softening or contradicting them is not
```

## Nesting is a claim

```
An indent asserts the child is
	- Part of the parent
	- Or its cause, or caused by it
	- Or a detail of it
	- Or evidence for it

Read every indent aloud
	- "<child> is part of / a cause of / caused by / a detail of / evidence for <parent>"
	- One must be true
		- "Signing certificate expired" is a cause of "iOS build blocked"
	- None true or unsupported -> re-parent it
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
	- Wrong - "US region" holding both, a bare label
	- Right - "US NOT cut over" holding both
		- Built from the source's own "cutover"
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
		- Only where the indent shows it
		- "Dana's sign-off" on one line keeps the "'s"
	- Causality, so drop "because" and "so"
	- Order, so drop "then" and "after that"

Always drop
	- "Basically"
	- "Just", as emphasis
		- "Just" meaning only or recently is a fact, keep it
	- "Simply"
	- "It turns out that"
	- Vague counts of a complete list
		- "a couple prs: X, Y" -> list X, Y
		- Partial list -> "some" is a qualifier, keep it
			- "Fixed some of the errors" stays "some"
	- Articles, only when nothing is lost
		- "The old queue" keeps "the" - it means the previous one

Never drop
	- Who did it
		- Including I / we / you
		- "I rewrote it" -> "I rewrote it", not "it was rewritten"
		- Negatives say whose, explicitly
			- "I did NOT touch the parquet writer"
				- Only I am known not to have touched it
			- "No one touched the parquet writer"
				- Everyone, verified unchanged
				- Only when the source says so
			- Bare "NOT touched" means NO ONE touched it
				- Never shorthand for "I did not"
	- A qualifier
		- "some"
		- "most"
		- "partially"
	- A hedge
		- "probably"
		- "not verified"
	- Half of a contrast
		- "his call, not mine"
			- Only when the source says "not mine"
	- A fact that only looks redundant
		- "not done" and "still needed" differ
	- Anything unfinished or untouched

A comma-separated list is several ideas
	- Split it into bulleted children
	- Under a parent naming what they share
	- Except a contrast
		- "Suggested by platform, not required" stays one line
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
I bumped the S3 retry count 3 -> 5
	- Platform team's suggestion
	- I doubt it fixes the timeouts
		- Failures we saw were permission errors, not load

I did NOT touch the parquet writer
	- Still the slowest step
```

What survives that usually does not

```
"suggestion"
	- Kept, not upgraded to "call" or "decision"

The doubt and its reason
	- Both, not just the doubt
	- Reason nested under the doubt, as its evidence

"we saw"
	- Limits the claim to observed failures

The untouched item
	- Its own base item
	- NOT a child of the retry change
	- Keeps "I" - the source only says I did not touch it
		- "Parquet writer NOT touched" would claim no one did

The contrast
	- "permission errors, not load" stays one line
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
haven't heard back. Android is fine; nobody has touched that build since
the last release. For docs, I updated the API
reference for the two new endpoints but not the migration guide, which
still describes the old queue.
```

MicroSpeak, plain default

```
Payments migration is done in staging, but the second load test run had
3 timeouts I have not explained. iOS is blocked on an expired signing
certificate.


Payments
--------

Migration to the new queue done in staging
	- I ran the load test twice
		- p95 latency 420ms -> 180ms

Second load test run had 3 timeouts
	- I have NOT explained them yet

Production cutover scheduled Thursday
	- Pending Dana's sign-off


Mobile
------

iOS build blocked
	- Signing certificate expired
	- Marco said he'd renew it today
		- I have NOT heard back

Android fine
	- No one has touched that build since the last release


Docs
----

I updated the API reference
	- Two new endpoints

I did NOT update the migration guide
	- Still describes the old queue
```

One section of it in rendered markdown

```markdown
## Mobile

iOS build blocked
- Signing certificate expired
- Marco said he'd renew it today
  - I have NOT heard back

Android fine
- No one has touched that build since the last release
```

The lead, done wrong

```
Great week! Payments migration is done and we're set for Thursday's cutover.
```

Why it fails

```
"Great week!"
	- Filler, and a verdict the source never made

"Migration is done"
	- Drops "in staging"

"Set for Thursday"
	- Drops "pending Dana's sign-off"
	- Drops the unexplained timeouts
```

What survives that usually does not

```
"I haven't explained yet"
	- The timeouts stay open work, not a footnote

"pending Dana's sign-off"
	- Thursday is conditional

"I haven't heard back"
	- Marco said he would renew it
	- NOT confirmed done

The migration guide
	- Untouched work gets its own base item
	- "I did NOT update" - only the speaker is known

The Android build
	- "No one has touched" - the source says nobody
```

## Worked example, spacing

Packed - child groups run together

```
Three features gone in 2.0
	- Legacy XML export
		- No usage in 6 months of logs
		- Sales confirmed no contracts need it
	- `--fast` CLI flag
		- Did nothing since 1.4
		- Kept as a no-op alias for one release
```

Spaced - full reply, every level of spacing

```
Three features are removed for 2.0, and the config migration script
is NOT tested on Windows.


Removed
-------

Three features gone in 2.0
	- Legacy XML export
		- No usage in 6 months of logs
		- Sales confirmed no contracts need it

	- `--fast` CLI flag
		- Did nothing since 1.4
		- Kept as a no-op alias for one release

	- Python 3.8 support
		- End of life
		- CI matrix no longer runs it

Changelog updated
	- Lists all three removals


Added
-----

Config migration script
	- Converts 1.x YAML to 2.0 TOML
	- Tested on Linux and macOS
	- NOT tested on Windows

New `doctor` command
	- Checks config version
	- Checks Python version
```

Where the blank lines go

```
After the lead
	- Two

After a header
	- One

Between base items
	- One

Between child groups with their own details
	- One

Leaf-only children
	- None, they stay together

Before the next header
	- Two
```

## Before sending

```
Every base item clear alone?
Every indent true?
Every fact from the source present?
Every hedge and qualifier intact?
Any comma-run left to split?
Bullets and headers in the destination's syntax?
Headers distinct from base items?
Blank lines between items, groups and sections?
Long response opens with a lead that matches its details?
No preamble beyond the lead, no sign-off?
```
