---
name: microspeak
description: |
  Write status, findings, and summaries as nested indented fragments with zero filler, losing zero information. Use when reporting what you did, what you found, what broke, or what changed - and whenever the user says "microspeak", "condense this", "no prose". Prose: "I merged in a couple prs for the api-gateway and admin-portal repos" becomes "merged prs" with "api-gateway" and "admin-portal" indented under it. Strip filler words. Keep every fact, hedge, quantifier, and quoted string.
---

# MicroSpeak

fragments over sentences
indentation over connectives
zero words dropped that carry meaning
zero words kept that do not

## Core rule

```
every word must earn its place
every fact must survive

fail either -> not microspeak
```

lossy condensation is the common failure

```
llms drop nuance when told "be brief"
microspeak is NOT brief
microspeak is DENSE
    line count may rise
    word count falls hard
```

## Shape

```
parent line
    detail
        sub detail
    detail

next parent
```

```
blank line between top-level topics
indent = "belongs to line above"
no connective words needed
    indentation already says "because", "so", "which"
```

parent lines may be invented

```
a parent line names the topic
    it need not appear in the source
    "submission duplicates"
        source said only "double clicks needed to be debounced"
        naming the topic is allowed
constraint
    an invented parent must add no claim
    it labels children, nothing more
    if it asserts something the source did not
        you fabricated - remove it
```

## Word budget

```
3-5 words per line, typical
longer allowed when needed
    quoted strings: verbatim, never trimmed
    identifiers: verbatim
    technical phrases with no shorter true form
```

## Always DROP

```
I / we / you as subject
    implied by context
    EXCEPTION - keep the actor when it carries information
        "I did not fix"
            responsibility for unfinished work
        "Priya's suggestion"
            attribution
        "customer reported"
            who observed it
        rule: drop the actor only when
            it is you
            AND the fact is finished work
"I went ahead and"
"it turns out that"
"basically", "essentially", "just", "simply"
"in order to" -> "to"
"was able to" -> did
"there is/are", "it is"
"currently", "now" when tense already says it
vague counts of things you then list
    "a couple prs" + lists 2 prs -> "prs"
articles a/an/the when unambiguous
restating the question back
```

## Always KEEP

```
scope qualifiers
    "some of the errors"
        right: "some errors"
        wrong: "errors"
    the incompleteness IS the information
hedges
    "probably", "appears", "not verified"
negations, exceptions, conditions
numbers, versions, paths, names, flags
quoted user-facing strings, verbatim
causality when non-obvious
    express by nesting, not by "because"
ordering when order matters
who/what did it when not obvious
```

## Litmus test

```
reader reconstructs original meaning
    from microspeak alone
    no guessing
if not -> you dropped info -> failed
if any line has filler -> failed
```

## Anti-patterns

```
bullets that are still sentences
    "- Fixed the login page which was hanging due to a bad reference"
    wrong: prose with a dash
flat list, no nesting
    loses relationships
summary paragraph above the bullets
    the nesting IS the summary
"Here's what I did:" preamble
closing "Let me know if..." offer
dropping the hedge to sound confident
    worst failure mode
```

---

# Examples

## Example 1 - short

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

note

```
"a couple" dropped
    the list itself carries the count
```

## Example 2 - the canonical case

prose

```
I identified and resolved some of the errors in the code causing our
current issues. The login page was hanging on load due to a bad
reference, double clicks needed to be debounced on submit button,
username field updated to use our css properly. The mouseover text now
properly reads 'Enter your case sensitive username here'
```

microspeak

```
resolved some errors
    not all known errors

login page hanging
    page had bad reference
    reference corrected
        page no longer hangs on load

submission duplicates
    double clicks errantly processed
    debounce solved issue

username field mouseover text wrong
    corrected, uses our css now
    now reads:
        'Enter your case sensitive username here'
```

notes

```
"some" survives as "not all known errors"
    highest-value nuance in the whole passage
quoted string verbatim
each fix its own top-level topic
```

## Example 3 - verbose incident report

prose

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

microspeak

```
intermittent 502s
    checkout endpoint
    customer reported

cause
    upstream payment service slow
        exceeded nginx proxy_read_timeout
            30s
        nginx gave up
            returned 502 to client

stopgap applied
    proxy_read_timeout 30s -> 90s
    502s gone in staging
        NOT confirmed in production

real fix, probably
    async payment call
        webhook callback
    much larger change
    needs payments team buy-in

logging gap found
    upstream response time not logged
    added $upstream_response_time
        nginx access log format

UNFIXED - double charge risk
    checkout_client.py retries on 502
    slow payment could charge twice
    I did not fix
```

notes

```
"seems to have" -> "NOT confirmed in production"
    hedge preserved, made sharper
"probably" preserved on the real fix
"I did not fix that" preserved explicitly
    never let an unfixed item read as fixed
"spent the morning digging into" -> gone
    zero information
```

## Example 4 - decision / tradeoff

prose

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

microspeak

```
cache layer - 3 options discussed

redis, shared instance
    + already running for sessions
    - cache and sessions share failure domain

memcached, separate
    + simpler
    - no recent team experience

in-process LRU
    + free, fast
    - breaks past 1 pod
        multi-pod planned next quarter

leaning: redis, separate instance
    slightly more ops work
    failure domains stay split
```

notes

```
"we talked through" -> gone
"I'm leaning toward" -> "leaning:"
    stays a preference, not a decision
```

## Example 5 - answering a question

question

```
does the importer handle duplicate rows?
```

prose answer

```
Yes, it does handle duplicates, at least partially. The importer uses an
upsert on the external_id column, so rows that come in with an
external_id we've already seen will just update the existing record
rather than creating a new one. However, if a row comes in without an
external_id at all, it falls through to a plain insert, so those can
absolutely duplicate. I checked import_service.py lines 88-140.
```

microspeak answer

```
partially

has external_id
    upsert on external_id
    existing record updated
    no duplicate

no external_id
    plain insert
    duplicates possible

source: import_service.py:88-140
```

notes

```
"yes" alone would be wrong
    "partially" is the honest head
file:line kept verbatim
```

---

# Self-check before sending

```
scan every line
    any word removable without losing meaning?
        remove it
    any fact in the original not present?
        add it back
    any hedge/qualifier softened or dropped?
        restore it
    any line a full sentence?
        split into parent + children
    preamble or sign-off present?
        delete
```
