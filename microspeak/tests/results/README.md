# What each result file is

Two run types live here. They are NOT comparable, and only one of them is a
real test of the skill.

## `*_skilldiscovery_*` - real skill test

```
setup
    isolated folder, .claude/skills/microspeak/SKILL.md
    claude CLI, cwd = that folder
    --setting-sources project
        user-level skills excluded
prompt
    "convert this to microspeak:" + the paragraph
    skill never named as a file
    model never told to read anything
verification
    Skill tool invocation captured from stream-json
    proof the skill was discovered, not pasted
```

## `taskA_condense_*` and `taskB_livework_*` - NOT a skill test

```
these were run before the setup above existed

prompt began with
    "Read /path/to/SKILL.md and follow it as your output format instruction"

so they measure
    how well a model follows an explicit instruction document
        handed over under direct order
they do NOT measure
    whether the skill triggers
    whether the description field works
    anything about skill discovery

kept for history, not for scoring the skill
    see logs/003
```
