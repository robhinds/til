# Automatic Tail-Recursion Optimization in Scala

When writing recursive methods in Scala, even without using the `@tailrec` annotation (in fact, even if the method isnt 100% tail-recursive) the Scala compiler will attempt to optimize the code as tail-recursive.

However, the compiler can only optimize this if the recursive method is not polymorphic (e.g. `private` / `final`, nested inside another calling function or an `object` method rather than a `class` method). This can be seen if you add a `@tailrec` annotation to a non-private/final `class` method, the compiler will complain.

This is worth knowing, because I had a recurisve method on an `object` that was being optimised (and that optimisation was preventing stackoverflow errors), and I changed the `object` to a `class` (with companion object) and my unit tests started failing due to the stackoverflow error - It caught me out for a few minutes to work out why it had stopped working.
