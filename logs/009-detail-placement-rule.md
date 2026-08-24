# 009 - detail placement rule

date
    2026-08-24

scope
    minimal re-run, by request
        only the failing test - 07
        only the failing models - haiku, sonnet
    opus already passed 07, not re-run
    08 passed on all three, not re-run

## Rule added

    "A detail belongs to what it is ABOUT, not what it was mentioned NEAR"

    reasoning
        prose runs in one line
        a detail often appears beside the wrong topic
        adjacency is an accident of sentence order
            not a relationship

    the question to ask per detail
        what is this a detail OF
        NOT
        what did I write just before it

    two worked examples, both from real failures
        the cutover - sonnet's false indent
        the region - haiku's trap 1

    the orphan check added
        read each top-level topic ALONE
        does it still carry its own open work
        if a topic reads thinner than the source
            a detail of it was filed elsewhere

    the orphan check targets the second harm
        a misfiled detail damages TWO topics
            the parent gains a false claim
            the real owner silently loses a fact

## Results

### haiku 07 - PASS, all four traps

    trap 1 closed

        search index rolled out - EU region
            Thursday

        US region
            still on old index
            cutover NOT scheduled

    US is top-level
    the cutover moved with it
    parent no longer over-claims

### sonnet 07 - PASS, false indent gone

        search index rolled out - EU only
            Thursday
            relevance +~12 percent
                internal eval set only
                not measured on real traffic

        US region
            still on old index
            cutover NOT scheduled

    cutover correctly filed under US
    relevance stayed under the EU parent
        correct - relevance improved IN EU
        it is genuinely a detail of the EU rollout
        the rule did not over-correct

## State of the known failures

    closed
        haiku trap 1 - parent over-claiming
        sonnet cutover - detail filed near, not about
        haiku iOS structural error - closed in log 007
        contrast clause on held-out content - closed in log 007

    open
        haiku 06 - false indent, merged root
            "most workloads moved" under "completed"
            declared a haiku limitation, not chased
        control run - still never done
            the baseline claim from log 001 remains unverified

    untested
        micro suite on sonnet and opus
        06 on sonnet and opus
