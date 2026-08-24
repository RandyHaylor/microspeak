tracked files
	6 total
	CLAUDE.md
		2595 bytes
	README.md
		935 bytes
	logs/000-project-start.md
		1674 bytes
	microspeak/SKILL.md
		8351 bytes
	microspeak/tests/test_paragraph_condense_input.md
		1232 bytes
	microspeak/tests/test_paragraph_condense_scoring_key.md
		1455 bytes

SKILL.md worked examples
	5 total
	Example 1 - short
	Example 2 - the canonical case
	Example 3 - verbose incident report
	Example 4 - decision / tradeoff
	Example 5 - answering a question

Always KEEP list
	scope qualifiers
	hedges
	negations, exceptions, conditions
	numbers, versions, paths, names, flags
	quoted user-facing strings, verbatim
	causality when non-obvious
		express by nesting, not by "because"
	ordering when order matters
	who/what did it when not obvious

git status
	remote: git@github.com:RandyHaylor/microspeak.git
	branch: main
	up to date with origin/main
	working tree: 1 modified file, 1 untracked file

defects found

CLAUDE.md
	line 3: "folowing" typo
		should be "following"
	line 25: "os to" typo
		should be "is to"

SKILL.md
	Always KEEP section, scope qualifiers subsection
		"NOT -> "errors"" unclear formatting
		reads like incomplete transformation rule
		likely meant to express negation but syntax breaks meaning

working tree inconsistency
	test_paragraph_condense_scoring_key.md
		git status: Untracked files
		git ls-files: present, tracked
		git index: present with hash 74eb1144
		contradiction: appears tracked yet status reports untracked
