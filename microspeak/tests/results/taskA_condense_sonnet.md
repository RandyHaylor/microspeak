ingest pipeline backlog, mostly cleared this week

nightly job skipping filenames with spaces
    cause: curl shell-out, path unquoted
    fixed: switched to subprocess with argument list
        no shell involved now
    skipped files picking up correctly in dev

backfill NOT done
    ~400 files skipped, last 2 months
    still needs to happen
    open decision: one-shot vs throttled

S3 put retry count 3 -> 5
    Priya's suggestion
    not sure it fixes root cause
        observed failures looked like permission errors
        not transient

health endpoint false 200s
    was returning 200 even when queue depth above alert threshold
    fixed: now returns 503
        body: "queue depth exceeded: {depth}"

dead code removed
    ingest_v1 module deleted
    unused since March

parquet writer
    not touched
    still slowest step, by a wide margin
