## Substitution

e.g.1 

```ocaml
let x =5 in ((let x = 6 in x) + x)
->
((let x = 6 in x) + x){5/x}
=(let x = 6 in x) + 5
->
(x{6/x}) + 5
=6 + 5
```

e.g. 2

```ocaml
let x = 1 in (let x = x + x in x + x)
->
(let x = x + x in x + x){1/x}
=(let x = 1 + 1 in x + x)
->
(x + x){2/x}
=2 + 2
```

## Defining substitution: let

```ocaml
(let y = e1 in e2){v/x}
->
let y = (e1{v/x}) in (e2{v/x})

(let x = e1 in e2){v/x}
->
let x = (e1{v/x}) in e2
(* the x in e2 was shadowed by the x(different with the former) after the let *)
```