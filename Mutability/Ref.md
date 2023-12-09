## References

- Aka "ref" or "ref cell"

- **Pointer** to a typed location in memory

  ```ocaml
  let x = ref 0
  (* val x : int ref = {contents = 0} *)
  !x
  (* - : int = 0 *)
  x := 1
  (* this is the assignment on ref,
     - : unit = ()*)
  !x
  (* - : int = 1 *)
  ```

  Notice

  -  the type of x is `int ref` not `int`
  - the thing was changed is not the address of x points to but the content in that location

- Binding of variable to pointer: **immutable**

- Contents of memory location: **mutable**

### Definition

- Syntax : **ref e**
- Evaluation:
  - Evaluation **e** to a value **v**
  - Allocate a new location **loc** in memory to hold **v**
  - Store **v** in **loc**
  - <u>Return **loc**</u>

- Type checking:

  - New type constructor: `t ref` where t is a type
    - Note: **ref** is used as keyword in type and as keyword in value

  - **ref e : t ref** if **e : t**

### Assignment

- Syntax: **e1 : = e2**
- Evaluation:
  - Evaluate **e2** to a value **v2**
  - Evaluate **e1** to a location **loc**
  - Store **v2** in **loc**
  - Return **()**

- Type checking:
  - If **e2 : t**
  - and **e1 : t ref**
  - then **e1 := e2 : unit**

### Unit

- unit is a type
  - Its only value is (), also pronounced "unit"
  - There are no interesting operations on unit

- Analogy: Booleans
  - boolean is a type
  - It has two values
  - So unit is like a Boolean with one fewer value

- Analogy: void
  - When a preocedure in Java or C has no interesting value to return, its return type is void
  - Similar with print and assert in OCaml:
    - print_string : string -> unit
    - assert b : unit (assuming b : bool)

### References

- Syntax: **!e**
  - note: not negation

- Evaluation:
  - Evaluate **e** to **loc**
  - Return contents of **loc**

- Type checking:
  - If **e : t ref**
  - then **!e : t**



## Semicolon aka Sequence

- Syntax: **e1; e2**