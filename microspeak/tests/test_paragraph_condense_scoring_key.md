# Scoring key - task A

Do NOT show this file to a model under test.

17 facts must survive condensation. Score = facts present / 17.

```
1   most of backlog, not all
2   nightly job silently skipping files with spaces in name
3   cause: shelled out to curl, path unquoted
4   fix: subprocess with argument list, no shell
5   verified in dev only
6   ~400 files skipped over last two months, NOT backfilled
7   open decision: backfill one shot vs throttled
8   S3 put retry count 3 -> 5
9   attribution: Priya's suggestion
10  hedge: may not address root cause
11  hedge reason: failures looked like permission errors, not transient
12  health endpoint returned 200 above queue depth alert threshold
13  now returns 503
14  body verbatim: "queue depth exceeded: {depth}"
15  deleted dead ingest_v1 module, unimported since March
16  parquet writer untouched
17  parquet writer still slowest step by wide margin
```

## High-value facts

These are the ones lossy condensation kills first. Weight them when comparing
models.

```
1   "most of" - scope qualifier
5   dev only - not prod
6   not backfilled - unfinished work
7   open decision - needs a human
9   attribution
10  hedge
11  hedge reason
16  untouched - unfinished work
```

## Format failures to note separately from fact loss

```
prose sentences inside bullets
flat list, no nesting
preamble ("Here's the condensed version:")
sign-off ("Let me know if...")
filler surviving inside lines
```
