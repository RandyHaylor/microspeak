# 07 nesting traps - scoring key

This test scores NESTING TRUTH first. Facts alone do not pass it.

## The four traps

```
TRAP 1 - US region under the rollout
    source: EU rolled out, US still on old index
    FALSE indent
        "US region" nested under "search index rollout"
        asserts US was part of the rollout
    US must be a sibling, or a topic of its own

TRAP 2 - latency spike under the rollout
    source explicitly DENIES this causation
        "was not caused by the index rollout"
    FALSE indent
        latency spike nested under rollout
    this is the strongest trap
        topic adjacency pulls hard
        the source denies it outright

TRAP 3 - autoscaling rule parented wrongly
    the rule is the CAUSE of the latency spike
    correct
        latency spike -> caused by Fatima's autoscaling rule
    wrong
        autoscaling rule nested under the rollout

TRAP 4 - flag rename nested under search work
    source: "unrelated to any of this, just cleanup"
    topically it is search team work
    source denies the relationship
    must be its own top-level topic
```

## Facts required

```
1   HV  new search index rolled out to EU only
2       Thursday
3   HV  US region still on OLD index
4   HV  cutover NOT scheduled
5       relevance improved ~12 percent in EU
6   HV  measured on internal eval set ONLY
7   HV  not measured on real traffic
8       latency spike seen Friday
9   HV  NOT caused by the index rollout
10      cause - bad autoscaling rule
11  HV  attribution - Fatima pushed it
12      Friday morning
            wrong value if reported as Thursday
            Thursday is the rollout day, a plausible wrong anchor
13      rule reverted
14      latency recovered within the hour
15      'fuzzy_match' renamed to 'typo_tolerance'
16      verbatim flag names, both
17  HV  rename unrelated to everything else
18      rename is just cleanup
```

## An acceptable shape

```
search index - EU only
    rolled out Thursday
    relevance +12 percent
        internal eval set ONLY
        NOT real traffic

US region
    still on old index
    cutover NOT scheduled

latency spike Friday
    NOT caused by index rollout
    cause - bad autoscaling rule
        Fatima pushed it
        same morning
    rule reverted
        latency recovered within the hour

flag rename - unrelated, cleanup
    'fuzzy_match' -> 'typo_tolerance'
```

## Automatic failure

```
any indent that places
    US region        under the rollout
    latency spike    under the rollout
    flag rename      under any search index work
-> FALSE indent -> run failed
```
