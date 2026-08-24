# 002 - skill revisions from run 001

date
    2026-08-24

source
    defects found by the models under test
    logs/001-first-model-test-run.md

---

## Revision 1 - actor-drop exception

found by
    opus, task B

defect
    DROP list said drop "I / we / you as subject"
    Example 3 kept "I did not fix"
        its own note called that correct
    KEEP list covered it only by inference
        "who/what did it when not obvious"
    no stated rule
        models resolve arbitrarily

fix
    explicit EXCEPTION under the DROP entry
    stated rule
        drop the actor only when
            it is you
            AND the fact is finished work
    three worked cases added
        "I did not fix" - responsibility for unfinished work
        "Priya's suggestion" - attribution
        "customer reported" - who observed it

why this matters
    dropping the actor on unfinished work
        makes unfinished work read as done
        same failure class as dropping a hedge

## Revision 2 - invented parent lines now documented

found by
    opus, task B

defect
    Example 2 uses head "submission duplicates"
    phrase does not appear in the source prose
    legitimate practice, no rule permitted it
    a model following the skill strictly
        would think the example violates the skill

fix
    new "parent lines may be invented" block under Shape
    constraint stated
        an invented parent labels children
        it must add no claim
        if it asserts something the source did not
            that is fabrication - remove it

## Revision 3 - ambiguous KEEP line rewritten

found by
    haiku, task B

defect
    line read: NOT -> "errors"
    haiku called it unclear formatting
        "reads like incomplete transformation rule"
    correct call - the arrow is doing two jobs
        transformation elsewhere in the file
        negation here

fix
    rewritten as explicit right/wrong pair
        right: "some errors"
        wrong: "errors"

## Revision 4 - scoring procedure added

found by
    opus, task B

defect
    scoring key listed 8 high-value facts
        said "weight them"
        gave no weight
    format failures listed
        said "note separately"
        gave no scale, no threshold
    cross-model comparison not reproducible

fix
    new file microspeak/tests/SCORING.md
    fact score
        high-value 3 points, ordinary 1
        max 33
        any high-value loss = run failed
            no partial pass on those
    format score
        deduction table from 100
        pass >= 80
    half-credit rule defined
        scope kept in weaker words = full credit
        scope dropped = zero, not half
    run hygiene section
        commit and push before any run
        prevents the stale git reads seen in run 001

---

## Not done, deliberately

    LICENSE file
        flagged by sonnet and opus
        not requested - leaving to repo owner

    CI config
        flagged by sonnet
        no test runner exists to run yet

    harder task A paragraph
        needed - 17/17 across all three models
        current input does not discriminate
        next round

    CLAUDE.md typos
        flagged by haiku - "folowing", "os to"
        CLAUDE.md is the original brief
        kept verbatim as a historical document
