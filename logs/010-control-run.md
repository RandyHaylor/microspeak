# 010 - control run

date
    2026-08-24

this closes the UNVERIFIED claim opened in logs/001

## Setup

    control folder
        /home/aikenyon/ai_skills_agents_resources/microspeak_control_no_skill_session
        no .claude directory at all
        --setting-sources project
            user-level skills excluded
        no skill can load

    prompt
        "condense this into terse bullets:" + the text
        the naive instruction the skill is meant to beat
        the word "microspeak" never appears

    scope, kept small by request
        2 tests - 07, 08
        2 models - haiku, opus
            weakest and strongest, to bracket the range
        sonnet skipped for cost

## opus control - ALL FACTS KEPT, both tests

    07 - 18/18
        US still on old index - kept
        cutover not yet scheduled - kept
        NOT real traffic - kept
        Friday morning - kept
        "unrelated" on both the spike and the rename - kept

    08 - 15/15
        "Priyanka wrote the export script; I only ran it"
            the contrast survives via the pairing

## haiku control - FACTS LOST, both tests

    07
        DROPPED  "not on real traffic"        HV
        DROPPED  "Friday morning"
        DROPPED  "unrelated" on the flag rename  HV
        DEGRADED "cutover NOT scheduled"
            became "US pending cutover"
            pending implies queued
            the source says not scheduled
        DEGRADED "US still on old index"
            folded into "US pending cutover"
            the old-index state is no longer stated

    08
        DROPPED  "not me"                     HV

        WRONG VALUE - actor swapped

            haiku control
                "Export script by Priyanka; you ran it"
            source
                "Priyanka wrote the export script,
                    not me, I only ran it"

            "I only ran it" became "you ran it"
            the speaker's own action reassigned to the reader
            this is the wrong-value category from SCORING.md
                a fact present and false
            with the skill loaded haiku wrote
                "speaker ran only"
                correct

## What the control actually establishes

    the causal claim from logs/001 was
        "the KEEP list is doing the work"
    marked UNVERIFIED then
    now testable

    verdict - TRUE FOR HAIKU, NOT SHOWN FOR OPUS

        haiku
            without skill - loses high-value facts, swaps an actor
            with skill    - keeps them
            the skill is doing real work

        opus
            without skill - keeps every fact on both tests
            with skill    - keeps every fact
            no fact-retention benefit demonstrated
                on these two tests

    so the skill's fact-retention value is
        large at the weak end
        unproven at the strong end
    my earlier framing implied it carried all three models
    on these tests it does not

## What the skill changes at EVERY tier

    structure

        control output, all models
            flat markdown bullets
            bold headers
            prose fragments inside bullets
            em-dashes and semicolons joining ideas
            NO hierarchy

        with skill, all models
            nested trees
            one idea per line
            relationships carried by indentation

    so the shape change is universal
    the fact-retention change is not

## Honest limits of this control

    2 tests, 2 models, 1 run each
    no repetition, so run-to-run variance is unmeasured
    sonnet never controlled
    the naive prompt is one phrasing
        "condense this into terse bullets"
        a different naive prompt might score differently
    opus keeping 18/18 and 15/15 once
        does not prove it always would
