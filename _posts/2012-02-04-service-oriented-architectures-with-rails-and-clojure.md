---
layout: post
category : functional
tags : [clojure, SOA, ruby, functional-programming]
---
{% include JB/setup %}

Service Oriented Architectures with Rails and Clojure
=====================================================

Why functional languages (a primer)
-----------------------------------

* Simple to reason about
 - inputs yield outputs
 - data and behavior are the same

* Simple to decompose
 - functions are truly first class
 - when everything is composed of functions/data powerful patterns of abstraction become available
 - currying

* Simple to compose
  - partial application | a function without all it's arguments simply returns a function expecting those additional args
  - (implicit in ML style languages, explicit in lisps/clojure)

* Composition leads to reuse
  - Almost anything you can imagine writing that's a general operation, you will almost certainly see that it was available to you before hand.
  - Learn to recognize patterns and be tickled by them, intuit that someone smarter than you has probably solved this.

* Programming, motherfucker
 - it matters
 - ...the more you know!
 - exposure and experimentation build & refine tastes
 - Do you have an argument for not knowing more? Is putting the shoe on the other foot a bad idea sometimes?

Why Clojure
-----------

* Lightweight Syntax
 - very little to learn, data and behavior share representation
 - omg parens. Whatever, like everything about programming you currently understand made sense to you immediately.
  - I can't read arabic, so it's fucking worthless?

* Pragmatic
 - Nearing two years old, it's not just going to go away
 - first class citizen of the JVM. There is a Java library for your problem, and it's probably a lot more refined than you realize.
  - ie: ruby has can reach out to C, but there's almost no reason you would unless you _really_ had to. It's hard.
 - performant... without the expense of obfuscation. Write code as succinct (if not more so), than your current code, and watch it fly
 - people are using it on real projects to solve real problems
  - Relevance
  - 8th light
  - Edgecase
  - Atomic Object
  - ... and plenty of startups
  - ... and plenty of enterprise companies

* Hype
 - founded hype, at that. Solves real problems, unlike things such as Node.js (if evented concurrency was a good idea, tornado or eventmachine would be successful)
 - a real chance to innovate and be thought leaders
  - making a grand impact on the Ruby and Rails community is really hard right now.
   - ... but maybe if we listened to other communities more we could see what we're lacking
    - it's a two-way street

* Fun
 - A lot of what attracted me to the Ruby community when I came into is present in the Clojure community
   - Want to work with passionate and intelligent people?
     - Attract talent! Recruiting is _HARD_, especially right now
     - it's just compounded with super smart JVM/Java guys
     - and super smart Lisp guys
     - and super smart CS guys
   - and you don't need to rewrite every tool ever. The ecosystem is already there.
   - when you do need to rewrite a tool, guess what, you're a hero. Well done.
 - palpable excitement from the community. Haven't felt that in a while here :(

* Simplicity vs Ease
 - Ruby is easy... sort of
 - Clojure is hard(er)... sort of
 - Ruby makes it really easy to get a reasonably tiny system up and running quickly, and achieve sorcery in the process
 - Clojure (and FP in general) make it really easy to get reasonably large systems up and maintainable, and achieve wizardry
 - A LOT of our apps go longer than 3-4 months. Perhaps we should think about things longer term.


OOP vs FP
---------
This is a silly digression, we can talk about it later.

Making it Real
--------------
* Service Layer behind a Rails app
  - we should probably be designing a lot more of our applications this way anyway

* Full Stack
  - the framework support isn't quite there yet for getting up and running quickly
  - ...but most of our projects last longer than a month anyway
  - and if it truly is tiny enough that it would be a month long project... then the tooling is there

* During the times we're not using Clojure, we will be better Ruby devs for having done so
  - Learning.
  - Learning.
  - Learning.
  - ... Ruby supports (and took!) a lot of abstractions from Functional languages and Lisps

So why not?
-----------
* Learning new things is hard
  * You need to learn FP and Lisp in one swoop
    - I had a hard time reasoning about CLJ in my independent studies without spending time with Haskell first
  * There's a good chance OOP has broken your brain.
    - It's not always easy to reason about problems in new ways
    - We are the next wave of BASIC programmers
      - ... that was a Dijkstra joke
      - "It is practically impossible to teach good programming to students that have had a prior exposure to BASIC: as potential programmers they are mentally mutilated beyond hope of regeneration."

  * As a Rubyist that learning curve _is_ lower
    - You understand type dynamism
    - You understand metaprogramming
    - You understand higher order functions
      - Enummerable
      - Blocks, Procs, Lambdas, Object#method
    - You probably care about programming if you're here

* Tooling
  - Especially around Vim, it's not quite there yet.
    - ...but if you know how to use Vim outside of a Rails app anyway, you'll be fine
  - Pure Clojure Libraries
    - A lot of them are missing
    - Sometimes interacting with a Java library can be clunky
      - If it becomes enough of a problem, write a wrapper around it. The Facilities for doing so are awesome.

* Vulnerability
  - You don't know everything
    - You need to admit and be in tune with this if you want to grow
  - Making mistakes... probably more than you're used to
    - ... but that's okay
    - I'm pretty sure you weren't as bad ass as you are now when you first started with
      * Ruby or...
      * Objected Oriented Programming or...
      * Abstractions or...
      * Programming

Concrete, damn you!
-------------------

* I don't know (every|any)thing either.
* This becomes more apparent to me _every_ _day_

* Let's look at some code
  - https://github.com/rbxbx/clojure-as-a-service-example
