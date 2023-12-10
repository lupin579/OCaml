type inference algorithm proceeds as follows:
1. Each node of AST is **annotated**(aka **decorated**) with a unique type variable.
2. The AST is traversed to collect a set of equations between types that must hold for the expression to be well-typed.
3. Finally, those equations are solved to find an assignment of types to the original variables; this step is called **unification**
simplified version as follows:
1. annotate AST with unique type variable
2. collect constraints
3. unification
