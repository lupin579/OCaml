## Functions

Since functions are values:


```ocaml
<env, fun x -> e> ==> fun x -> e
```
This is tempting, simple, and **wrong**


**the essence of the semantics in ocaml(the lexical semantics) is**
**the evaluation of the function:**
```ocaml
<{x:0},fun y -> x + y> ==> (|fun y -> x + y, {x:0}|)
```
when compiler encounter a function, it will not do any substitution,
it will just create a closure(seal the current environment, and the whole the funciton),
when we do the function application on this function, e.g. f x
it will evaluate the **expression f** then the **arguement x** based on the current environment at first,
then unseal the closure, evaluate the function based on the **"current" environment at that time**.
