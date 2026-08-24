```
repo
    /home/aikenyon/ai_skills_agents_resources/microspeak
    git: yes
    branch: main
        tracks origin/main, up to date
    remote origin
        git@github.com:RandyHaylor/microspeak.git
        fetch + push, same url
    working tree clean

tracked files - 6

    CLAUDE.md
        2595 bytes
    README.md
        935 bytes
    logs/000-project-start.md
        1674 bytes
    microspeak/SKILL.md
        8351 bytes
    microspeak/tests/test_paragraph_condense_input.md
        1232 bytes
    microspeak/tests/test_paragraph_condense_scoring_key.md
        1455 bytes

SKILL.md worked examples - 5

    Example 1 - short
    Example 2 - the canonical case
    Example 3 - verbose incident report
    Example 4 - decision / tradeoff
    Example 5 - answering a question

Always KEEP list - 8 entries

    scope qualifiers
        "some of the errors" -> "some errors"
        NOT -> "errors"
        the incompleteness IS the information
    hedges
        "probably", "appears", "not verified"
    negations, exceptions, conditions
    numbers, versions, paths, names, flags
    quoted user-facing strings, verbatim
    causality when non-obvious
        express by nesting, not by "because"
    ordering when order matters
    who/what did it when not obvious

defects / inconsistencies

    task B test assets missing
        CLAUDE.md requires 2 test tracks
            A - condense paragraphs
            B - do work, report only microspeak
        logs/000 "next" names both
        only task A input + key tracked
        tests/ has no task B file at all

    no results log
        logs/ holds only 000-project-start.md
        README describes logs/ as
            "every experiment, result, and revision"
        zero test runs recorded
        3 models x 2 tasks all unrun

    DROP vs KEEP conflict on "I"
        DROP list: "I / we / you as subject"
        Example 3 microspeak keeps "I did not fix"
            its note calls that preservation correct
        KEEP has "who/what did it when not obvious"
            covers it only by inference
        no stated exception rule
            models will resolve it arbitrarily

    no scoring procedure
        key gives facts / 17
        high-value facts listed - 8
            "weight them" stated
            no weight value given
        format failures listed
            "note separately"
            no scale, no pass threshold
        cross-model comparison not reproducible

    no test runner
        tests/ is prose only
        scoring by hand, unspecified who

    Example 2 head invented
        prose has no "submission duplicates" phrase
        derived from debounce sentence
        acceptable, but undocumented
            no note that headers may be synthesized

    repo hygiene
        no LICENSE
        no .gitignore
        tests/ has no README
            key warns "do NOT show to model under test"
            warning lives inside the key only
```
