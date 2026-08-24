# Scoring procedure

How to score a MicroSpeak test run reproducibly.

## Task A - condensation

```
two independent scores
    never collapse them into one number
    a model can be perfectly formatted and lossy
    lossy is the failure that matters
```

### Fact score

```
weights
    high-value fact   3 points
    ordinary fact     1 point

test_paragraph_condense_input.md
    8 high-value  -> 24
    9 ordinary    ->  9
    max           -> 33

credit
    full    fact present, meaning intact
    half    fact present, meaning weakened
        "mostly" for "most of the backlog"
            still scopes - full credit
        "cleared backlog" with no qualifier
            scope lost - zero, not half
    zero    fact absent or reversed

pass threshold
    33/33 on high-value facts is required
        any high-value loss = run failed
        no partial pass on these
    ordinary facts
        >= 8/9 to pass
```

### Format score

```
deductions, from 100

    -25  a fact was invented
    -20  preamble or sign-off present
    -15  flat list, no nesting where nesting was warranted
    -15  output wrapped in a code fence when asked for microspeak only
    -10  per line that is a full sentence
    -10  summary paragraph above the structure
    -5   per line carrying filler
    -5   per line over 5 words with no reason
        quoted strings exempt
        identifiers exempt
        technical phrases with no shorter true form exempt

pass threshold
    >= 80
```

## Task B - real work, report only in microspeak

```
scored on three axes

    task completion
        did it answer every numbered item
        pass = all items answered

    accuracy
        every claim verifiable against the repo
        stale reads noted separately
            quiesce the repo before the run
            a stale read is a setup fault, not a model fault

    format
        same deduction table as task A
```

## Run hygiene

```
before any run
    commit and push everything
        working tree clean
    otherwise models report git state that changes under them

each model
    fresh agent, no shared context
    told to read SKILL.md
    blocked from reading scoring key

record
    raw output verbatim
        tests/results/
    scores and reasoning
        logs/
```
