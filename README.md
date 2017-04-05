# GRAMMAR ISSUES

`a:b` is a parse error, but should instead mean something similar to `function(...) return a.b(a, ...) end`

`5:square()` is a parse error, but should instead mean `(5):square()`

`"dog"[2]` is a parse error, but should instead mean `("dog")[2]`

closed over `...` cannot be used (this may be an issue with the runtime rather than the grammar, and is not a big deal)

# TABLES

`#t` is log time for tables (should be constant time) and not defined to be a particular number for numerical tables with gaps (wtf????).

You can capture varargs or multiple returns using `{...}` or `{f()}`, but that won't let you differentiate between explicit nils and the absence of a value. You need to use `select("#", ...)` and `some_other_function_that_collects_this_information(f())` respectively to get the right thing to happen.

Thinks like json serializers have to do extra work to guess whether tables are numeric or not.

Mike Pall says: [Corollary: one should definitely separate the concepts of a map and an array if one were to design a new computer language.]

With all this in mind, maybe there should be separate concepts of maps and arrays???????

# MEMORY LIMIT

Hey the luajit memory limit sucks. If I want to write inefficient code that will abuse the GC I should be able to do that, thanks.

# indexing and intervals

According to [this dude](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html) we should use half-open intervals like [a, b) starting at 0 in programming languages. Lua uses closed intervals like [a,b] starting at 1.
