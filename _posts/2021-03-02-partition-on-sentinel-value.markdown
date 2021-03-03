---
layout: post
title:  "Partitioning data with sentinel value using Pandas"
date:   2021-3-2 8:00:00 -0800
categories: Python Pandas Analytics
---

# The problem

I have a collection of sensor readings / telemetry that I want to partition into subsets based on the detection
of a sentinel value. For this case, imagine a collection of power readings for a motor running a conveyor
belt in a factory. When a batch is being produced, the conveyor belt runs continuously. The belt motor
is powered off during process change-overs.

The motor drive is polled once per minute and instantaneous power draw is saved to database along with
other metrics from elsewhere in the process.

# The solution

It is easier to show than explain...

<script src="https://gist.github.com/vschmidt94/91518e3c40e0f1284401297049439376.js"></script>


