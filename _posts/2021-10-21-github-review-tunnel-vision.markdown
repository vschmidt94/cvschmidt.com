---
layout: post
title:  "Github code review tunnel-vision"
date:   2021-10-21 8:00:00 -0800
categories: Github, Software, Quality
---

# The problem with github's code reviews

Today's soapbox: Github's code review tool creates tunnel vision

I see this happening a lot: a PR on github is reviewed only within the extent of the changes.
That is to say, "Yep, the code you wrote LGTM" without considering the context of the larger
code base.

Today's example was the addition of new logic with a corresponding (new) boolean flag parameter
to control basic logic within the function. All that's fine and good - but once I opened the
file up in an actual editor and started tracing calls upstream and downstream, we quickly identify
the new boolean flag is superflous, and what's more - we've got another parameter that now mirrors
an existing object attribute - so why are we still passing it around?

Also, we can't comment on lines outside the diff itself - so drawing attention to something else,
or questioning an existing (but un-changed) block of code isn't the easiest to do. We end up with
comments like 
> Not your change, but L187-190 above should be changed to reflect new object attribute.

But the bigger problem - and original gripe - is the tunnel-vision.  We're rushing these patches 
through review without spending time looking at them with a more holistic approach and when we
finish our review with `+1 LGTM`, we really haven't considered the code change in the bigger
picture - are we duplicating functionality? Is this optimal fix, or are we just doing what is
most convenient here because to do it correctly, we really need to refactor this module and nobody's 
got time for that? etc.

For me, I'm going to make a point to pull down more code reviews locally and spend the time it takes
to check better upstream and downstream - especially when the entirety of the change isn't within
a single function.

