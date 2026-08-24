# MicroSpeak

A Claude Code skill for dense, lossless reporting.

```
fragments over sentences
indentation over connectives
zero words dropped that carry meaning
zero words kept that do not
```

## The problem

```
llms condense badly
    told "be brief" -> drop facts
    told "use bullets" -> bullets are still prose
lost first, always
    scope qualifiers - "some of the errors"
    hedges - "not verified in prod"
    unfixed items
```

## The example

prose

```
I merged in a couple prs for the api-gateway and admin-portal repos
```

microspeak

```
merged prs
    api-gateway
    admin-portal
```

## Install

```
cp -r microspeak ~/.claude/skills/
```

or per-project

```
cp -r microspeak .claude/skills/
```

## Layout

```
microspeak/SKILL.md
    the skill
microspeak/tests/
    test inputs + scoring keys
logs/
    breadcrumb history
    every experiment, result, and revision
CLAUDE.md
    original project brief
```
