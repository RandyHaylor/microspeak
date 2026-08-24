# 08 held-out key

Why this test exists

```
SKILL.md Example 6 is the 05 paragraph verbatim
    05 is now a memorization check, not a generalization check
    haiku can read the answer in the skill

08 carries the SAME failure patterns
    different domain, different wording
    never appears in SKILL.md
    this is the honest generalization test
```

## Target patterns, same as 05

```
A  contrast clause in a long report
    05 - "Wei found it, not me"
    08 - "Priyanka wrote the export script, not me"
    plus a third half 05 lacks
        "I only ran it"
        the speaker's actual role, separate fact

B  parent naming that could over-claim
    05 - iOS under "shipped 4.2"
    08 - Quebec under "Ontario export"
        Quebec was skipped ENTIRELY
        nesting it under an Ontario parent is FALSE

C  a scoped measurement
    05 - "on wifi" with "no cellular numbers at all"
    08 - "validated against sample checksums"
         "but not against the full set"

D  a scope qualifier
    05 - "about half the install base"
    08 - "roughly 80 percent of their records"
```

## Facts - 15

```
1   HV  Ontario export finished, ~80 percent of records, not all
2       the 14th
3   HV  Quebec tenants skipped ENTIRELY
4       reason - different retention policy
5   HV  NOT decided how to handle Quebec
6       validated against sample checksums
7   HV  NOT validated against the full set
8   HV  hedge - "would not call it verified"
9   HV  Priyanka wrote the export script
10  HV  explicitly NOT the speaker
11  HV  speaker only ran it
12      CSV header emitted 'client_id'
13      downstream expects 'clientId'
14      corrected now
15  HV  archive job never re-enabled, still paused
```

verbatim strings
```
'client_id' and 'clientId' must both appear exactly
    they differ only by underscore and case
    an altered quote is a wrong value, not a near miss
```

## Automatic failure

```
Quebec nested under any Ontario-scoped parent
    -> FALSE indent -> run failed

"not me" dropped
    -> HV loss -> run failed

'client_id' or 'clientId' altered
    -> wrong value on a quoted string -> run failed
```
