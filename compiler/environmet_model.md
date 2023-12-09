## Environment Model for simPL

- Easy way to think about computation
  - except capture avoidance!
- Not a realistic model of machines
  - Code and data kept separate
  - Code note "edited" during computation
  - Data is kept in memory...

```ocaml
let x = 42 in
(* x | 42 *)
let y = 3110 in
(* x | 42
   y | 3110*)
x + y
```
(* x | 42
   y | 3110*)
### Dynamic environment
- Maps variable names to **values** in current scope
- Implements a kind of ***lazy substitution***
ps: as opposed to static environment(which maps variable names to **types**)


