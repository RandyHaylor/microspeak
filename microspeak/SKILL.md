---
name: microspeak
description: |
  Dense lossless output format
      - Nested fragments, zero filler, zero facts lost
      - Use for status, findings, what broke, what changed
      - Triggers: "microspeak", "condense this", "no prose"

  Prose converted to microspeak
      - "I merged in a couple prs for the api-gateway and admin-portal repos"
      - Becomes:
          * Merged prs
              - api-gateway
              - admin-portal

  Rules for shaping a response
      - Base items at column 0, blank line between
          * Each a phrase clear on its own
          * Children may be terse, parents supply the subject
      - Bullets alternate - then * by depth
      - Capitalize each line
      - Quoted strings and identifiers verbatim
      - Over 3 base items
          * Wrap each area in === Header ===
          * Close with === Response summary ===, areas only

  Never lose a detail
      - Keep qualifiers, hedges, negations, attribution
      - Keep numbers, quoted strings, unfinished work
      - Long line = two ideas, split to parent + child
---

# MicroSpeak

Fragments over sentences
Indentation over connectives
Zero words dropped that carry meaning
Zero words kept that do not

## Format

```
=== Subject Header ===

Base item 1
    - Phrase one here
    - Update two is here
        * Update two's detail 1
        * Update two's detail 2
            - Further nesting like this
            - Etc.

Base item 2
    - Detail

=== Response summary ===

- Base item 1
- Base item 2
```

Bullets alternate by depth

```
Base items
    - No bullet, column 0
Depth 1
    - Dash
Depth 2
    - Asterisk
Depth 3
    - Dash again
Depth 4
    - Asterisk again
```

Capitalization

```
Capitalize the first letter of every line
Quoted strings and identifiers stay exactly as written
    - 'client_id' is not 'Client_id'
    - api-gateway is not Api-gateway
```

## Core rule

```
Every word must earn its place
Every fact must survive

Fail either -> not microspeak
```

Lossy condensation is the common failure

```
LLMs drop nuance when told "be brief"
Microspeak is NOT brief
Microspeak is DENSE
    - Line count may rise
    - That is fine

Shorter is NOT the goal
    - Clear and complete is the goal
    - A longer correct answer beats a shorter lossy one, always
    - Never delete a fact to shorten
        * Deleting facts IS the problem microspeak solves
        * A compressed answer that lost a fact has failed
            - No matter how clean it looks
```

## Shape

```
Blank line between base items
Indent = "belongs to line above"
No connective words needed
    - Indentation already says "because", "so", "which"
```

## What each line has to say on its own

```
A line is read with its ancestors
    - Parents, grandparents, up to the base item
    - NOT siblings
    - NOT neighbouring branches

Base items have no ancestors
    - So a base item must be clear alone
    - A phrase, roughly 3-5 words, lenient
    - "Output" alone says nothing
    - "Dense lossless output format" does

Children lean on their parents
    - Terse is correct when the parent supplies the subject
    - Under "Retry count raised 3 -> 5"
        * "Platform team's call" is complete
        * Repeating the subject would be filler
```

A run of category labels at base level is a smell

```
Smell - three labels in a row
    - Format
        * Base items at column 0
    - Keep
        * Qualifiers, hedges
    - Never
        * Drop a fact

Those are a list wearing the costume of topics
    - Rules for shaping a response
        * Base items at column 0
        * Keep qualifiers and hedges
        * Never drop a fact
```

## Subject headers

```
When to use
    - More than 3 base items -> use headers
    - 3 or fewer -> no headers, plain microspeak
```

Syntax

```
=== S3 Retry Change ===

S3 retry count 3 -> 5
    - Platform team's suggestion
    - May not fix timeouts

Rollback script
    - Never tested against staged rollout
```

Rules

```
Blank line after every header
Blank line before every header

Header text
    - A sentence fragment, never a full sentence
    - Longer than a normal microspeak line is fine
    - Names the AREA, not the findings

Content under a header
    - Starts at column 0
    - A header adds NO indent level
    - Normal microspeak, unchanged
```

## Response summary

```
The last thing in the response
    - After every subject block
    - Always present when headers are used
```

```
=== Response summary ===

- S3 retry change
- Rollback script coverage
- Open decisions
```

What it is

```
A table of contents
    - What the response COVERS
    - NOT what the response SAYS

One short line per area
    - No numbers
    - No findings
    - No conclusions
    - The reader scans it to pick where to look

Wrong - restates the content
    - Retry count 3 -> 5, may not fix timeouts
Right - names the area
    - S3 retry change
```

Why it stays empty of detail

```
The detail is already above it
    - Repeating it doubles the reading
    - And invites a lossy second version
```

## Every indent is a claim

```
Nesting is not layout
    - It is the only thing carrying relationship
    - Get it wrong and the document lies
        * While every single line reads as true

Each indent asserts one of
    - Child is PART OF parent
    - Child is CAUSED BY parent
    - Child is a DETAIL OF parent
    - Child is EVIDENCE FOR parent

That assertion must be true
    - And supported by the source
    - An unsupported indent is fabrication
        * Same severity as inventing a fact
        * Worse than omitting one
            - Omission leaves a gap
            - False nesting states something
```

The indent test - run it on every line

```
Read the indent aloud as a sentence
    - "<child> is part of <parent>"
If that sentence is false     -> re-parent it
If the source never said it   -> re-parent it
If you are unsure             -> make it a sibling
    - A flat pair is honest
    - A wrong parent is not
```

The topic-adjacency trap

```
Two things about the same subject
    - Are not automatically parent and child

Source
    - "we shipped 4.2 to android
        I did not touch the iOS build
        it is still on 4.1"

Wrong
    - Shipped 4.2
        * Android
            - ~50% install base
        * iOS
            - Still on 4.1
    - The indent says iOS is part of the 4.2 shipment
    - The source said the opposite
    - Every line above is individually true
        * The document is still false

Right
    - Shipped 4.2 - Android only
        * ~50% install base
    - iOS NOT touched
        * Still on 4.1
        * No timeline

Both are about the release
    - Only one shipped
    - So they are siblings, not parent and child
```

## Name the parent to match what it holds

```
A parent's name sets the scope of every indent under it
    - Name it narrow -> children must all be inside that scope
    - Name it wide   -> children may vary

Source
    - "rolled out the new search index to the EU region
        the US region is still on the old index"

Wrong
    - Search index EU rollout
        * US still on old index
    - The indent now reads
        * "US is part of the EU rollout"
    - False

Two ways to fix
    - Widen the parent
        * Search index migration
            - EU - rolled out Thursday
            - US - still on old index
    - Or split into siblings
        * Search index rolled out - EU
            - Thursday
        * US region
            - Still on old index

Pick the parent name AFTER you know its children
    - Then re-read every indent under it
    - A name that was honest with 2 children
        * Can go false when you add a 3rd
```

## A detail belongs to what it is ABOUT

```
Not to what it was mentioned NEAR

Prose runs in one line
    - A detail often appears beside the wrong topic
    - That adjacency is an accident of sentence order
    - It is not a relationship

For each detail ask
    - What is this a detail OF
    - Not what did I write just before it
```

Worked - the cutover

```
Source
    - "we rolled out the new search index to the EU region
        the US region is still on the old index
        and I have not scheduled the cutover yet"

Wrong
    - Search index rolled out - EU only
        * Thursday
        * Cutover NOT scheduled
    - US region
        * Still on old index
    - The cutover is the US cutover
    - Filed under an EU parent it reads as
        * "the EU cutover is not scheduled"
    - And the US topic is left without its key fact
        * A reader scanning "US region"
            - Sees only "still on old index"
            - And misses the open work

Right
    - Search index rolled out - EU only
        * Thursday
    - US region
        * Still on old index
        * Cutover NOT scheduled
```

Worked - the region

```
Wrong
    - Search index EU rollout
        * US region
            - Still on old index
    - US was not part of the EU rollout

Right
    - US region
        * Still on old index
```

The orphan check

```
After placing every detail
    - Read each base item ALONE
    - Does it still carry its own open work
        * Its own numbers
        * Its own unfinished items
    - If a topic reads thinner than the source
        * A detail of it was filed elsewhere
```

Parent lines may be invented

```
A parent line names the topic
    - It need not appear in the source
    - "Submission duplicates"
        * Source said only "double clicks needed to be debounced"
        * Naming the topic is allowed

Constraint
    - An invented parent must add no claim
    - It labels children, nothing more
    - If it asserts something the source did not
        * You fabricated - remove it
```

## Line length

```
One idea per line
    - A line holding two ideas reads badly
    - Fix by SPLITTING, never by cutting facts
        * Long line -> parent + child
        * Every FACT survives the split
        * Filler does not - see below

Lines often land at 3-5 words
    - That is a RESULT of one-idea-per-line
    - It is NOT a budget to hit
    - A 9-word line holding one idea is correct
        * Do not cut it to reach 5

Never shorten a line by dropping
    - A qualifier - "most", "some", "partially"
    - A hedge - "probably", "not verified"
    - A fact that merely looks redundant
    - Quoted strings - verbatim, never trimmed
    - Identifiers - verbatim
```

## The structure already says it - delete the words for it

```
Nesting carries ownership, connection and order
    - A word that only states one of those
        * Is filler
        * Delete it
    - The indent already said it
```

Ownership - the indent means "of" and "'s"

```
Prose
    - "the read timeout for the payment service"
Wrong
    - Timeout for the payment service
Right
    - Payment service
        * Read timeout 30s
```

Connection - the indent means because, so, which, due to

```
Prose
    - "the page hung because the reference was bad"
Wrong
    - Page hung because of a bad reference
Right
    - Page hung
        * Bad reference
```

Order - line order means first, then, after that

```
Prose
    - "we reverted the rule and then latency recovered"
Wrong
    - Reverted the rule, then latency recovered
Right
    - Rule reverted
        * Latency recovered
```

The test

```
Does this word only express
    - Whose it is
    - What caused what
    - What happened first
If yes, and the nesting shows it
    - The word is filler
    - Delete it

If the nesting does NOT show it
    - Keep the word
    - Or fix the nesting
```

## Always DROP

```
I / we / you as subject
    - Implied by context
    - EXCEPTION - keep the actor when it carries information
        * "I did not fix"
            - Responsibility for unfinished work
        * "Priya's suggestion"
            - Attribution
        * "customer reported"
            - Who observed it
        * Rule: drop the actor only when
            - It is you
            - AND the fact is finished work
"I went ahead and"
"It turns out that"
"Basically", "essentially", "just", "simply"
"In order to" -> "to"
"Was able to" -> did
"There is/are", "it is"
"Currently", "now" when tense already says it
Vague counts of things you then list
    - "a couple prs" + lists 2 prs -> "prs"
Articles a/an/the when unambiguous
Restating the question back
```

## Always KEEP

```
Scope qualifiers
    - "some of the errors"
        * Right: "some errors"
        * Wrong: "errors"
    - The incompleteness IS the information
Hedges
    - "probably", "appears", "not verified"
Negations, exceptions, conditions
    - A "not X" clause is a fact, not decoration
    - "Ravi's call, not mine" is TWO facts
        * Who decided
        * Who did not
Attribution
    - Gets its own line, never a parenthetical
    - Wrong - "pool 10 -> 25 (Ravi)"
    - Right
        * Pool 10 -> 25
            - Ravi's call
            - Explicitly not the speaker's
    - A parenthetical demotes a fact to an aside
Numbers, versions, paths, names, flags
Quoted user-facing strings, verbatim
Causality when non-obvious
    - Express by nesting, not by "because"
Ordering when order matters
Who/what did it when not obvious
```

## Litmus test

```
Reader reconstructs original meaning
    - From microspeak alone
    - No guessing
If not -> you dropped info -> failed
If any line has filler -> failed
```

## Anti-patterns

```
Bullets that are still sentences
    - "- Fixed the login page which was hanging due to a bad reference"
    - Wrong: prose with a dash
Flat list, no nesting
    - Loses relationships
Summary paragraph above the bullets
    - The nesting IS the summary
"Here's what I did:" preamble
Closing "Let me know if..." offer
Dropping the hedge to sound confident
    - Worst failure mode

Dropping a fact because it "looks redundant"
    - Source: "I have not backfilled the files
        that still needs to happen"
    - Two different facts
        * NOT done      - current state
        * Still needed  - still required
    - Work can be undone AND cancelled
        * Keeping only one loses which case this is
    - Right
        * Backfill NOT done
            - Still needs to happen
    - Wrong
        * Backfill NOT done

Dropping a clause because something else implies it
    - "Implied" is not "stated"
    - If the source stated it, state it
    - A deadline does NOT replace "still needed"
        * Right
            - Migration NOT run on production
            - Still needs to happen
            - Before Friday
        * Wrong
            - Migration NOT run on production
            - Deadline: before Friday
    - Half of a contrast is not the contrast
        * Source: "which was Ravi's call, not mine"
        * Right
            - Ravi's call
            - Explicitly not the speaker's
        * Wrong
            - Ravi's call
        * "not mine" is the speaker distancing
            - Dropping it reassigns responsibility

Merging two topics under one parent to save a line
    - Six unrelated topics nested under one root
        * Reads as though all six are subtopics
    - Each topic gets its own base item
```

---

# Examples

## Example 1 - short

Prose

```
I merged in a couple prs for the api-gateway and admin-portal repos
```

MicroSpeak

```
Merged prs
    - api-gateway
    - admin-portal
```

Note

```
"a couple" dropped
    - The list itself carries the count
Repo names stay lowercase
    - They are identifiers
```

## Example 2 - the canonical case

Prose

```
I identified and resolved some of the errors in the code causing our
current issues. The login page was hanging on load due to a bad
reference, double clicks needed to be debounced on submit button,
username field updated to use our css properly. The mouseover text now
properly reads 'Enter your case sensitive username here'
```

MicroSpeak

```
Resolved some errors
    - Not all known errors

Login page hanging
    - Page had bad reference
    - Reference corrected
        * Page no longer hangs on load

Submission duplicates
    - Double clicks errantly processed
    - Debounce solved issue

Username field mouseover text wrong
    - Corrected, uses our css now
    - Now reads:
        * 'Enter your case sensitive username here'
```

Notes

```
"some" survives as "not all known errors"
    - Highest-value nuance in the whole passage
Quoted string verbatim
Each fix its own base item
```

## Example 3 - verbose incident report

Prose

```
So I spent the morning digging into the intermittent 502s that our
customers have been reporting on the checkout endpoint. It turns out
that the upstream payment service was occasionally taking longer than
our nginx proxy_read_timeout of 30 seconds, which caused nginx to give
up and return a 502 to the client. I bumped the timeout to 90 seconds
as a stopgap, and that seems to have made the 502s go away in staging,
though I haven't confirmed it in production yet. The real fix is
probably going to be making the payment call asynchronous with a
webhook callback, but that's a much larger change and would need buy-in
from the payments team. I also noticed while I was in there that we're
not logging the upstream response time at all, so I added
$upstream_response_time to the nginx access log format. One more thing
- the retry logic in checkout_client.py retries on 502, which means a
slow payment could be charged twice. I did not fix that.
```

MicroSpeak

```
=== Checkout 502s ===

Intermittent 502s
    - Checkout endpoint
    - Customer reported

Cause
    - Upstream payment service slow
        * Exceeded nginx proxy_read_timeout 30s
        * Nginx gave up
            - Returned 502 to client

Stopgap applied
    - proxy_read_timeout 30s -> 90s
    - 502s gone in staging
        * NOT confirmed in production

Real fix, probably
    - Async payment call
        * Webhook callback
    - Much larger change
    - Needs payments team buy-in

=== Other findings ===

Logging gap found
    - Upstream response time not logged
    - Added $upstream_response_time
        * nginx access log format

UNFIXED - double charge risk
    - checkout_client.py retries on 502
    - Slow payment could charge twice
    - I did not fix

=== Response summary ===

- Checkout 502 cause and stopgap
- Proposed real fix
- Logging gap
- Unfixed double charge risk
```

Notes

```
"seems to have" -> "NOT confirmed in production"
    - Hedge preserved, made sharper
"probably" preserved on the real fix
"I did not fix that" preserved explicitly
    - Never let an unfixed item read as fixed
"spent the morning digging into" -> gone
    - Zero information
More than 3 base items
    - So headers and a summary are used
```

## Example 4 - decision / tradeoff

Prose

```
We talked through three options for the cache layer. Redis is the
obvious choice since we already run it for sessions, but it would mean
the cache and the session store share a failure domain. Memcached is
simpler and we could run it separately, but nobody on the team has
operated it recently. An in-process LRU is free and fast but breaks as
soon as we scale past one pod, which we're planning to do next quarter.
I'm leaning toward Redis on a separate instance - it's slightly more
ops work but keeps the failure domains split.
```

MicroSpeak

```
Cache layer - 3 options discussed

Redis, shared instance
    - Already running for sessions
    - Cache and sessions share failure domain

Memcached, separate
    - Simpler
    - No recent team experience

In-process LRU
    - Free, fast
    - Breaks past 1 pod
        * Multi-pod planned next quarter

Leaning: Redis, separate instance
    - Slightly more ops work
    - Failure domains stay split
```

Notes

```
"we talked through" -> gone
"I'm leaning toward" -> "Leaning:"
    - Stays a preference, not a decision
```

## Example 5 - answering a question

Question

```
does the importer handle duplicate rows?
```

Prose answer

```
Yes, it does handle duplicates, at least partially. The importer uses an
upsert on the external_id column, so rows that come in with an
external_id we've already seen will just update the existing record
rather than creating a new one. However, if a row comes in without an
external_id at all, it falls through to a plain insert, so those can
absolutely duplicate. I checked import_service.py lines 88-140.
```

MicroSpeak answer

```
Partially

Has external_id
    - Upsert on external_id
    - Existing record updated
    - No duplicate

No external_id
    - Plain insert
    - Duplicates possible

Source: import_service.py:88-140
```

Notes

```
"yes" alone would be wrong
    - "partially" is the honest head
file:line kept verbatim
```

## Example 6 - a contrast clause buried in a long report

The hardest case in practice
    - The rule is easy in isolation
    - It gets dropped when 15 other facts compete for attention
    - So here it is under load

Prose

```
We shipped 4.2 to about half the Android install base on Tuesday, staged
rollout, and I have not promoted it to the remaining users. Crash-free
sessions are at 99.4 percent, slightly better than 4.1, though the sample
is only two days old so I would not read much into it. The biggest fix was
the camera permission prompt appearing twice on first launch, which was a
duplicate call in the onboarding flow, and Wei found it, not me. The prompt
now reads 'Allow PhotoSync to use your camera?' and appears once. We raised
the upload chunk size from 1 MB to 4 MB, which cut median upload time
roughly in half on wifi, but we have no cellular numbers at all. I did not
touch the iOS build; it is still on 4.1 and there is no timeline.
```

MicroSpeak

```
=== 4.2 Android Release ===

Shipped 4.2 - Android only
    - ~half the install base
    - Staged rollout
    - Tuesday
    - NOT promoted to remaining users

Crash-free sessions 99.4 percent
    - Slightly better than 4.1
    - Sample only 2 days old
        * Would not read much into it

=== Fixes And Changes ===

Camera permission prompt appeared twice
    - On first launch
    - Biggest fix in the build
    - Cause - duplicate call in onboarding flow
    - Found by Wei
        * NOT by the speaker
    - Now appears once
        * 'Allow PhotoSync to use your camera?'

Upload chunk size 1 MB -> 4 MB
    - Median upload time cut roughly in half
        * On wifi
    - No cellular numbers at all

=== Untouched ===

iOS NOT touched
    - Still on 4.1
    - No timeline

=== Response summary ===

- 4.2 Android rollout status
- Crash-free rate
- Camera prompt fix
- Upload chunk size change
- iOS status
```

What survives here that usually does not

```
"not me"
    - Kept as its own line - "NOT by the speaker"
    - NOT collapsed to "found by Wei"
    - NOT demoted to "(Wei)"
    - The speaker is disclaiming credit
        * Drop it and you assign them the find

"about half"
    - Kept - "~half the install base"
    - Not rounded away to "shipped to Android"

"no cellular numbers at all"
    - Kept as a sibling of the wifi result
    - The wifi number alone implies coverage that does not exist

iOS
    - Its own header, NOT under the release block
    - Parent renamed "Shipped 4.2 - Android only"
        * So no indent under it can over-claim
```

---

# Self-check before sending

```
Every base item clear on its own?
    - Read it with nothing else on screen
    - A bare label means it belongs in a list, not at base level

More than 3 base items?
    - Wrap each area in === Subject Header ===
    - Blank line before and after every header
    - End with === Response summary ===
        * Areas only, never findings

Read every indent as a sentence FIRST
    - "<child> is part of <parent>"
    - False or unsupported?
        * Re-parent, or make it a sibling
    - This check outranks every other check
        * A lie in the nesting survives every other pass

Scan every line
    - Any word removable without losing meaning?
        * Remove it
    - Any fact in the original not present?
        * Add it back
    - Any hedge/qualifier softened or dropped?
        * Restore it
    - Any line a full sentence?
        * Split into parent + children
    - Preamble or sign-off present?
        * Delete
    - First letter capitalized?
        * Except quoted strings and identifiers
    - Bullets alternate dash, asterisk, dash?
        * By depth
```
