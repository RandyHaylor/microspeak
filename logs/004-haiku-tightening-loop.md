# 004 - haiku tightening loop

date
    2026-08-24

## Framing correction

    earlier logs ranked the models against each other
        that was never the goal
    goal is coverage
        the skill must work on ALL models
        haiku is the weakest defender
        so haiku is the target
    ranking language in logs/001 and logs/003
        describes a competition that was not the point

## Anti-shortness fixes applied first

    the rubric and skill rewarded brevity
        SKILL.md said "word count falls hard"
            a shortness target
        SKILL.md section was named "Word budget"
            a budget invites minimizing
        SCORING.md deducted
            "-5 per line over 5 words with no reason"
            a model raises its score by deleting content
        nothing in the rubric rewarded readability
            five deductions, zero rewards

    over-compression is the problem microspeak solves
        the rubric was rewarding it

    changes
        removed "word count falls hard"
            replaced with "shorter is NOT the goal"
            "a longer correct answer beats a shorter lossy one, always"
        "Word budget" -> "Line length"
            one idea per line
            long line -> SPLIT into parent + child
            never trim to hit a word count
            "a 9-word line holding one idea is correct"
        SCORING.md
            deleted the over-5-words penalty
            replaced with two-ideas-in-one-line penalty
            added ABSOLUTE RULE
                never deduct against a line that preserves a fact
                line length is NOT scored

## Micro tests built

    small, one failure mode each
        02-03 sentences
        fast to iterate

    01_scope_qualifier
        targets dropping "most"
    02_state_versus_requirement
        targets merging "not done" with "still needed"
    03_unrelated_topics
        targets nesting unrelated topics under one root
    04_hedge_and_attribution
        targets compressing a hedge and its attribution

## Iteration on haiku

### cycle 1 - after anti-shortness fixes

    01  PASS - kept "most fixed"
    02  PARTIAL - dropped "still needs to happen"
        kept "deadline: before Friday"
        deadline implies pending, so weakened not erased
    03  PASS - three separate top-level topics
    04  FAIL - dropped "not mine"
        kept "Ravi's call"

### tweak - implied is not stated

    added anti-pattern
        "dropping a clause because something else implies it"
        a deadline does NOT replace "still needed"
        half of a contrast is not the contrast

### cycle 2

    02  FIXED - "still needs to happen" restored
    04  WORSE
        "not mine" still dropped
        attribution collapsed to a parenthetical
            "pool size 10→25 (Ravi)"
        output more compressed than cycle 1

    the worked example alone was not enough
        the exact "Ravi's call, not mine" case was in the file
        haiku still dropped it

### tweak - attribution is a fact

    added to KEEP list
        a "not X" clause is a fact, not decoration
        "Ravi's call, not mine" is TWO facts
            who decided
            who did not
        attribution gets its own line, never a parenthetical
            a parenthetical demotes a fact to an aside

### cycle 3

    01  PASS
    02  PASS
    03  PASS
    04  PASS
        "Ravi's call" and "not mine" both present
        own lines, no parenthetical

    all four micro tests pass on haiku

## Regression check on the original long paragraph

    FAILED - 16/17

    haiku dropped "most of the backlog" again
        output opens
            "worked through ingest pipeline backlog this week"
        no quantifier
        same failure as run 003

    two format regressions, both new
        preamble emitted
            "Looking at the skill guide and scanning my output,
                here's a refined version addressing the key points:"
        trailing commentary emitted
            "Key changes from my first pass: ..."
        skill forbids both explicitly

    merged root returned
        all six topics nested under one line
        test 03 passes this on short input
        long input reproduces the failure

    haiku asserted its own correctness, falsely
        "All facts, hedges, and quoted strings preserved"
        it had just dropped "most"

## What this run establishes

    the failures are LENGTH-DEPENDENT
        short single-topic input - haiku passes
        long multi-topic input - haiku fails
            drops the scope qualifier
            merges unrelated topics under one root
            adds preamble and commentary

    the micro tests do NOT catch the regression
        they were built from the failures
        they are too short to reproduce them
        passing all four proves less than it appears

    a micro test suite must include at least one long input
        not yet added

## Open

    haiku still fails the long paragraph
        16/17
    micro suite needs a long multi-topic case
    sonnet and opus not re-tested since the revisions
    still no control run
