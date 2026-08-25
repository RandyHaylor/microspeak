# 011 - haiku retest, both open failures closed

date
    2026-08-24

scope
    haiku only
    only its two known failures
        06 - the nesting regression
        work task - the invocation that never fired

## 06 - PASS, 20/20, false indent gone

    previous failure, log 007

        reporting workloads - migration to new warehouse
            completed
                most workloads moved

        "most workloads moved is part of completed"
        parent asserted done, child said not all

    now

        reporting workloads migration
          off Redshift → new warehouse (most)

          2 jobs remain on Redshift
            finance month-end job
            churn model feed
            blocker
              UNLOAD syntax (Redshift-specific)
                new engine unsupported
            Marcus: rewrite to generic COPY
              untried

    no "completed" parent at all
    "(most)" survives on the parent line
    all 20 facts present, all 6 high-value ones

    note on form
        "(most)" is a parenthetical
        the skill bans parentheticals for ATTRIBUTION
        a scope qualifier in one is weaker but not lost
        no fact loss, so not scored a failure

    what likely closed it
        the detail-placement rule from log 009
            added AFTER 06 last failed
        06 was never re-run in between
        so this is the first look at 06 under that rule
        plausible, not proven
            no controlled comparison run

## Work task invocation - PASS, skill fired

    previous failure, log 003
        prompt ended with bare "use microspeak"
        haiku made NO Skill tool call
        output was

            Using microspeak to report:

            **Tests would pass**
            - test_line_subtotal_multiplies_price_by_quantity: ...

        it pattern-matched the word
        announced the format
        produced ordinary markdown

    now, prompt ends with "use the microspeak skill"

        Skill invocation captured
            {'skill': 'microspeak', 'args': '...'}

        output is real microspeak
            nested
            no preamble
            no bold headers
            no prose sentences in bullets

    naming the skill is what changed
        "microspeak" alone - a word the model can imitate
        "the microspeak skill" - a thing the model must load

    content accuracy also correct
        all 4 tests correctly called PASS
        found the > vs >= boundary
        found the discount / free-shipping interaction
        hedged appropriately - "may be intentional, unverified"

## README updated

    invocation section now leads with
        "use the microspeak skill"
    states why the bare word is weaker
        with the haiku failure as the worked example

## State of known failures

    all previously open haiku failures are now closed
        06 nesting regression
        work task invocation
        07 trap 1 - closed in log 009
        iOS structural error - closed in log 007
        contrast clause on held-out content - closed in log 007

    remaining caveats, unchanged
        single runs, variance unmeasured
        05 retired, its text is Example 6 in the skill
        sonnet and opus never run on 06 or the micro suite
