---
title: Metamathematics Sketchpad
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

### Mathematical Expressions

Mathematical expressions can be considered as naturally being trees of $n$-ary functions, these trees capable of being mapped with arbitrary mathematical notations.

$$ equals(plus(1, 2), 3) \Leftrightarrow 1 + 2 = 3 $$

### Iterative Computation of Sets of Mathematical Expressions

Let us consider a function,

$$ \left< X_{N+1}, R_{N+1}^{+}, R_{N+1}^{-}, M_{N+1}^{++}, M_{N+1}^{+-}, M_{N+1}^{-+}, M_{N+1}^{--} \right> = C \left( \left< X_{N}, R_{N}^{+}, R_{N}^{-}, M_{N}^{++}, M_{N}^{+-}, M_{N}^{-+}, M_{N}^{--} \right> \right) $$

where $X_{i}$ are sets of mathematical expressions, $R_{i}^{+}$ are sets of rules for adding mathematical expressions, $R_{i}^{-}$ are sets of rules for removing mathematical expressions, $M_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $M_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $M_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $M_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

An illustrative example is one where a function, $C$, is provided with initial conditions including only a set of mathematical expressions, $X_{0}$, and an initial set of additive rules, $R_{0}^{+}$.

For some such scenarios, the following simplifications might hold:

$$ \left< X_{1}, R_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = C \left( \left< X_{0}, R_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) $$

$$ \left< X_{N}, R_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = \overbrace{C ... C_\text{N}} \left( \left< X_{0}, R_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) $$

### Mathematical Truth

The sets $X_{i}$ can be interpreted as being intended to be sets of "true" mathematical expressions.
