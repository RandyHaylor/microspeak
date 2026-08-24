# 000 - project start

date
    2026-08-24

goal
    skill teaching llms dense lossless reporting
    named microspeak

problem being solved
    llms condense lossily
        "be brief" -> facts dropped
        "use bullets" -> bullets still prose
    high-value casualties
        scope qualifiers
            "some of the errors" -> "errors"
            incompleteness IS information
        hedges
        unfixed / untouched items

design decisions

    skill description field
        must carry a working micro-example
        it is the only text auto-injected
        chose the api-gateway / admin-portal pair
            shortest case that shows the shape

    SKILL.md written IN microspeak
        the file demonstrates the format it teaches
        fenced code blocks used for all examples
            markdown collapses leading whitespace otherwise
            indentation is the entire grammar - must survive render

    explicit DROP list and KEEP list
        DROP list alone produced lossy output in prior art
        KEEP list is the anti-lossy guard
        KEEP leads with scope qualifiers, deliberately

    5 worked examples, escalating length
        1 - one-liner
        2 - canonical login/debounce/mouseover case from brief
        3 - long incident report, hedges + unfixed item
        4 - decision/tradeoff, preference not decision
        5 - answering a question, "partially" not "yes"

    self-check block at end
        five backward-looking questions
        targets the specific failure modes above

next
    test haiku / sonnet / opus
        task A - condense a paragraph
        task B - perform real work, report only in microspeak
