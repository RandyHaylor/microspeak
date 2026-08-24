# Scoring procedure

How to score a MicroSpeak test run reproducibly.

## Task A - condensation

```
three independent scores
    never collapse them into one number
    a model can be perfectly formatted and lossy
    a model can keep every fact and still lie
        through nesting alone
```

### Nesting truth - scored FIRST, gates the rest

```
every indent asserts
    child is PART OF / CAUSED BY / DETAIL OF / EVIDENCE FOR parent

procedure
    read each indent as "<child> is part of <parent>"
    mark it
        TRUE        - source supports it
        UNSUPPORTED - source never said it
        FALSE       - source denied it

scoring
    any FALSE indent     -> run failed, no other score matters
    any UNSUPPORTED      -> -1 fact-equivalent each
    treat a FALSE indent as a fabricated fact
        not a format problem
        it asserts something the source denied
        while every line reads as true

why this gates
    a fact loss leaves a gap a reader can notice
    a false parent reads as confident and correct
    it survives proofreading
        because no single line is wrong
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

presence is not correctness
    check every fact for BOTH
        is it there
        is its value right
    a present fact with a wrong value scores WORSE than a missing one
        missing  - reader sees a gap
        wrong    - reader acts on a false number

    wrong-value categories to check explicitly
        dates and days
            a nearby date is a plausible wrong anchor
        numbers, versions, counts
        directions of change
            "3 -> 5" reported as "5 -> 3"
        who did what
            attribution swapped between people
        quoted strings altered
            any edit at all is a wrong value

    scoring
        wrong value on a high-value fact  -> run failed
        wrong value on an ordinary fact   -> -2, not -1

credit
    full    fact present, value right, meaning intact
    half    fact present, value right, meaning weakened
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
    -5   per line holding two ideas that should be nested
        long is not the offense
        two-ideas-in-one-line is the offense
        fix is splitting, never trimming

ABSOLUTE RULE
    never deduct against a line that preserves a fact
    line length is NOT scored
        a 9-word line holding one idea costs nothing
    if a shorter output and a longer output
        both keep all facts
        and both nest one idea per line
        they score the SAME

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
