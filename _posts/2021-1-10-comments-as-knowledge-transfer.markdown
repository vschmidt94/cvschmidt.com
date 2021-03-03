---
layout: post
title:  "Code comments as knowledge transfer"
date:   2021-1-9 12:00:00 -0800
categories: software
---
## Uncle Bob vs. Me

In another post: [Clean Code by R. Martin]{% post_url 2020-12-27-book-notes-martin-clean-code %}, I am keeping 
some running notes as I re-read the Uncle Bob's well known book.

Chapter 4: _Comments_ made me start questioning myself, and my own use of comments. Along the lines of "Hello,
my name is Vaughan, and I am a code commenter." _Do I really have a problem and am I hiding it from myself?_

Possibly, but on closer inspection perhaps it is not as bad as it appears.

## Where Clean Code gets it right

In principle I agree with everything Robert Martin has put into the _Comments_ chapter:

* "Don't comment bad code - rewrite it" - Kernigham & Plaugher
* "The proper use of comments is to compensate for our failure to express ourself in code." - Robert Martin
* Comments lie
* Become maintainabilty issue - code evolves, comments don't 
* Code is the source of truth
* Spend effort to minimize comments

I don't disagree with any of this, and when I find myself writing a comment, I always try to take a second
pass to eliminate the need for the comment. Often a little refactoring goes a long way to remove the need
for a comment.

## The missing case for comments: Knowledge Capture & Transfer

I am biased by the code bases I've worked on professionally. They've been mature (read: long-lived) code
bases that are still constantly evolving as technologies and business needs evolve.

What I've found in practice is that comments are invaluable for *knowledge transfer*.

As software developers, we find ourselves translating business needs and customer requirements to code.
Sometimes it is very straightforward, but many times it is not. We have to develop an understanding of
the underlying business reasons and user expectations in the business domain, which we are likely not
experts in ourselves. We do this by talking to the customers & users, other managers, doing our own
research, etc. 

At the end of this process, we are mentally holding a bunch a details that use to inform the writing of
the code. Usually in a matter of days, weeks, and possibly months - we've become the subject matter 
expert on the dev team for the module we are working on.

Then one day the module is magically finished, merged into mainline, and we pick up a new ticket to
start working, and move on with new issues.  Before long, some other developer has to go work in that 
module we knew so much about, and learned the intricate details. Good comments can help this other
developer (or even future us who has forgotten some of the details) understand the reasoning and 
implementation choices that were made at the time.

### Example: Realistic depiction of runway thresholds on graphical flight displays

This is one of the issues I worked at Garmin. At the time, Garmin's flight displays had a generic
visualization of 8 runway threshold stripes that was used on all runways. It helped make the 
runway displayed on the moving map "look" like a runway.

In the quest for continual product improvement, somebody realized that in fact, "real world" 
runway markings were much more complicated - and different markings conveyed different 
information to the pilot about to land on the runway.

In the process of implementing the feature improvement - which started out as the simple request
"Runway threshold stripes should correctly match the use of stripes on the actual runway", I ended
up learning quite a bit about runway markings. I learned a lot of details from the 
[FAA's AC150/5300 Airport Design Standards](https://www.faa.gov/airports/resources/advisory_circulars/index.cfm/go/document.current/documentNumber/150_5300-13).

The first implementation of the new logic was merged with much rejoicing... until a few weeks later
feedback started coming in from the test pilots along of the lines of "the new runway lines seem to dance
and flash as we land, it is distracting". That was indeed a problem - so back to the drawing board.

To spare the details, we had to make changes and compromises within the actual FAA standards and 
what we could do to get a clear, non-distracting visualization on the display. The FAA standards are
applied to runways 50 to 200+ feet wide, and the display has to work with a finite number of pixels.

At the end of the day, the module was commented with all sorts of information for the next person that
had to deal with it:
* Links to the appropriate FAA standards online
  * Yes, these could change over time, but at least they provide a starting point for the next developer that needs to get up to speed.
* Explanations of design choices. Examples:
  * Why I only generated a dynamic texture for half the runway width (because we can mirror-image it)
  * A brief history of why the 'obviously simpler' approach failed.
    * As we don't want history to repeat itself a couple of years later when somebody say "Oh, this can be done quicker and simpler if we do a, b, and c"  Been there, tried that, results were not acceptable.
  * Why we fall back to using a lower-resolution static image at certain zoom ranges
  * How projects consuming the library can use tunables to configure the behaviour for the parameters of their particular display.
  * How the stripe image asset was developed and importance of design choices that support a texture that has sufficient anti-aliasing not to flicker
  * Math employed to properly center the texture on our world cordinate system
  * and so on.

All this provides a lattice of information that some other developer new to the module
could easily leverage to minimize time and effort to get up to speed with the implementation provided by
the module. Lack of sufficient documentation would be called out by teammates during review - they knew
it could be them working in that module next.

### Closing: Don't consider comments as second-class citizens

Robert Martin's advice on code comments is good and true, but runs the risk of deprecating the added value
useful, informative, and well-considered comments can bring to software. Comments should carry the same weight
as the code itself - they are not second-class citizens you should feel free to skim over as you maintain your
code.  Yes, they are a maintenance burden - so use discretion and think carefully about their use.

One of the first things Robert Martin mentions in _Clean Code_ is the Boy Scout motto of "Leave the campground
better than you found it". In this context, think of good comments as that voice of experience you can 
leave for new campers to more quickly orient themselves on arriving at the campsite.

