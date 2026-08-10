# Flow Is Built for Testability

One of the defining principles of Flow is testability.

Flow deliberately forces code into a methodical structure. Every function lives in its own file, with a clear name and a consistent prefix. That discipline may initially feel restrictive, but it serves a very important purpose: it makes regression testing, dependency analysis and data-flow tracing dramatically easier.

When each function has a clear identity and location, it becomes possible to see precisely how the system is assembled, what changed and what might break as a result.

## Every Interface Is a Pipeline

An interface is fundamentally a pipeline.

Data enters from one or more sources. It passes through validation, transformation and decision-making. Then data leaves through one or more outputs.

To understand the system, you need visibility across that entire pipeline:

* What came in?
* Which functions processed it?
* What decisions were made?
* What came out?
* How long did each stage take?

Timing is especially important. From a Theory of Constraints perspective, you cannot identify the true bottleneck unless you can see where time is being spent.

Flow’s tracing system is designed around that reality.

## Why I Kept Going Back to C++

Whenever I tried to do serious work in Iguana 6 or Iguana X, I often became frustrated and returned to C++.

The problem was not that C++ was inherently easier or more pleasant. It was that the tracing system we had built in C++ was more useful.

It was less visually sophisticated than the Iguana Translator, but it allowed me to focus on exactly what mattered. I could insert tracing where I wanted it, observe the relevant inputs and outputs and follow the important parts of the pipeline without spending time manipulating a graphical interface to produce the perfect view.

That directness made the system easier to understand.

You need to see what is actually moving through the pipeline. You need to see how it changes. You need to see how quickly it moves. Only then can you identify the real sources of complexity and the true bottlenecks.

## Everything Should Be Visible

Flow is designed to make the entire system visible.

Customers should be able to see not only their own configuration and business logic, but also the underlying C++ code through which their data moves.

That transparency is deliberate.

Healthcare integration software has become critical infrastructure. It is no longer acceptable for such infrastructure to remain entirely dependent upon one company, one development team or one individual.

Customers need to understand the methodology by which the software is developed. They need access to the tools, source code and conventions required to maintain it. The system should rely upon open formats and open technologies wherever possible.

## Software That Can Outlive Its Creators

At some point, every company changes. Every development team eventually moves on. Every individual becomes unavailable.

Critical infrastructure must be designed with that uncomfortable reality in mind.

Our responsibility is to ensure that, when we are no longer able to continue the work ourselves, the software can be understood, maintained and handed over without the infrastructure collapsing around it.

That means clear code. Clear conventions. Repeatable tests. Transparent tracing. Open systems. And a development methodology that can be learned and continued by others.

We understand the responsibility that comes with building infrastructure upon which healthcare organizations depend.

We take that responsibility very seriously.

