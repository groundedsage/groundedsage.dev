---
title: The Clojure Mindshare.
description: Why I chose Clojure as the mother tongue in the realms of software.
date: 2018-05-01
tags:
  - Clojure
  - Programming
---
When I get asked why Clojure can be very difficult to summarize. We are in an industry that is so new, so fast-moving and so financially rewarding that people tend to gravitate towards popular programming languages. These people are quick to migrate to a new technology, they often skip fundamentals or simply have no interest in gaining fundamental knowledge. 

As a result, there is always a "battle" for mindshare with new languages, libraries, frameworks, and tools. 

- - -

## Definitions

In typical Clojurian fashion, I would like to pause for a minute to review some definitions.

**Mindshare:**

"consumer awareness of a product or brand, typically as opposed to market share"

**Mind:**

"a person's ability to think and reason; the intellect"

**Share:**

"have a portion of (something) with another or others"

*As we can see the definition of **mindshare** has been forged by people in marketing. But when we break that word into its components and inspect them we can derive a radically different meaning.*

- - -

## How I found Clojure

I came into programming with a bit of a different mindset from others. The motivation was a common one: I want to build an app. But I wanted to do more than build it, I wanted to craft it. I wanted to find a general purpose programming language that was powerful enough and flexible enough for me to create anything I could think of now and in the future.
On this journey, I became an active Twitter user because I found this is where a lot of programmers spend their time. As I followed people who had very thoughtful and intelligent discussions in the field of programming I started to notice a large majority of them either used or advocated the Clojure programming language.
At the same time, I invested a lot of time reading the wisdom of others on how to pick a programming language. I did this instead of picking a popular language and diving straight into learning how to code. From this I found two pieces of advice on the web that defined the path I have taken to this day.
1. Forget about arguments around popularity, syntax, and semantics. Look at the philosophy behind the language
2. Lisp is the most expressive and flexible language. You can reach a flow-state where ideas can freely flow from your mind into code

#### The Philosophy

To learn about the Clojure philosophy I read this article by Michael Fogus: <https://www.drdobbs.com/architecture-and-design/the-clojure-philosophy/240150710>
TL'DR

* **Simplicity** - by using pure functions
* **Empowerment** - by being Practical
* **Freedom to Focus** - by being expressive

These 3 goals coming together to create the central goals of Clarity and Consistency.
The diagram below is extracted from that article and illustrates this more clearly and in more detail.
{% image "./clo1.gif", "Diagram of the main Clojure goals" %}

#### Expressiveness and Flexibility

Lisp languages have a long and deep history in programming (the first Lisp was originally specified in 1958). It is the second-oldest high-level programming language, Fortran is older by one year.
The Lisp programming language Racket is used to teach programming fundamentals in modern Computer Science courses. <https://www.edx.org/micromasters/software-development>

The language Racket <https://racket-lang.org/> is also used in both academic research, such as Programming Language Theory (PLT) and industry, for deeply complex problems such as tooling for the formal verification and synthesis of other programming languages. (Skip to 42:00 for the example applications in Industry) <https://www.youtube.com/watch?v=KpDyuMIb_E0>

The editor Emacs is one of the oldest editors and is still very popular among programmers. It is primarily written in Emacs Lisp.

Common Lisp is very old and less common these days (Pun intended). People used to learn Common Lisp because it already had features their day to day language was planning to have, "some day in the future". It has taken years for other programming languages to catch up. Still, Common Lisp has features missing from other languages, they will likely never be able to have those specific features. There is also a rather famous story of debugging and fixing a satellite in space (production), doing this all remotely from the ground using the REPL. [https://www.youtube.com/watch?v=_gZK0tW8EhQ&feature=youtu.be&t=2520](https://www.youtube.com/watch?v=_gZK0tW8EhQ&feature=youtu.be&t=2520)


Lisp also has a history of being a secret weapon at technology start-ups. As illustrated in this article by Paul Graham - Beating the Averages. <http://www.paulgraham.com/avg.html> 

*My initial idea of finding one programming language that I can use everywhere turned out to be a naive beginner thought. Polyglot programming is inevitable. It is impossible and foolish to try and solve every problem with one programming language. Lisp is a language that embraces this at it's core. It is a language for creating other languages. The best language to use will always be a language designed specifically for that domain.*

**As an Aside:** We live in a world today where the problems we face today are beyond simple, what seems simple on the surface often explodes into complexity. These problems require multidisciplinary thinking and at best we can construct a model that partially satisfies the requirements of our problem (with a bit of squinting). Even after the solution has been verified, deployed and demonstrated to work it is naive thinking to assume that this solution will (with 100% certainty) continue to work in the future. Perhaps the solution unlocked deeper parts of the problem and needs to evolve, or the problem was misunderstood, or the problem no longer exists, or how we verified our solution was wrong. Throughout history we have come up with models that work and used them successfully for centuries without any formal explanation of how it works. Using programming languages that require Types or some kind of formal proof when exploring a new problem domain is counter productive and can halt progress all together. If you watch this short snippet from William Byrd, (from 4:00 to 5:20) [https://www.youtube.com/watch?v=OyfBQmvr2Hc](https://youtu.be/OyfBQmvr2Hc?t=240), you can see how just a few lines of code have existed for decades without being able to be formally verified with a proof, even by the top people in their field. This is very telling. We need languages that mould easily in our hands, languages that trust us to say "this works" instead of blowing up in our faces.

Clojure itself was designed as a hosted language. Because of this, it loses some of the raw flexibility Lisp offers in exchange for being practically useful in industry. The two core targets of Clojure is the Java Virtual Machine (JVM) and JS to run anywhere Javascript runs. There is also a very up to date version that runs on Common Language Runtime (CLR) maintained mostly by people wanting to build games on Unity [https://arcadia-unity.github.io/](https://arcadia-unity.github.io/).

In addition to that, there are various implementations and experiments that use a subset of Clojure or draw inspiration from Clojure. Such as Clojerl [http://clojerl.org/](http://clojerl.org/) for the Erlang VM (BEAM), Ferret for writing C++11 [https://ferret-lang.org/](https://ferret-lang.org/), and Carp, a statically typed lisp [https://github.com/carp-lang/Carp](https://github.com/carp-lang/Carp). The cool thing is that files can be written with the `.cljc` extension and run on multiple different run-times. Library authors take advantage of this so you often get libraries that work across run-times.

- - -

## Why I stick with Clojure

Once I found Clojure there are a few extra things that made me stay (or keep coming back after exploring other languages). 

* Stability
* Small and focused community
* High signal vs noise
* Clojure databases

### Stability

I want to build software that keeps working without requiring maintenance. In most other languages and tools things break when you upgrade the language or a library. Upgrading is essential to take advantage of new features which include performance and security. For those that live this life it's difficult to see how bad this is. You can spend days, weeks or months fixing something broken that worked before, instead of adding new features. Sometimes you even have to adopt a library, maintaining a fork of it for up to a lifetime because the maintainer is slow to update it or has left the field entirely. I've simply become "Allergic to the Churn", as described perfectly in this article <https://lambdaisland.com/blog/2019-08-07-advice-to-younger-self>

The stability of Clojure is rock solid. It might as well be bedrock.
{% image "./cljs-survival-graph.jpeg", "Clojurescript Survival Graph" %}
{% image "./clojure.jpeg", "Clojure survival graph" %}
These graphs were created based on this article which has a few examples of other repositories. <https://erikbern.com/2016/12/05/the-half-life-of-code.html> I've seen a number of these graphs and nothing compares to how solid Clojure is. As you move up from the language into the library and tooling ecosystem these benefits amplify. In addition to the amplified effect of moving up the stack. The community does it's best to embody this philosophy and process of maintaining stability.

### Small and Focused Community

The Clojure community is small. In fact, is mostly consists of senior programmers. [https://insights.stackoverflow.com/survey/2019#developer-profile-_-years-coding-professionally](https://insights.stackoverflow.com/survey/2019#developer-profile-_-years-coding-professionally)
Because of how small it is you can frequently get questions answered directly by the creators of a library or the people that work directly on the compiler. These people also take time to really think through problems, often reading and implementing fantastic research from old forgotten papers in computer science.

### Signal vs Noise

There are fewer libraries to choose from. This is often seen as a negative, but it's a feature. Other programming ecosystems need huge frameworks or zero-config set-ups. Simply because the amount of decisions developers have can paralyze them from actually getting anything done. As mentioned before with how focused the community is. These libraries are also generally very high quality with features or concepts that take years to reach programming communities outside Clojure. Sometimes it lags behind, but there is a saying that resonates with how I have seen the Clojure ecosystem grow.

*Slow is smooth. Smooth is Fast.*

If you really need that library that exists outside of Clojure. You most likely can still use it. Clojure was designed as a hosted language that embraces the platform. Simple interop is a key feature of the Clojure language.

### Clojure Databases

It may come as a surprise to those outside the Clojure community but Clojure has some interesting database options. In fact, Rich Hickey thought about Clojure and what became Datomic simultaneously, he first had to create the language to create the database. This database was a major reason why I was also interested in Clojure. Datomic <https://www.datomic.com/> was and still seems like a database from the future. We also now have Datahike <https://github.com/replikativ/datahike> and Crux <https://opencrux.com/>. All with their unique benefits and trade-offs. All from the future.

- - -

## Summary

There are so many brilliant minds in the Clojure community. Tapping into what these **minds share** and the rich history of Lisp seems like a wise decision.