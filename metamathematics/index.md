---
title: Metamathematics
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

### Iterated Computation of Sets of Expressions and Rules

Let us consider a function, $C$, such that

$$ \left< x_{n+1}, r_{n+1}^{+}, r_{n+1}^{-}, m_{n+1}^{++}, m_{n+1}^{+-}, m_{n+1}^{-+}, m_{n+1}^{--} \right> = C\left( \left< x_{n}, r_{n}^{+}, r_{n}^{-}, m_{n}^{++}, m_{n}^{+-}, m_{n}^{-+}, m_{n}^{--} \right> \right) $$

where $x_{i}$ are sets of mathematical expressions, $r_{i}^{+}$ are sets of rules for adding mathematical expressions, $r_{i}^{-}$ are sets of rules for removing mathematical expressions, $m_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $m_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $m_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $m_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

Per the notation of [iterated functions](https://en.wikipedia.org/wiki/Iterated_function), we can write:

$$ \left< x_{N}, r_{N}^{+}, r_{N}^{-}, m_{N}^{++}, m_{N}^{+-}, m_{N}^{-+}, m_{N}^{--} \right> = C^{N}\left( \left< x_{0}, r_{0}^{+}, r_{0}^{-}, m_{0}^{++}, m_{0}^{+-}, m_{0}^{-+}, m_{0}^{--} \right> \right) $$

Let us use a syntax convention that $r_{n}^{+}( x_{n})$ means those expressions produced by applying the rules in set $r_{n}^{+}$ to a set of mathematical expressions $x_{n}$, and a syntax convention that $m_{n}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-})$ means those rules produced by applying the rules in set $m_{n}^{++}$ to a set of mathematical expressions $x_{n}$ and sets of rules $r_{n}^{+}$ and $r_{n}^{-}$.

Let the resulting set of expressions from a set of rules, $r_{i}^{+}$, applied to a set of mathematical expressions, $x_{i}$, be the union of the resulting set from each individual rule, $\rho_{ij}^{+}$, contained in that set of rules, $r_{i}^{+}$, applied to $x_{i}$.

$$ r_{i}^{+}(x_{i}) = \bigcup_{\rho_{ij}^{+} \in r_{i}^{+}} \rho_{ij}^{+}(x_{i}) $$

$$ r_{i}^{-}(x_{i}) = \bigcup_{\rho_{ij}^{-} \in r_{i}^{-}} \rho_{ij}^{-}(x_{i}) $$

Similarly with the set of rules $m_{i}^{++}$ and the individual rules, $\mu_{ij}^{++}$, contained in that set.

$$ m_{i}^{++}(x_{i}, r_{i}^{+}, r_{i}^{-}) = \bigcup_{\mu_{ij}^{++} \in m_{i}^{++}} \mu_{ij}^{++}(x_{i}, r_{i}^{+}, r_{i}^{-}) $$

$$ m_{i}^{+-}(x_{i}, r_{i}^{+}, r_{i}^{-}) = \bigcup_{\mu_{ij}^{+-} \in m_{i}^{+-}} \mu_{ij}^{+-}(x_{i}, r_{i}^{+}, r_{i}^{-}) $$

$$ m_{i}^{-+}(x_{i}, r_{i}^{+}, r_{i}^{-}) = \bigcup_{\mu_{ij}^{-+} \in m_{i}^{-+}} \mu_{ij}^{-+}(x_{i}, r_{i}^{+}, r_{i}^{-}) $$

$$ m_{i}^{--}(x_{i}, r_{i}^{+}, r_{i}^{-}) = \bigcup_{\mu_{ij}^{--} \in m_{i}^{--}} \mu_{ij}^{--}(x_{i}, r_{i}^{+}, r_{i}^{-}) $$

Let the following equations describe $C$:

$$ x_{n+1} = \left( x_{n} \cup r_{n}^{+}(x_{n}) \right) \setminus r_{n}^{-}(x_{n}) $$

$$ r_{n+1}^{+} = \left( r_{n}^{+} \cup m_{n}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-}) \right) \setminus m_{n}^{+-}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ r_{n+1}^{-} = \left( r_{n}^{-} \cup m_{n}^{-+}(x_{n}, r_{n}^{+}, r_{n}^{-}) \right) \setminus m_{n}^{--}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ m_{n+1}^{++} = m_{n}^{++} $$

$$ m_{n+1}^{+-} = m_{n}^{+-} $$

$$ m_{n+1}^{-+} = m_{n}^{-+} $$

$$ m_{n+1}^{--} = m_{n}^{--} $$

This set of equations can be simplified:

$$ x_{n+1} = \left( x_{n} \cup r_{n}^{+}(x_{n}) \right) \setminus r_{n}^{-}(x_{n}) $$

$$ r_{n+1}^{+} = \left( r_{n}^{+} \cup m_{0}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-}) \right) \setminus m_{0}^{+-}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ r_{n+1}^{-} = \left( r_{n}^{-} \cup m_{0}^{-+}(x_{n}, r_{n}^{+}, r_{n}^{-}) \right) \setminus m_{0}^{--}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

There are two deltas or differences to consider between the sets of mathematical expressions $x_{n}$ and $x_{n+1}$. Firstly, there is the set of mathematical expressions that were added to $x_{n}$ to result in $x_{n+1}$. Secondly, there is the set of mathematical expressions that were removed from $x_{n}$ to result in $x_{n+1}$.

$$ \Delta_{x_{n} \rightarrow x_{n+1}}^{+} = x_{n+1} \setminus x_{n} $$

$$ \Delta_{x_{n} \rightarrow x_{n+1}}^{-} = x_{n} \setminus x_{n+1} $$

### Rules

Rules could be expressed with a notation resembling:

$$ e_{3} \in x_{i+1} \stackrel{+}\leftarrow e_{1} \in x_{i} \wedge e_{2} \in x_{i} $$

Note that certain additive rules of inference should be carefully considered before being added to the types of systems under discussion.

That is, something like [conjunction introduction](https://en.wikipedia.org/wiki/Conjunction_introduction):

$$ e_{1} \wedge e_{2} \in x_{i+1} \stackrel{+}\leftarrow e_{1} \in x_{i} \wedge e_{2} \in x_{i} $$

would result in a combinatorial amount of expressions being added to iterated sets.

### Abstract Rewriting Systems

[Abstract rewriting system](https://en.wikipedia.org/wiki/Abstract_rewriting_system)

### Lindenmayer Systems

[L-system](https://en.wikipedia.org/wiki/L-system)

### Rule Induction

[Rule induction](https://en.wikipedia.org/wiki/Rule_induction)

### Grammar Induction

[Grammar induction](https://en.wikipedia.org/wiki/Grammar_induction), [Grammar-based code](https://en.wikipedia.org/wiki/Grammar-based_code)

### Reverse Mathematics

[Reverse mathematics](https://en.wikipedia.org/wiki/Reverse_mathematics)

### Differentiable Self-organizing Systems

[https://distill.pub/2020/selforg/](https://distill.pub/2020/selforg/), [https://distill.pub/2020/growing-ca/](https://distill.pub/2020/growing-ca/)

### Graph Neural Networks

[Graph neural network](https://en.wikipedia.org/wiki/Graph_neural_network), [Hypergraph](https://en.wikipedia.org/wiki/Hypergraph)

### Mathematical Truth

For some systems, the sets of expressions $x_{i}$ can be interpreted as being intended to be "true" expressions.

### Paradoxes

[Paradox](https://en.wikipedia.org/wiki/Paradox), [Paradoxes and Contemporary Logic](https://plato.stanford.edu/entries/paradoxes-contemporary-logic/), [Self-reference and Paradox](https://plato.stanford.edu/entries/self-reference/)

### Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
