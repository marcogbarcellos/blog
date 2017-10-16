---
title: How Elixir and Erlang handle recursion
subtitle: Why using recursion in elixir/erlang is not as bad as it is in most OO languages(in most cases)?
date: 2017-10-15
tags: ["elixir", "erlang", "beam", "recursion", "functional programming", "erlang vm", "memory management", "performance", "scalability"]
---

Many developers when solving specific problems prefer to stick with a recursive approach, and the reason might be because in some cases it helps get a better time complexity(Big O) thus improving the service performance. It also may involves personal preferences, i.e some might think it's a cleaner aproach, more readable, more elegant and so on.

For most languages, this approach can demand a lot of memory to be executed as everytime you call a function in a recursive manner, this call goes to the memory stack to be executed later. Thus, depending on the amount of pushes to the stack, it may be heavier than choosing a non-recursive approach to execute it, even though its time complexity can be superior.

## Erlang and Elixir Approach


In Elixir and Erlang, we have what's called `tail-call optimization`. A tail call function is a function which call another functions as its last thing. And this optimization works in a way that's similar to a `goto` or a `jump` and you don't need to allocate extra memory when pushing more functions to the stack.

The following snippet gives an example of what is a tail call function:

```

def first_func(...) do
  ...
  another_func(...)
end

```

But how does it actually works ?!?!

In the snippet above, the final result of the `first_func` is the result of `another_func`. This is why the compiler can safely perform the operation by jumping to the beginning of another_fun without doing additional memory allocation. When another_func finishes, you return to whatever place original_func was called from.

## Endless loops won't cause Stack Overflow

Take the following function :

```

def endless_loop(...) do
  ...
  endless_loop(...)
end

```

This `endless loop` takes advantage of the `tail-optimization` as it can run without consume any additional memory .

This solution fits well for arbitrarily large iterations. There is a downside, though. Whereas classical (non-tail) recursion has a more declarative feel to it, tail recursion usually looks more procedural.