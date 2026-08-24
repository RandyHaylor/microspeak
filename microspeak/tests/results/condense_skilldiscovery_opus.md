model: opus
skill invocation captured: {'skill': 'microspeak'}
prompt: "convert this to microspeak:" + paragraph
fact score: 17/17 - PASSED

verbatim output follows

---

```
ingest pipeline backlog
    most cleared this week

nightly job silently skipping files
    any filename containing a space
    cause
        shelled out to curl
        path unquoted
    fix
        subprocess call, argument list
        no shell involved
    skipped files picking up correctly
        dev only

UNFIXED - backfill
    ~400 files skipped
        last 2 months
    not backfilled
    still needs to happen
    open decision
        one shot vs throttle
        someone must decide

S3 put retry count
    3 -> 5
    Priya's suggestion
    may not address root cause
        failures looked like permission errors
        not transient

health endpoint returned 200
    even when queue depth above alert threshold
    fixed
        now 503
        body: "queue depth exceeded: {depth}"

dead module deleted
    ingest_v1
    no imports since March

UNTOUCHED - parquet writer
    still slowest step by wide margin
```
