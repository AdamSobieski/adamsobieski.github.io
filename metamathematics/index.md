title: "Metamathematics Sketchpad"

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

### Mathematical Expressions

Mathematical expressions can be considered as naturally being trees of $n$-ary functions, these trees capable of being mapped with arbitrary mathematical notations.

$$ equals(plus(1, 2), 3) \Leftrightarrow 1 + 2 = 3 $$

### Iterative Computation of Sets of Mathematical Expressions

Let us consider a function,

$$ \left< X_{N+1}, R_{N+1}^{+}, R_{N+1}^{-}, M_{N+1}^{+}, M_{N+1}^{-} \right> = C \left( X_{N}, R_{N}^{+}, R_{N}^{-}, M_{N}^{+}, M_{N}^{-} \right) $$

where $X_{i}$ are sets of mathematical expressions, $R_{i}^{+}$ are sets of rules for producing or adding mathematical expressions, $R_{i}^{-}$ are sets of rules for removing or deleting mathematical expressions, $M_{i}^{+}$ are sets of rules for producing or adding rules, and $M_{i}^{-}$ are sets of rules for removing or deleting rules.

An illustrative example is one where the function, $C$, is provided with the initial conditions of a set of mathematical expressions, $X_{0}$, and an initial set of additive rules, $R_{0}^{+}$.

$$ \left< X_{1}, R_{1}^{+}, R_{1}^{-}, M_{1}^{+}, M_{1}^{-} \right> = C \left( X_{0}, R_{0}^{+}, \emptyset, \emptyset, \emptyset \right) $$

For some scenarios, this output vector could be rewritten as:

$$ \left< X_{1}, R_{0}^{+}, \emptyset, \emptyset, \emptyset \right> = C \left( X_{0}, R_{0}^{+}, \emptyset, \emptyset, \emptyset \right) $$

### Mathematical Truth

The sets $X_{i}$ can be interpreted as being intended to be sets of "true" mathematical expressions.
