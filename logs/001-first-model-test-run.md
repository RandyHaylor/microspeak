# 001 - first model test run

date
    2026-08-24

setup
    3 models
        haiku, sonnet, opus
    2 tasks each
        A - condense a fresh paragraph
        B - real investigation, report only in microspeak
    each agent
        told to read SKILL.md, follow it
        told final response must be microspeak only
        blocked from reading the scoring key
    raw outputs
        microspeak/tests/results/
        verbatim, unedited

---

## Task A - condensation

fact retention, out of 17

    haiku   17/17
    sonnet  17/17
    opus    17/17

all three high-value facts groups survived

    scope qualifier "most of"
        haiku   "mostly"
        sonnet  "mostly cleared"
        opus    "most of ... not all"
    dev-only verification
        all three
    ~400 files NOT backfilled
        all three
    open decision, one-shot vs throttle
        all three
    Priya attribution
        all three
    hedge on root cause + permission-error reason
        all three
    parquet writer untouched + still slowest
        all three
    quoted string "queue depth exceeded: {depth}"
        all three, verbatim

result
    zero fact loss across all three models
    including haiku

UNVERIFIED - no control run
    no baseline was measured
    the same paragraph was never condensed
        without the skill loaded
    so this run does NOT show the skill caused the retention
    it shows only that retention was total WITH the skill
    control run required before any causal claim
        same 3 models
        same paragraph
        prompt: "condense this into terse bullets"
        next round

format quality

    opus    best
        "not all" as its own child line
            most explicit preservation of the scope qualifier
        NOT-touched flagged in caps
    haiku   close second
        tightest lines
        "uncertain: root cause addressed?" - good compression of the hedge
    sonnet  weakest of the three
        several lines run long
            "was returning 200 even when queue depth above alert threshold"
            11 words, could nest
        "still needs to happen" redundant beside "backfill NOT done"

no model produced
    preamble
    sign-off
    prose sentences with dashes

---

## Task B - real work, report only in microspeak

all three
    completed the investigation
    reported in microspeak
    no preamble, no sign-off

haiku
    correct facts
    found 2 real typos in CLAUDE.md
        "folowing", "os to"
    flagged the KEEP list line
        'NOT -> "errors"'
        called it unclear formatting
        FAIR - the line is ambiguous out of context
    reported a git contradiction
        status untracked vs ls-files tracked
        STALE READ - it observed mid-commit
        not a repo defect

sonnet
    correct facts
    flagged uncommitted staged changes
        also a stale read, same cause
    real findings
        no test runner
        no LICENSE
        no CI

opus
    strongest output of the six
    found genuine design defects in the skill itself
        1  DROP vs KEEP conflict on "I"
            DROP list says drop "I" as subject
            Example 3 keeps "I did not fix"
            no stated exception
            models will resolve arbitrarily
        2  synthesized parent headers undocumented
            Example 2 head "submission duplicates"
            phrase not in the source prose
            legitimate, but no rule permits it
        3  scoring procedure absent
            key says weight high-value facts
            no weight given, no threshold
            cross-model comparison not reproducible
    format flaw
        wrapped entire output in a code fence
        instruction was microspeak only

---

## Conclusions

    the KEEP list may be doing the work
        untested - see UNVERIFIED above
        hypothesis, not finding
        keep it first-class until the control run says otherwise

    17/17 on all three models means the paragraph
        did not discriminate between models
        task A needs a harder input next round
            longer, more hedges, more interleaved topics

    task B discriminated well
        depth of findings scaled with model
        format compliance was flat - all three fine

    stale git reads by two models
        caused by commits landing mid-run
        not a skill problem
        future runs - quiesce the repo first

## Actions taken from this run

    see logs/002
