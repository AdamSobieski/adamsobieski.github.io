---
title: Metamathematics
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

### Expressions

Mathematical expressions can be considered as naturally being trees of $n$-ary functions, these trees capable of being mapped with arbitrary mathematical notations.

$$ equals(plus(1, 2), 3) \Leftrightarrow 1 + 2 = 3 $$

### Iterated Computation of Sets of Expressions and Rules

Let us consider a function, $C$,

$$ C : X \times R \times R \times M \times M \times M \times M \rightarrow X \times R \times R \times M \times M \times M \times M$$

such that

$$ \left< x_{n+1}, r_{n+1}^{+}, r_{n+1}^{-}, m_{n+1}^{++}, m_{n+1}^{+-}, m_{n+1}^{-+}, m_{n+1}^{--} \right> = C \left( \left< x_{n}, r_{n}^{+}, r_{n}^{-}, m_{n}^{++}, m_{n}^{+-}, m_{n}^{-+}, m_{n}^{--} \right> \right) $$

where $x_{i}$ are sets of mathematical expressions, $r_{i}^{+}$ are sets of rules for adding mathematical expressions, $r_{i}^{-}$ are sets of rules for removing mathematical expressions, $m_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $m_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $m_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $m_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

An illustrative example is one where a function, $C$, is provided with initial conditions including only a set of mathematical expressions, $x_{0}$, and an initial set of additive rules, $r_{0}^{+}$.

For some such scenarios, the following simplifications might hold:

$$ \left< x_{1}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = C \left( \left< x_{0}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) $$

$$ \left< x_{2}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = C \left( C \left( \left< x_{0}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) \right) $$

$$ \vdots $$

$$ \left< x_{N}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = \overbrace{C \ldots C}^{N} \left( \left< x_{0}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) $$

Which, per the notation of [iterated functions](https://en.wikipedia.org/wiki/Iterated_function), we can write:

$$ \left< x_{N}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> = C^{N} \left( \left< x_{0}, r_{0}^{+}, \emptyset, \emptyset, \emptyset, \emptyset, \emptyset \right> \right) $$

Another illustrative example is one where a function, $C$, is provided with initial conditions including only a set of mathematical expressions, $x_{0}$, an initial set of additive rules, $r_{0}^{+}$, and a set of rules for adding additive rules, $m_{0}^{++}$.

For some such scenarios, the following simplifications might hold:

$$ \left< x_{N}, r_{N}^{+}, \emptyset, m_{0}^{++}, \emptyset, \emptyset, \emptyset \right> = C^{N} \left( \left< x_{0}, r_{0}^{+}, \emptyset, m_{0}^{++}, \emptyset, \emptyset, \emptyset \right> \right) $$

Using a syntax convention that $r_{n}^{+} \left( x_{n} \right)$ means those expressions produced by applying the rules $r_{n}^{+}$ to a set of mathematical expressions $x_{n}$, and a syntax convention that $m_{n}^{++} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right)$ means those rules produced by applying the rules $m_{n}^{++}$ to a set of mathematical expressions $x_{n}$ and sets of rules $r_{n}^{+}$ and $r_{n}^{-}$, the following could be stated with respect to a possible implementation of a function $C$:

$$ x_{n+1} = \left( x_{n} \cup r_{n}^{+} \left( x_{n} \right) \right) \setminus r_{n}^{-} \left( x_{n} \right) $$

$$ r_{n+1}^{+} = \left( r_{n}^{+} \cup m_{n}^{++} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) \right) \setminus m_{n}^{+-} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) $$

$$ r_{n+1}^{-} = \left( r_{n}^{-} \cup m_{n}^{-+} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) \right) \setminus m_{n}^{--} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) $$

$$ m_{n+1}^{++} = m_{n}^{++} $$

$$ m_{n+1}^{+-} = m_{n}^{+-} $$

$$ m_{n+1}^{-+} = m_{n}^{-+} $$

$$ m_{n+1}^{--} = m_{n}^{--} $$

This set of equations could be simplified:

$$ x_{n+1} = \left( x_{n} \cup r_{n}^{+} \left( x_{n} \right) \right) \setminus r_{n}^{-} \left( x_{n} \right) $$

$$ r_{n+1}^{+} = \left( r_{n}^{+} \cup m_{0}^{++} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) \right) \setminus m_{0}^{+-} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) $$

$$ r_{n+1}^{-} = \left( r_{n}^{-} \cup m_{0}^{-+} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) \right) \setminus m_{0}^{--} \left( x_{n}, r_{n}^{+}, r_{n}^{-} \right) $$

### Rules Applied to Sets of Expressions and Rules

### Rulial Systems

### Mathematical Truth

The sets of mathematical expressions, e.g., $x_{i}$, can be interpreted as being intended to be sets of "true" mathematical expressions.

### Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
