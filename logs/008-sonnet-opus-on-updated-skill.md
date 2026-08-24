# 008 - sonnet and opus on the updated skill

date
    2026-08-24

scope
    two tests only, deliberately small
        07_nesting_traps
        08_heldout_contrast_and_parent
    05 excluded - retired, its text is Example 6 in the skill
    06 excluded - haiku regression, not chased further

## Decision recorded - haiku limitation

    call made by the project owner
        haiku's remaining failures are a haiku limitation
        reasoning given
            microspeak deviates significantly
                from haiku's trained output formatting

    haiku's state when this was called
        PASSING
            08 held-out - 15/15
            07 traps 2, 3, 4
            all four micro tests
        FAILING
            06 - false indent, "most workloads moved" under "completed"
                a case that passed 20/20 twice before
            07 trap 1 - parent named with an action word
            "not me" in 05-style long input
                though 08 carried the same disclaimer successfully

    not investigated further, by decision

## opus - PASS on both

    07
        all four traps passed
        cutover correctly parented

            US region
                still on old index
                cutover NOT scheduled
                    speaker has not scheduled it

        kept the actor on the cutover
        every fact present, every value right

    08
        15/15
        parent self-scopes

            compliance export finished - Ontario tenants only

        Quebec top-level, skipped entirely
        contrast explicit - "NOT by the speaker"
        both quoted strings exact
        also kept "only issue hit"

## sonnet - 08 PASS, 07 has one FALSE indent

    08
        15/15
        contrast in the explicit form

            export script written by Priyanka
                NOT by speaker
                speaker only ran it

        Quebec top-level, "skipped entirely" kept whole

    07
        all 18 facts present
        all four traps passed
        ONE false indent

            search index rolled out - EU only
                Thursday
                cutover NOT scheduled

            US region
                still on old index

        the cutover is the US cutover
            source - "the US region is still on the old index
                and I have not scheduled the cutover yet"
        nested under an EU-scoped parent it reads as
            "the EU cutover is not scheduled"
        false

        second harm
            the US topic is left without its key fact
            a reader scanning "US region" sees only
                "still on old index"
            the open work is filed under the wrong region

## What this establishes

    nesting truth is NOT a haiku-only problem

        sonnet produced a false indent
            every fact present
            every line individually true
            the document still says something false

        opus caught the same case and placed it correctly

    so the failure spans tiers
        opus  - clean
        sonnet - one occurrence
        haiku  - repeated occurrences

    the skill's nesting rules help but do not close it
        07 trap 1 caught haiku
        07 cutover caught sonnet
        both are placement-of-a-detail errors
            not topic-level merges
        the rules address topic-level nesting well
        detail-level placement is weaker

    a detail belongs to the topic it is ABOUT
        not the topic it was mentioned NEAR
        no rule states this yet

## Untested

    micro suite on sonnet and opus
    06 on sonnet and opus
        would show whether the merged-root regression spans models
    control run still not done
