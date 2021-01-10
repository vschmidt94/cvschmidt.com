---
layout: post
title:  "Book Notes: Clean Code by R. Martin"
date:   2020-12-27 8:00:00 -0800
categories: ComputerScience Books
---
I want to take another pass through Uncle Bob's (a.k.a. Robert Martin) book, _Clean Code_.

A lot of my work lately has been trending towards overhaul & refactoring legacy modules that have been modified, patched, and
Frakenstein'd for years. This typically starts with a new feature request, which seems simple enough on the surface -
but once I get into the modules in question, some of the accrued technical debt means it's not as simple as it could be.

I want to avoid giving the wrong impression though: I think our particular code base is in fairly average condition
given its age, size, complexity, and number of contributors. It's just time to bring some of the _Boy Scout Rule_
he mentions right in Chapter 1: **Leave the campground better than you found it.**

## Book Notes != Book Review

To be clear, the purpose of this post is a place to collect my own notes as I read through the book. Uncle Bob is going
to explain some things that reasonate with me strongly, and probably there will be things I disagree with as well.

My goal is 1 chapter a every day or two, and I'll just continually update this post until I'm finished. What I hope to
produce in the end is a Cliff Notes-ish post that will be useful for me to circle back to in the future.

## Chapters
### 1. Clean Code

* LeBlanc's law: _Later equals never_ 
  * I need to remember this one for Kanban review and planning meetings when we kick the can.
  * Corollary (or something): _Perfect is the enemy of done_
* Various takes on the idea of Clean Code by big names in CS
* _Making code easier to read actually makes it easier to write_
* Boy Scout rule: _Leave the campground better than you found it._

### 2. Meaningful Names

No suprises here, agree with everything, a couple of highlighted notes:
* Clarity is king
* Don't be afraid to rename if you come up with something better
* Don't add gratuitous context

This is something every team I've been on has been about the same stage of acceptance: The benefit of longer / more
descriptive names for everything across the board outweighs the cost of the longer name. Still, if you can be concise
and short - that's even better. Just don't be short named and vague.

### 3. Functions

* Keep them small!
* Functions should do one thing, do it well, and do it only
  * "If a function does only those steps that are one level below the stated name of the function, then the function is
  doing one thing"
* Code should read like a top-down narrative
* By their nature, switch statements do N things
* Use descriptive names for functions
  * "A long descriptive name is better than a long descriptive comment"
* Ideal number of arguments is 0, followed by 1, then 2.
  * Boy, do I have a lot to work on here.
  * more arguments = more testing / harder testing
  * A boolean argument is really, really bad
    * Means the function does 2 things
    * IMO, maybe not that bad... essentially lets you choose a strategy - but I get his point.
* Functions should not have side effects
  * "Side effects are lies"
* Function should do something or answer something - not both
* Exceptions > Returning error codes
  * Lets you separate error handling from happy path
  * Error handling qualifies as "one thing" - so have error handling functions
* DRY
* Structured Programming - the old single entry / single exit:
    * If functions are small, so what if you return early
    * Personally, I like early bail outs when justified, it cuts the mental clutter of what the possible cases are by
      tying off loose ends early.
* It is not natural to write code like this:
    * Start with getting the logic down, then:
        * refactor! refactor! - try different things

### Comments

* "Don't comment bad code - rewrite it" - Kernigham & Plaugher
* "The proper use of comments is to compensate for our failure to express ourself in code." - Uncle Bob
* Comments lie
* Become maintainabilty issue - code evolves, comments don't 
* Code is the source of truth
* Spend effort to minimize comments
* Acceptable as Explanation of intent, warning of consequences

The chapter goes into a lot more details and specific examples that are worthwhile to review, but the above
bullets capture the essence.

### Formatting

* Formatting is important
* ... is about communcation
* Vertical density implies close associations
* Declare variables as close to their useage as possible
* Instance variables should be declared at top of class
* Dependent functions should be vertically close
* Functions with high conceptual affinity should be close
* Vertical ordering -> call dependencies should point downward
* Horizontal formatting - 80 chars is arbitrily short, but don't go too long either
* Indentation helps visualize structure, and also too deeply nested code
* Follow team rules, use static analysis

### Objects and Data Structures

