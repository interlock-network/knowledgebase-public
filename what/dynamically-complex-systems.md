# Dynamically Complex Systems

These are the kinds of systems that we work with (in web3).
These systems exhibit a kind of complexity called
[dynamic complexity](../what/dynamic-and-combinatorial-complexity.md).

As mentioned in the linked article, these systems have few moving
parts, but a huge number of possible _states_. These states arise
out of feedback-delays. Most of the literature involves solving
problems by _reducing_ feedback delays, _where possible_. Where it
is _not possible_ (i.e. markets), one has to discover/invent alternative
feedback-vectors that can be used to reduce the number of unfavorable states
a system can enter (i.e. the federal reserve's function since the great
depression).

A guy named Schneiderman found that in industrial processes with
low-feedback-latencies, the halflife of improvement is on the order of days
or weeks, while processes with high-feedback-latencies have a half-life on
the order of years.

This is similar to programming, where the latency detection of a fault/error/bug,
and the root-causing of the bug, can result is a much higher-quality
product. (Root-causing is often the slowest part of the cycle, while writing
the fix itself is the fastest, and the detection can vary, depending on
the presence and quality of tests and telemetry).

Another bedevilling characteristic of dynamically complex systems is
that, because different parts of the state (called 'variables' in the
literature) feed back onto each other, it is impossible to hold any
of the variables constant (doing so would have ripple effects, making
any kind of empirical insight or conclusion impossible).

This is why we often use computer simulations to conduct experiments
(asking 'what-if' questions). See: [cadCAD](../cadcad.md).

# Causal Factors

There are 10 (at least) causal factors that cause a system to have
dynamical complexity:

Firstly, systems are dynamic, meaning they experience sudden phase-shifts and reversals.
Secondly, systems are tightly coupled, with one small change rippling through entire system.
Thirdly, the tight coupling causes systems to feed back onto themselves.
Fourthly, they are non-linear, meaning that effect is not proportional to cause.
Fifthly, they are history-dependent, meaning taken-actions cannot be untaken -- at least not at the same energy-cost.
Sixthly, they are self-organizing, wherein small purterbations cause patterns that are formed and sustained by feedback loops.
Seventhly, they are adaptive, in that their agents learn from patterns and change their behavior to leverage those patterns, thus causing the patterns to change.
Eightly, they are counter-intuitive, because causes and effects are distant from each other in space and time.
Ninethly, they are policy-resistant, in that seemingly obvious solutions to a problem are ineffective or counter-effective.
Tenthly, they involve trade-offs, wherein one must accept negative outcomes now, to get positive outcomes in the future, and vice-versa.


As you can imagine, using simulation is the only feasible way to understand, and _engineer_,
systems with these kinds of properties. The framework, cadCAD, is the preferred tool
for doing this in a web3 context (though it is useful in almost any context that involves
a dyanmically complex system.

The use of this software is not a one-and-done, kind of thing. The design of a simulation
is best done by _everyone_ (individually) that seeks to understand the system-under-design.
Discrepencies between the simulation-models reveal unspoken assumptions held by each
designer. Even with _one_ solitary designer, the process of understanding is fundamentally
dialectical and reflective. The model is _grown_, and as understanding improves, it is changed,
and grown further, until the designers feel that the model is comprehensive enough
for implementation and _testing_ in the real world. If there are chronic discrepancies
between the real world and the model, the model must be changed.

See: [The Market for Lemons](../what/the-market-for-lemons.md), for an example of
a trivial system that had pathological negative outcomes that could _only_ be
remedied by simple policy-changes (i.e. regulations).