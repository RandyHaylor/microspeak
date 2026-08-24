most of ingest backlog cleared
    this week
    not all

nightly job silently skipping files
    filenames containing space
    cause
        shelling out to curl
        path unquoted
    fix
        subprocess call, argument list
        no shell involved
    skipped files picking up correctly
        in dev

backfill NOT done
    ~400 files skipped
        last two months
    still needs to happen
    open decision
        one shot vs throttled

S3 put retry count 3 -> 5
    Priya's suggestion
    may not address root cause
        observed failures looked like permission errors
        not transient

health endpoint wrong status
    returned 200 above queue depth alert threshold
    fixed
        now returns 503
        body:
            "queue depth exceeded: {depth}"

dead ingest_v1 module deleted
    nothing imported it since March

parquet writer NOT touched
    still slowest step by wide margin
