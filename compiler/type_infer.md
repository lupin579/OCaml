## Intuition for Unification

```
5x + 2y =  9
 x -  y = -1
```

how do we solve equations?
- Eliminate a variable
- Find value of other variable
- Use that to find value of original fisrt variable
- Solution is a **substitution** that **unifies** set of equations

### Substitutions as solutions
- A substitution may be a **sequence** **S1; S2; ...; Sn** of smaller indididual substitutions, carried out in order
- A substitution **S** unifies a constraint **t1 = t2** if **t1 S = t2 S**
- A substitution **S** unifies a set **C** of constraints if it unifies all the constraints in the set

```
'x ->('x -> int) = int -> 'y
'x -> 'x = 'y

{'x -> 'x / 'y}

'x ->('x -> int) = int -> 'y
'x ->('x -> int) = int -> ('x -> 'x)

{int / 'x}
int ->(int -> int) = int -> (int -> int) 

int = int
int = int

{'x -> 'x / 'y}; {int / 'x}(the substitution)
```

```
(1)'x ->('x -> int) = int -> 'y
(2)'x -> 'x = 'y

from (1), we can extract that: 
'x = int
'x -> int = int -> 'y

then based on the extraction(aim at unifying the extraction), we create the substitution:
{int / 'x}

we apply this substitution on (2), we can get:
int -> int = 'y

based on the equation we get(aim at unifying the equation), we can create a new substitution:
{int -> int / 'y}

then we put these two substitutions on (1) and (2), we find we can unify them
so {int / 'x}; {int -> int / 'y} is a substitution for this constraint
```

## Let Inference

e ::= |let x = e1 in e2

```
env |- let x = e1 in e2 : t2 |- C1, C2
  if env |- e1 : t1 |- C1
  and env, x : t1 |- e2 : t2 |- C2
```

e.g.
{} |- let x = 42 in x : int -| {}
  {} |- 42 : int -| {}
  {x:int} |- x : int -| {} 

### Polymorphsim is tricky

```ocaml
let id = fun x -> x in
let a = id 0 in
id true
```
We want **id: 'a -> 'a**
not int -> int or bool -> bool(these two are too specific)

### Types schemes
- Insprired by **universal quantification** in logic
  - for all x, it holds that 0 * x = 0
- A type scheme is written 'a.t(formally, forall a . t)
  - 'a is a type variable that is in scope in t
  - t is a type
e.g.
```ocaml
List.length
(* - : 'a list -> int = <fun> *)
let myLen : 'a . 'a list -> int = List.length
(* val myLen : 'a list -> int = <fun> *)
(* the universal quantification was omitted by utop, it will not explicitly show this,
   because programmer doesn't need to konw that *)
```

## Let Polymorphsim

### Generialization and instantiation
let id = fun x -> x in ...
- **Generialize** type to **'a . 'a -> 'a** in environment
- At each application, **instantiate** type with new type variables
  - At **id 0**, instantiate to 'b -> 'b
  - At **id true**, instantiate to 'c -> 'c
  - Now each use is independent of the others

```ocaml
env |- let x = e1 in e2 : t2 -| C1, C2
  if env |- e1 : t1 -| C1
  and generialize(C1, env, x : t1)
        |- e2 : t2 -| C2

env |- n : instantiate(env(n)) -| {}
```
### Generialization
**generialize(C1, env, x : t1)**
- Fully finish inference of binding expression:
  - Use **unify** to solve **C1**
  - Apply resulting substitution to **env** and **t1(type)**, yielding **env1** and **u1(type)**
- Generialize **u1(type)** to a type scheme **s1(type)**
  - Do generialize variables in **u1(type)**
  - Do not generialize variables also in env1(cuz they are constrained by outside code)
- Return **env1, x : s1**

**This is what makes polymorphism type inference work**

### instantiation
- Doesn't change a type 
- Changes a type scheme to a type
  - Get rid of the **'a ... 'an** before the dot
  - substitute a fresh type variable for each of them
- E.g., **'a . 'a -> 'a**
  becomes **'b -> 'b** for a fresh **'b**

## Mutability and polymorphism
*Mutability always makes our lives worse*
What do all these have in common?
- ref None
- ref []
- ref (fun x -> x)





