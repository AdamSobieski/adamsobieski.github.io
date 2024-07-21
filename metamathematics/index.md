---
title: Metamathematics
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

### Mathematical Expressions

Mathematical expressions can be considered as naturally being trees of $n$-ary functions, these trees capable of being mapped with arbitrary mathematical notations.

$$ equals(plus(1, 2), 3) \Leftrightarrow 1 + 2 = 3 $$

### Iterative Computation of Sets of Mathematical Expressions

Let us consider a function,

$$ \left< X_{k+1}, R_{k+1}^{+}, R_{k+1}^{-}, M_{k+1}^{++}, M_{k+1}^{+-}, M_{k+1}^{-+}, M_{k+1}^{--} \right> = C \left( \left< X_{k}, R_{k}^{+}, R_{k}^{-}, M_{k}^{++}, M_{k}^{+-}, M_{k}^{-+}, M_{k}^{--} \right> \right) $$

where $X_{i}$ are sets of mathematical expressions, $R_{i}^{+}$ are sets of rules for adding mathematical expressions, $R_{i}^{-}$ are sets of rules for removing mathematical expressions, $M_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $M_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $M_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $M_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

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

One approach is to consider that a set of rules could exist in $m_{0}^{++}$ which would otherwise utilize both expressions from $x_{i}$ and rules from $r_{i}^{+}$ to add rules to $r_{i+1}^{+}$, those rules which could be used to add expressions into $x_{i+2}$.

In this approach, using the convention that $R_{n}^{+} \left( X_{n} \right)$ means those expressions produced by applying the rules $R_{n}^{+}$ to the set of mathematical expressions $X_{n}$, the following could be stated with respect to one possible $C$:

$$ X_{n+1} = \left( X_{n} \cup R_{n}^{+} \left( X_{n} \right) \right) \setminus R_{n}^{-} \left( X_{n} \right) $$

$$ R_{n+1}^{+} = \left( R_{n}^{+} \cup M_{n}^{++} \left( R_{n}^{+} \right) \right) \setminus M_{n}^{+-} \left( R_{n}^{+} \right) $$

$$ R_{n+1}^{-} = \left( R_{n}^{-} \cup M_{n}^{-+} \left( R_{n}^{-} \right) \right) \setminus M_{n}^{--} \left( R_{n}^{-} \right) $$

$$ M_{n+1}^{++} = M_{n}^{++}$$

$$ M_{n+1}^{+-} = M_{n}^{+-}$$

$$ M_{n+1}^{-+} = M_{n}^{-+}$$

$$ M_{n+1}^{--} = M_{n}^{--}$$

### Rules Applied to Expressions and to Rules

### Rulial Systems

### Mathematical Truth

The sets of mathematical expressions, e.g., $x_{i}$, can be interpreted as being intended to be sets of "true" mathematical expressions.

### Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
