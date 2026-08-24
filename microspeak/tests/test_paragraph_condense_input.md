# Condensation test input

Condense the paragraph below into MicroSpeak. Output the MicroSpeak only.

---

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

---

## Facts that must survive (scoring key — do not show to the model under test)

1. most of backlog, not all
2. nightly job silently skipping files with spaces in name
3. cause: shelling out to curl, path unquoted
4. fix: subprocess with argument list, no shell
5. verified in dev only
6. ~400 files skipped over last two months, NOT backfilled
7. open decision: backfill one shot vs throttled
8. S3 put retry count 3 -> 5
9. attribution: Priya's suggestion
10. hedge: may not address root cause
11. reason for hedge: failures looked like permission errors, not transient
12. health endpoint returned 200 above queue depth alert threshold
13. now returns 503
14. body verbatim: "queue depth exceeded: {depth}"
15. deleted dead ingest_v1 module, unimported since March
16. parquet writer untouched
17. parquet writer still slowest step by wide margin
