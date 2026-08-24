cleared backlog
    ingest pipeline
    mostly

nightly job skipping files with spaces
    cause: curl unquoted path
    fixed: subprocess call
        argument list
        no shell involved
    files picking up correctly
        dev only

~400 files skipped
    last 2 months
    not backfilled
        decision needed
            one shot OR throttle

S3 retry count bumped
    3 -> 5
    Priya's suggestion
    uncertain: root cause addressed?
        failures were permission errors
            not transient

health endpoint
    was returning 200
        despite queue depth > alert threshold
    fixed: returns 503
        body: "queue depth exceeded: {depth}"

ingest_v1 module deleted
    nothing imported since March

parquet writer untouched
    slowest step by wide margin
