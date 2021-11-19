---
layout: post
title:  "On Software Quality & Requirements"
date:   2021-11-19 8:00:00 -0800
categories: Software Quality
---

# Inspiration

My team's applications are the product of dozens - if not hundreds - of different engineers
contributions going back to 2015. That is to say, we're a fairly mature product being used
by hundreds of other engineers every day. But, how do measure quality? We report all sorts of
metrics upstream to management, but nowhere in there is a metric that measures the quality of
our code. Oh, we do have some checks like cyclomatic complexity - and other checks by linters
and tools to enforce conformance to best practices, etc.

What we do have is self-acknowledged tech debt, a backlog of Jira Issues, various TODOs 
scattered around in the code base - and overflowing good intentions to address these just as 
soon as the stars align to allow us to free up developer time to start tackling the backlog.

That is not to say me and my teammates don't do our best to address issues when we find them
in the course of working our tickets - but more that any improvement to code quality is more
of a side-effect of writing new functionality into existing code, than the goal itself.

# What is Quality?

Paraphrasing the definition as found in both ISO 9000, PMBOK, and elsewhere:
> ...the degree in which a set of inherent characteristics of an object fulfills requirements.

It's important to distinguish quality from grade when used as a metric for fit-for-purpose.
Quality is the degree in which a product fulfulls its promises and obligations, where Grade 
is the category of the product. 

# Requirements: the missing ingredient of software quality

As software engineers, we write code, unit tests, functional tests, integration tests all in the 
spirit of producing high quality software. We will create Jira tickets that detail user stories
and acceptance criteria. 

But, where do we track and trace requirements? Some companies have compliance obligations and
will employ formal requirement documentation and tracing. However, this is the exception rather
than the rule. It adds a layer of complexity and expense - both in hard dollars and developer 
time.

However, it's right there in the definition of quality - how well does our software fulfill
the _requirements_? Sure, requirements don't have to be recorded - but how well are we actual
tracking / revisiting old requirements. Often our source of truth for requirements related to
the current codebase is that senior engineer who was there the last time this module was changed
and remembers something - vaguely - about the original request. So, we end up implementing
what user A asked for without realizing the negative impact it will have on user B.

# What is needed (Opinionated)

Requirements management tools exist, but most of us don't bother using them. It's too much
book-keeping that is not seen as clear added value.

Ultimately, we have to convince ourselves, our peers, and our managers that there's value to
formal requirement tracking for any long-lived application under active development. We need
to be able to be agile (lower case agile - not opening the door to the whole Agile discussion
here), but we need _something_ to hold us accountible to the decisions made yesterday, but
yet allow those decisions to be further refined or changed today.


