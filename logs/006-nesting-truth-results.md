# 006 - nesting truth rules and results

date
    2026-08-24

## Why nesting got its own rules

    05 produced a document where every line was true
        and the document was false

        shipped 4.2
            Android
                ~50% install base
            iOS
                still on 4.1

    source said "I did not touch the iOS build"
    the indent said iOS was part of the 4.2 shipment
    no single line is wrong
    the reader still concludes iOS shipped

    nesting carries all relationship meaning
        wrong nesting invents relationships
        that is fabrication, not formatting

## Rules added to SKILL.md

    "Every indent is a claim"
        each indent asserts one of
            child is PART OF parent
            child is CAUSED BY parent
            child is a DETAIL OF parent
            child is EVIDENCE FOR parent
        unsupported indent = fabrication
            same severity as inventing a fact
            worse than omitting one
                omission leaves a gap
                false nesting states something

    the indent test
        read each indent aloud as a sentence
            "<child> is part of <parent>"
        false        -> re-parent
        unsupported  -> re-parent
        unsure       -> make it a sibling
            a flat pair is honest
            a wrong parent is not

    the topic-adjacency trap
        two things about the same subject
            are not automatically parent and child
        worked example uses the real iOS failure

    self-check reordered
        indent check now runs FIRST
        outranks every other check
            a lie in the nesting survives every other pass

## Rules added to SCORING.md

    nesting truth scored FIRST, gates the rest
        any FALSE indent -> run failed, no other score matters
        any UNSUPPORTED indent -> -1 fact-equivalent
        a FALSE indent counts as a fabricated fact
            not a format problem

## Results - haiku, revised skill

### 05_staged_release - nesting FIXED, fact still lost

    iOS now a separate top-level topic
        parent even self-scopes - "shipped 4.2, Android"
    the structural failure from log 005 is gone

    "not me" STILL DROPPED
        source - "Wei found it, not me"
        haiku  - "finder: Wei"
        this has now survived 3 tweaks
            cycle 3 micro fix
            implied-is-not-stated rule
            attribution-gets-its-own-line rule
        passes in the short micro test every time
        fails in the long input every time

    "cellular: no data" improved
        now paired against "wifi:" on a sibling line
        contrast makes it read as measurements

### 06_warehouse_migration - PASS, 20/20

    unchanged from log 005
    all top-level topics separate
    no false indents

### 07_nesting_traps - 3 of 4 traps passed

    TRAP 2 PASSED - latency spike
        strongest trap, source denies the causation outright
        haiku made it top level
            child - "NOT from index rollout"

    TRAP 3 PASSED - autoscaling rule
        correctly parented as CAUSE of the spike
        not parented to the rollout

    TRAP 4 PASSED - flag rename
        top level
        child - "unrelated to index rollout"

    TRAP 1 FAILED - US region

        search index EU rollout
            Thursday
            US still on old index
                cutover not scheduled yet

        indent reads
            "US still on old index is part of search index EU rollout"
        false - US was not in the rollout

        note on fairness
            the parent is named "EU rollout"
            that naming is what makes the indent false
            parent named "search index migration"
                would make the same indent defensible
            so this is a parent-naming failure
                as much as a placement failure

### date mismatch - I scored this wrong

    haiku wrote
        "Fatima pushed Thursday morning"

    I called this a fabrication. That claim was wrong.

    the test sentence was ambiguous
        "the latency spike people saw Friday
            was not caused by the index rollout,
            it was a bad autoscaling rule
            that Fatima had pushed the same morning"
        "the same morning" has two candidate referents
            the spike's day - Friday
            the rollout named in the same clause - Thursday
    I read it as Friday and scored haiku wrong on that basis
    the ambiguity was in MY input, not necessarily haiku's output
    haiku may have taken a defensible reading

    test text corrected
        now reads "pushed on Friday morning"
        unambiguous, trap preserved
    key updated
        Thursday is now an explicit wrong-value case
        it remains a plausible wrong anchor - the rollout day

    what stands regardless
        the fact keys checked presence, not correctness
        a fact can be PRESENT and WRONG
        no rubric category existed for that

## Open

    "not me" contrast clause under load
        3 tweaks, still failing
        short input passes, long input fails, consistently
    TRAP 1 - parent naming
        no rule yet about naming a parent so its scope is honest
    fact keys check presence, not correctness
        need a wrong-value category
    sonnet and opus not run on 05, 06, 07
