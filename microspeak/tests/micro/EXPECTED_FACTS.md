# Micro test expected facts

Each test is 2-3 sentences and targets ONE failure mode observed in haiku.
Not a ranking exercise. The bar is: every model keeps every fact.

## 01_scope_qualifier - targets dropping "most"

```
1  MOST of flaky tests done, not all      <- the target fact
2  auth suite
3  2 tests timing out
4  cause: waiting on real network call
5  stubbed those
6  billing suite NOT looked at at all
```

haiku failure this reproduces
```
dropped "most of the backlog" in the big test
```

## 02_state_versus_requirement - targets merging two facts that look redundant

```
1  migration script NOT run against production   <- state
2  still needs to happen                         <- requirement, separate fact
3  deadline: before Friday
4  Dana prefers maintenance window
5  attribution: Dana
6  Dana NOT sure window is long enough           <- hedge, hers not ours
```

facts 1 and 2 are different
```
work can be undone AND cancelled
keeping only one loses which case this is
```

## 03_unrelated_topics - targets nesting everything under one root

```
1  log retention 7 -> 30 days
2  staging db restored from Tuesday snapshot
3  on-call rotation now includes Marcus
4  the three are unrelated                       <- explicit in source
```

required shape
```
3 separate top-level topics
NOT one root with 3 children
```

haiku failure this reproduces
```
six unrelated topics nested under "ingest pipeline backlog"
```

## 04_hedge_and_attribution - targets compressing the hedge and its reason

```
1  connection pool 10 -> 25
2  attribution: Ravi's call, explicitly not the speaker's
3  hedge: doubts it fixes timeouts
4  hedge reason: slow queries showed as lock waits
5  not pool exhaustion
6  did not make anything worse in staging
```

fact 2 nuance
```
"which was Ravi's call, not mine"
    both halves matter
    speaker is distancing from the decision
```
