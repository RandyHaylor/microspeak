# 003 - first real skill test

date
    2026-08-24

## Why runs 001 was not a skill test

    every agent prompt in run 001 began
        "Read /path/to/SKILL.md
            and follow it as your output format instruction"

    so run 001 measured
        can a model follow an explicit instruction document
            handed to it under direct order

    run 001 did NOT measure
        does the skill trigger on its own
        does the description field work
            CLAUDE.md required that field carry the example
            it was built, never exercised
        anything about skill discovery

    the skill was never installed anywhere during run 001
        verified - not in ~/.claude/skills/
        verified - project had no .claude/ directory at all

    calling run 001 a skill test was wrong
        the 17/17 result describes instruction-following
        not skill behavior

## Run 003 setup - real discovery

    isolated folder
        /home/aikenyon/ai_skills_agents_resources/microspeak_skill_live_test_session
        .claude/skills/microspeak/SKILL.md
        nothing else in it
            no repo, no logs, no prior outputs
            models cannot stumble on examples

    claude CLI, cwd = that folder
        -p, non-interactive
        --setting-sources project
            excludes all 23 user-level skills
        --output-format stream-json
            captures tool invocations

    prompt, complete
        "convert this to microspeak:" + paragraph
        skill never named as a file
        no instruction to read anything
        no description of the format

    verification method
        parse stream-json for Skill tool_use blocks
        proves discovery, not assumption

## Result - discovery works

    all 3 models invoked the skill unprompted

        haiku   Skill{skill: microspeak}
        sonnet  Skill{skill: microspeak, args: <full paragraph>}
        opus    Skill{skill: microspeak}

    the word "microspeak" in the prompt was enough
        description field did its job
        this is the first evidence it works

    mechanical difference, unexplained
        sonnet passed the paragraph as args
        haiku and opus passed no args
        haiku stream was 166 lines
            sonnet 10, opus 8
        I do not know why
            not investigated

## Result - fact retention under real discovery

    scored against the same 17-fact key

        haiku   16/17  FAILED
        sonnet  17/17  passed
        opus    17/17  passed

    haiku lost fact 1
        "most of the backlog"
        its output opens "ingest pipeline backlog"
            no quantifier at all
        this is a high-value fact
            SCORING.md - any high-value loss = run failed

    this is the failure the skill exists to prevent
        a completeness qualifier dropped
        reader concludes the backlog is cleared
        it is not

    haiku did NOT lose this fact in run 001
        run 001 - ordered to read the whole file
        run 003 - skill loaded through normal discovery
        same model, same paragraph, different result

    what this means
        being ordered to read SKILL.md is stronger
            than the skill loading normally
        the 17/17 across all models in run 001
            overstated what the skill delivers
        run 003 is the honest number

    opus and sonnet both kept it
        sonnet  "most cleared this week"
        opus    "most cleared this week" as a child line

    opus additionally
        flagged UNFIXED - backfill
        flagged UNTOUCHED - parquet writer
        strongest output of the three

## Format notes

    haiku and opus wrapped output in a code fence
        prompt did not say "microspeak only"
        so a fence is reasonable presentation here
        not scored as a failure
            SCORING.md deduction applies only when
                the prompt demanded microspeak only

    haiku emitted trailing-whitespace-only lines
        inside its nesting
        cosmetic

    sonnet produced no fence, no preamble
        cleanest raw form

## Open

    haiku fact-1 loss needs a skill fix
        the KEEP list leads with scope qualifiers already
        it was not enough for haiku under normal load
        not yet addressed

    task B equivalent not yet run under real discovery
        "use microspeak" on a real work task
        run 001 version was instruction-following only

    still no control run
        no baseline without the skill
