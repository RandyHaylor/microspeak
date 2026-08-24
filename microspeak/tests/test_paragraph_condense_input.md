# Condensation test input (task A)

Okay so I finally got through most of the backlog on the ingest pipeline this
week. The big one was that the nightly job had been silently skipping any file
whose name contained a space, because we were shelling out to a curl command
without quoting the path — I switched that to a subprocess call with an argument
list, so no shell involved anymore, and the skipped files are picking up
correctly now in dev. I have not backfilled the roughly 400 files that were
skipped over the last two months; that still needs to happen and someone should
decide whether we backfill in one shot or throttle it. I also bumped the retry
count from 3 to 5 on the S3 put, which was Priya's suggestion, though honestly
I'm not sure it addresses the root cause since the failures we saw all looked
like permission errors rather than transient ones. Two smaller things: the
health endpoint was returning 200 even when the queue depth was above the alert
threshold, that's fixed and it now returns 503 with the body
"queue depth exceeded: {depth}", and I deleted the dead ingest_v1 module that
nothing has imported since March. I did not touch the parquet writer, which is
still the slowest step by a wide margin.
