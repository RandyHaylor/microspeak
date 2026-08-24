# 007 - held-out test, and a nesting regression

date
    2026-08-24

## Changes made this round

    test text fixed
        07 said "pushed the same morning"
            ambiguous - Friday or Thursday
        now "pushed on Friday morning"
        haiku reported Friday correctly after the fix
            confirms the earlier mismatch was my input

    log 006 corrected
        I had called the Thursday reading a fabrication
        that claim was wrong - my sentence was ambiguous

    SKILL.md - parent naming rule
        a parent's name sets the scope of every indent under it
        two fixes offered
            widen the parent
            or split into siblings
        "pick the parent name AFTER you know its children"
        "a name honest with 2 children can go false with a 3rd"

    SKILL.md - Example 6
        a contrast clause buried in a long report
        added because the rule kept failing under load
            the isolated example was not enough
            the example now matches the failing CONDITION

    SCORING.md - wrong-value category
        presence is not correctness
        a present fact with a wrong value scores WORSE than a missing one
            missing - reader sees a gap
            wrong   - reader acts on a false number
        explicit categories
            dates and days, numbers, direction of change,
            attribution swaps, altered quoted strings

## Example 6 contaminated test 05

    Example 6 is the 05 paragraph verbatim
    haiku now reproduces it almost exactly
    05 no longer measures anything
        the answer is in the skill

    05 is RETIRED as a test
        kept as an example only

    this is a cost of the add-an-example rule
        every example burns a test case
        each one added must come with a fresh held-out case

## 08 - the held-out replacement - PASS 15/15

    same failure patterns as 05
        contrast clause in a long report
        parent that could over-claim
        scoped measurement
        scope qualifier
    different domain, different wording
    never appears in SKILL.md

    parent trap HELD

        Ontario tenants - finished 14th
            ~80% of records

        Quebec tenants - skipped
            different retention policy
            no decision how to handle

        Quebec is top-level
        NOT nested under Ontario
        this is the 05 iOS failure, on unseen content, passing

    contrast clause SURVIVED

        export script
            Priyanka wrote
            speaker ran only

        not the explicit "NOT the speaker" form from Example 6
        the disclaimer is intact and unambiguous
        the pairing carries it

    verbatim strings exact
        'client_id' and 'clientId'
        differ only by underscore and case

    all 15 facts present, all values right

## 07 - trap 1 improved, not clean

    haiku widened the parent

        new search index rollout
            EU region
                Thursday
            US region
                still on old index

    this is the fix the skill endorses
        widen the parent, make EU and US siblings

    still not honest
        "rollout" is an action word
        US did not undergo a rollout
        "migration" or "status" would be true
    borderline, improved, not fixed

    traps 2, 3, 4 all pass
    date now correct

## 06 - REGRESSION on nesting

    was 20/20 twice
    now has a FALSE indent

        reporting workloads - migration to new warehouse
            completed
                most workloads moved

    read aloud
        "most workloads moved is part of completed"
    parent asserts done
    child says not all
    contradiction inside two indents

    also
        everything collapsed back under one root
        the six separate top-level topics from earlier runs are gone

    06 got WORSE after the nesting rules were added
        the rules were written to prevent exactly this

    I do not know why
        candidate - SKILL.md grew a lot this round
            parent naming section
            Example 6, long
            every-indent-is-a-claim section
        more rules may be crowding out earlier ones
    NOT investigated
        no evidence either way yet

## Where this leaves the bar

    passing on held-out content
        08 - contrast clause, parent naming, scope qualifiers, verbatim strings

    still failing
        06 - false indent, merged root, on a case that used to pass
        07 trap 1 - parent named with an action word

    untested since all these revisions
        sonnet
        opus
        the micro suite

## Next candidate, not yet done

    check whether SKILL.md length is hurting
        the file has roughly doubled this round
        06 regressed in the same round
        a shorter, ordered rule set may hold better
    that is a hypothesis, unverified
