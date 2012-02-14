---
layout: post
title: Bootstrapping a lightweight Object System in Ruby
tags: ['ruby', 'functional programming', 'oop', 'plt']
---
{% include JB/setup %}

OO for Blasphemers
------------------

There seems to be a quite a bit of talk these days about programming in an
Object Oriented vs a Functional style, and while that divide is real
(especially as specific implementations go), one must be aware of the
similarities between the two in order to properly evaluate each of its own
merits.
While it's easy to dismiss some of the loftier ideals of the
Functional paradigm as heady and academic, one must not forget that
ideas such as:

* Garbage Collection
* Type Inference
* Higher Order Functions (functions that consume and/or return other functions,
  Enummerable methods are a great example)
* List Comprehensions
* Aspect Oriented Programming (think Rails before/after methods)
* and much more were once rooted in Functional Academia, which turned out to be quite
useful, in practice.

However, enough of that. Let's delve into an exercise which hopes to illuminate
just how similar the two can be.

Given a basic Person class, as one would typically write it in Ruby, you'd
likely end up with something akin to this:

{% highlight ruby %}

        class Person
          def initialize(name, age)
            @name = name
            @age = age
          end

          def set_name(new_name)
            @name = new_name
          end

          def get_name
            @name
          end

          def get_age
            @age
          end
        end

{% endhighlight %}

(Pardon the explicit getters and setters, but for illustrative purposes please play along)

What we have here will allow us to create objects, which are classically defined as:

        "An object has state, behavior, and identity; the structure and
        behavior of similar objects are defined in their common class; the
        terms instance and object are interchangeable".

This enlightens us to some less obvious facts about Objects:

1.) My language doesn't necessarily need to provide them
2.) An object essentially wraps up method dispatch and state

And perhaps you're familiar with Closures, which are essentially stateful
Function Objects (think Procs & Blocks in Ruby) which have access to their
lexical environment. In other words, they "close over" free variables.

Aha!

From here, one could have the thought that Objects, in their most basic form,
are essentially hashes of stateful functions!

This hit me hard when I first came to understand it, perhaps we and our
Functional bretheren aren't so different after all?

So, that's fine and great and good theoretically, but how might this actually
look. In (working!) Ruby code, no less.

{% highlight ruby %}

        Person = ->(name=nil, age=nil) do
          methods = {
              get_name: -> { name },
              set_name: ->(new_name) { name = new_name },
              get_age: -> { age }
          }

          ->(meth, *args) { methods[meth].call(*args) }
        end

        Person.call("Robert", 24)
         => #<Proc:0x0000010109b008@(irb):98 (lambda)>

{% endhighlight %}

So what just happened here? Our Person function/constructor has returned a function which represents an instance of Person.

For familiarities sake, a little syntactic sugar:

{% highlight ruby %}

        def Person.new(name, age)
          call(name, age)
        end

        robert = Person.new("Robert", 24)
         => #<Proc:0x0000010109b008@(irb):98 (lambda)>

        robert.call(:get_name)
         => "Robert"

        robert.call(:set_name, "Robert Pitts")
         => "Robert Pitts"

        robert.call(:get_name)
         => "Robert Pitts"

{% endhighlight %}

Oh, and as of earlier this, week, that age isn't quite correct anymore, so let's add a `had_birthday` function to our methods hash.

{% highlight ruby %}

        methods = {
              get_name: -> { name },
              set_name: ->(new_name) { name = new_name },
              get_age: -> { age },
              had_birthday: -> { age += 1 }
        }

        robert.call(:had_birthday)
         => 25

        robert.call(:get_age)
         => 25

{% endhighlight %}

As you can see, our state is being preserved correctly, much like a standard Ruby Object would behave.

There are some downfalls...

{% highlight ruby %}

        robert.call(:gracefully_handle_errors)
         => NoMethodError: undefined method `call' for nil:NilClass

{% endhighlight %}

So perhaps we should have at least some primitive error handling as well.

{% highlight ruby %}

        no_method_error = ->(meth) do
          raise NoMethodError, "undefined method `#{meth}' for person"
        end

        ->(meth, *args) do
          if methods[meth]
            methods[meth].call(*args)
          else
            no_method_error.call(meth)
          end
        end

        robert.call(:gracefully_handle_errors)
         => NoMethodError: undefined method `gracefully_handle_errors' for person

{% endhighlight %}

One could always expand upon things from here, doing things such as using
`#method_missing` for more familiar invocation, etc.

Not bad!

While we still don't have inheritance, or a more formal separation of Classes
vs Instances, I'm sure you're beginning to see that in matters of Objects vs
Functions vs Data, there may be more in common than otherwise. Also, had you
not already realized, Ruby owes quite a bit more to Functional Programming than
is immediately obvious, and all this without delving very far into the
similarities at all.

Cheers!

Full Example Code:

{% highlight ruby %}

    Person = ->(name=nil, age=nil) do
      methods = {
          get_name: -> { name },
          set_name: ->(new_name) { name = new_name },
          get_age: -> { age },
          had_birthday: -> { age += 1 }
      }

      no_method_error = ->(meth) do
        raise NoMethodError, "undefined method `#{meth}' for person"
      end

      ->(meth, *args) do
        if methods[meth]
          methods[meth].call(*args)
        else
          no_method_error.call(meth)
        end
      end
    end

    def Person.new(name, age)
      call(name, age)
    end

{% endhighlight %}
