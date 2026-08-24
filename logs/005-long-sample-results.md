# 005 - long sample results, haiku, revised skill

date
    2026-08-24

two new long multi-topic inputs
    built to reproduce what the micro tests are too short to trigger
    haiku only, revised skill, real skill discovery

## 06_warehouse_migration - PASS, 20/20

    every fact survived
        including all 6 high-value facts
            "most" scope qualifier
            Marcus attribution
            Marcus has NOT tried it
            "treat that number as soft"
            other jobs NOT audited
            still paying Redshift in parallel

    structure correct
        six separate top-level topics
        no merged root
        no preamble
        no trailing commentary

## 05_staged_release - FAIL

### high-value loss

    source
        "Wei found it, not me"
    haiku
        "Wei found it"
    "not me" dropped

    this is the exact construction of micro test 04
        micro 04 - "Ravi's call, not mine"
        micro 04 PASSES in isolation
        same pattern FAILS inside a long input

### structural error

    haiku nested iOS under "shipped 4.2"

        shipped 4.2
            Android
                ~50% install base
            iOS
                still on 4.1
                no timeline

    reads as though iOS was part of the 4.2 shipment
    source said the opposite
        "I did not touch the iOS build"
    the explicit not-touched statement is also gone
        only "still on 4.1" survives
    a reader concludes iOS shipped something
        it shipped nothing

### weakened

    source
        "we have no cellular numbers at all"
    haiku
        "no cellular data"
    "numbers" means measurements
    "data" reads as either
        no measurements
        no cellular traffic
    nesting under upload chunk size implies measurements
    weakened, not erased

### what 05 got right

    "~50% install base" - scope qualifier kept
    "not promoted to remaining users" - kept
    hedge kept - "2-day sample (early to judge)"
    quoted prompt kept verbatim
    "on wifi" scope kept
    FLAG - rollback script never tested against staged rollout
        only tested against full
    no preamble
    no trailing commentary
    no single merged root

## What this pair establishes

    a controlled comparison, finally

        same failure mode - contrast clause "X, not me"
        short input  - PASSES  (micro 04, cycle 3)
        long input   - FAILS   (05)

    the skill rule exists and is followed on short input
    the same rule is not applied on long input
    passing the micro suite does NOT predict long-input behavior

    06 passing shows long input is not automatically fatal
        06 contains no "X, not me" contrast
        its attribution (Marcus) has no contrast half
        so 06 never exercised the failing rule

    length alone is not the variable
        06 is long and passes
        the variable is
            a rule that must fire mid-document
            competing with many other facts

## Not yet done

    no tweak attempted for the 05 failures
    sonnet and opus not run on 05 or 06
    still no control run
