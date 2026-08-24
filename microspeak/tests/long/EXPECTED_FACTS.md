# Long test expected facts

Long multi-topic inputs. These reproduce the failures the micro tests are
too short to trigger.

High-value facts marked HV. Any HV loss = run failed.

## 05_staged_release - 18 facts

```
1   HV  shipped to ~HALF the Android install base, not all
2       4.2 release
3       staged rollout
4       Tuesday
5   HV  NOT promoted to remaining users
6       crash-free sessions 99.4 percent
7       slightly better than 4.1
8   HV  hedge - sample only 2 days old, would not read much into it
9       camera permission prompt appeared twice on first launch
10      biggest fix in the build
11      cause - duplicate call in onboarding flow
12  HV  Wei found it, NOT the speaker
13      prompt verbatim - 'Allow PhotoSync to use your camera?'
14      now appears once
15      upload chunk size 1 MB -> 4 MB
16      cut median upload time roughly in half ON WIFI
17  HV  no cellular numbers at all
18  HV  iOS build not touched, still on 4.1, no timeline
19  HV  rollback script never tested against staged rollout, only full
```

count is 19 lines; facts 9 and 10 are one item split for clarity

## 06_warehouse_migration - 20 facts

```
1   HV  MOST reporting workloads migrated, not all
2       off Redshift, onto new warehouse
3       2 remain
4       finance month-end job
5       churn model feed
6       both blocked on the same cause
7       cause - Redshift-specific UNLOAD syntax
8       new engine does not support it
9       Marcus thinks generic COPY would work
10  HV  attribution - Marcus
11  HV  Marcus has NOT tried it
12      query cost ~$8,400/mo -> $5,100
13      based on first partial month
14  HV  hedge - treat that number as soft
15      migration broke the daily 6am email
16      sends 6am UTC instead of 6am Eastern
17      nobody noticed for 9 days
18      that is fixed
19  HV  NOT audited whether other scheduled jobs share the timezone assumption
20  HV  still paying for Redshift cluster in parallel, until last 2 jobs move
```

## Failure modes these are built to catch

```
scope qualifier dropped on a long input
    "about half" / "most of"
unrelated topics merged under one root
preamble or trailing commentary appearing
unfinished work reading as finished
scope of a measurement dropped
    "on wifi" without "no cellular numbers"
```
