# Project Description - ai agent management

ai agent will assist in building the folowing


# MicroSpeak - dense information language skill for llms

Small example:
"I merged in a couple prs for the api-gateway and admin-portal repos"
can be:
"merged in prs for
 api-gateway 
 admin-portal"

It's more efficient, but MUCH more readable/scannable, and loses NO nuance or information.  

This is a skill that ai agents do not do well.

We need to create a good description of this practice, and give a few verbose examples demonstrating that NO full prose is needed to relay complex topics, and ANY filler words, phrases that can be left out SHOULD be.

It's very hard to get llm's to do this. they drop a ton of actual information when they make condensed bullets.

Approach - give some good examples for skill/prompt injection.

Don't just have 'bulleted sections' yet still have descriptive sentences and blocks of text.  The point os to remove any 'in a couple' and ALL fluff while keeping ALL relevant nuances and details.

"I identified and resolved some of the errors in the code causing our current issues. The login page was hanging on load due to a bad reference, double clicks needed to be debounced on submit button, username field updated to use our css properly. The mouseover text now properly reads 'Enter your case sensitive username here'"

Nuances - 'SOME of the errors carries critical information (that it wasn't a comprehensive fix of all visible errors). but 'terse bullets' from an llm would almost always lose that critical point.  We MUST strip down and use nested bullets, effectively removing any fluff at all in favor of  nested lists/sub lists/sub sub lists. We must aggressively avoid more than 3-5 words in a row (allowed if it makes sense to have as many words as needed)

login page hanging
	page had bad reference
	reference corrected
		page no longer hangs on load

submission duplicates
	double clicks errantly processed
	debounce solved issue

username field mouseover text wrong
	corrected, uses our css now
	now reads:
		'Enter your case sensitive username here'
		
		
		
		
# Requirements

the skill summary (what's injected automatically in every chat about the skill) should have a small version with a small example embedded in it

the skill.md file should have some good detail as I've given above, plus have more verbose examples added.

test haiku, sonnet, opus on success in condensing example paragraphs into microspeak

test haiku,sonnet,opus on success in gathering info or performing a task and then communicating back ONLY in microspeak


