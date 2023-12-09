 

## Equational Reasoning

```ocaml
let twice f x = f (f x)
let compose f g x = f (g x)

twice h x = h(h x)
compose h h x = h(h x)
```

