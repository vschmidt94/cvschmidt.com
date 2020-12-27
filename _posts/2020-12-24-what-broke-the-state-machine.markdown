---
layout: post
title:  "Fixing a broken state machine"
date:   2020-12-24 14:27:14 -0800
categories: software statemachine
---
## What is a state machine?

From some software engineering class somewhere, everyone's run into the 
[finite state machine](https://en.wikipedia.org/wiki/Finite-state_machine) model. In a state machine,
behavior is controlled by transitioning through a series of states. Upon some logic condition,
the model moves through defined transitions between states.

![simple state machine](/cvschmidt_blog/assets/img/state_machine/state_machine.png){:width="200" height="auto"}

The software model of a state machine provides a very flexible framework for automation. For example, the movement of
objects between phases in their lifecycle.

## What happens if you break the rules?

The fundamental rules of a state machine are:
1. There are finite set of states.
2. There are defined transitions between states.

A recent project I was working on decided to bend (err, break) these rules a little by introducing a new state that
could be entered via user influence. In other words, upon certain interactions with UI, the object would immediately
*teleport* into this new state. The intent was good, in that the desire was to implement "Hey, the user has mucked with
the object and we don't really know how the object should now be handled. Let's put in this new 'updated' state and then
when the state machine logic kicks in, it can decide the outcome based on the whatever object mutation now exists."

So, we essentially had this:

![broken state machine](/cvschmidt_blog/assets/img/state_machine/broken_state_machine.png){:width="400" height="auto"}

Yep, it's pretty obvious once you diagram it out - especially when you consider two different processes potentially
could update the object's state. Given the state machine processing looped through several hundred individual objects
each loop, and user updates in the GUI were relatively rare events - _most_ of the time, everything just worked.

But we definitely had sporadic instances where the user's update to the object did not appear to be correctly handled.
This was ultimately due to the race condition found in the original code: The handler process was in the middle of a
transition at the same time a user update landed. If the user update landed first, it was over-written by the handler
process - and vice-versa.

## The fix

In this case, the ideal fix would have been to change the 'updated' state from a state to something like a flag, and
have the state handler process be aware of the update flag, and include the flag condition in the processing.

In my particular case, the object record in the database could not be altered (because... reasons). What I did end up
doing was (1) remove the updated state (the 'U' state), and (2) move the logic for deciding the appropriate original
state the object update should produce to the API process.  Finally, I introduced a lock on the object when it was being
handled by the User API process.
