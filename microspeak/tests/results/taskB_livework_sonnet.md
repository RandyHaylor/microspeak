tracked files, sizes bytes

    CLAUDE.md, 2595
    README.md, 935
    logs/000-project-start.md, 1674
    microspeak/SKILL.md, 8351
    microspeak/tests/test_paragraph_condense_input.md, 1232
    microspeak/tests/test_paragraph_condense_scoring_key.md, 1455

worked examples in SKILL.md, 5 total

    Example 1 - short
    Example 2 - the canonical case
    Example 3 - verbose incident report
    Example 4 - decision / tradeoff
    Example 5 - answering a question

Always KEEP list

    scope qualifiers
        "some of the errors" -> "some errors", not "errors"
    hedges
        "probably", "appears", "not verified"
    negations, exceptions, conditions
    numbers, versions, paths, names, flags
    quoted user-facing strings, verbatim
    causality when non-obvious
        expressed by nesting, not "because"
    ordering when order matters
    who/what did it, when not obvious

git remote

    origin -> git@github.com:RandyHaylor/microspeak.git
    branch checked out: main
    up to date with origin/main

defects/inconsistencies found

    uncommitted staged changes present
        modified: test_paragraph_condense_input.md
        new file: test_paragraph_condense_scoring_key.md
        not yet committed to main
    only 1 of 2 test files tracked cleanly
        scoring_key file untracked until now, no test runner script found in repo
            no automation ties input file to scoring key
    SKILL.md self-check section says "any line a full sentence -> split"
        but frontmatter description itself is full-sentence prose
            inconsistent with skill's own rule, though frontmatter is metadata not skill body
    no LICENSE file
    no CI config found
