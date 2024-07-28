---
title: Metamathematics
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

## Expressions

[Expression](https://en.wikipedia.org/wiki/Expression_(mathematics)), [Formula](https://en.wikipedia.org/wiki/Formula)

[Variable](https://en.wikipedia.org/wiki/Variable_(mathematics)), [Variable](https://en.wikipedia.org/wiki/Variable_(computer_science)), [Free variables and bound variables](https://en.wikipedia.org/wiki/Free_variables_and_bound_variables), [Propositional variable](https://en.wikipedia.org/wiki/Propositional_variable), [Predicate variable](https://en.wikipedia.org/wiki/Predicate_variable), [Unification](https://en.wikipedia.org/wiki/Unification_(computer_science))

[Well-defined expression](https://en.wikipedia.org/wiki/Well-defined_expression), [Well-formed formula](https://en.wikipedia.org/wiki/Well-formed_formula)

## Rules

Rules can be expressed using a notation:

$$ e_{2} \in x_{i+1} \leftarrow e_{1} \in x_{i} $$

$$ e_{3} \in x_{i+1} \leftarrow e_{1} \in x_{i}, e_{2} \in x_{i} $$

$$ e_{6} \in x_{i+1}, e_{7} \in x_{i+1} \leftarrow e_{4} \in x_{i}, e_{5} \in x_{i} $$

This notation is useful for cases where rules involve multiple input and/or output sets:

$$ \rho_{2} \in r_{i+1}^{+} \leftarrow e_{1} \in x_{i}, \rho_{1} \in  r_{i}^{+} $$

In some cases, when the sets being dealt with are clear in a context, this notation can be simplified to:

$$ e_{2} \leftarrow e_{1} $$

$$ e_{3} \leftarrow e_{1}, e_{2} $$

$$ e_{6}, e_{7} \leftarrow e_{4}, e_{5} $$

Considering again the elaborated notation, we can explore scenarios resembling:

$$ e_{2} \in x_{i+1} \leftarrow e_{1} \notin x_{i} $$

$$ e_{2} \notin x_{i+1} \leftarrow e_{1} \in x_{i} $$

Which, more succinctly, could be expressed:

$$ e_{2} \leftarrow \overline{e_{1}} $$

$$ \overline{e_{2}} \leftarrow e_{1} $$

Note that rules can preserve their inputs across their transformations:

$$ e_{1}, e_{2} \leftarrow e_{1} $$

Certain additive [rules of inference](https://en.wikipedia.org/wiki/Rule_of_inference) should be carefully considered before being added to the types of systems under discussion. That is, something like [conjunction introduction](https://en.wikipedia.org/wiki/Conjunction_introduction):

$$ e_{1}, e_{2}, e_{1} \wedge e_{2} \leftarrow e_{1}, e_{2} $$

would result in a combinatorial amount of expressions being added to sets $x_{i}$ per iteration.

## Iterated Computation

Let us consider a function, $C$, such that

$$ \left< x_{n+1}, r_{n+1}^{+}, r_{n+1}^{-}, m_{n+1}^{++}, m_{n+1}^{+-}, m_{n+1}^{-+}, m_{n+1}^{--} \right> = C\left( \left< x_{n}, r_{n}^{+}, r_{n}^{-}, m_{n}^{++}, m_{n}^{+-}, m_{n}^{-+}, m_{n}^{--} \right> \right) $$

where $x_{i}$ are sets of mathematical expressions, $r_{i}^{+}$ are sets of rules for adding mathematical expressions, $r_{i}^{-}$ are sets of rules for removing mathematical expressions, $m_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $m_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $m_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $m_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

Per the notation of [iterated functions](https://en.wikipedia.org/wiki/Iterated_function), we can write:

$$ \left< x_{N}, r_{N}^{+}, r_{N}^{-}, m_{N}^{++}, m_{N}^{+-}, m_{N}^{-+}, m_{N}^{--} \right> = C^{N}\left( \left< x_{0}, r_{0}^{+}, r_{0}^{-}, m_{0}^{++}, m_{0}^{+-}, m_{0}^{-+}, m_{0}^{--} \right> \right) $$

Let us use a syntax convention that $r_{n}^{+}( x_{n})$ means those expressions produced by applying the rules in set $r_{n}^{+}$ to a set of mathematical expressions $x_{n}$, and a syntax convention that $m_{n}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-})$ means those rules produced by applying the rules in set $m_{n}^{++}$ to a set of mathematical expressions $x_{n}$ and sets of rules $r_{n}^{+}$ and $r_{n}^{-}$.

Let the resulting set of expressions from a set of rules, $r_{i}^{+}$, applied to a set of mathematical expressions, $x_{i}$, be the union of the resulting set from each individual rule, $\rho_{ij}^{+}$, contained in that set of rules, $r_{i}^{+}$, applied to $x_{i}$.

$$ r_{i}^{+}(x) = \bigcup_{\rho_{ij}^{+} \in r_{i}^{+}} \rho_{ij}^{+}(x) $$

$$ r_{i}^{-}(x) = \bigcup_{\rho_{ij}^{-} \in r_{i}^{-}} \rho_{ij}^{-}(x) $$

Similarly with the set of rules $m_{i}^{++}$ and the individual rules, $\mu_{ij}^{++}$, contained in that set.

$$ m_{i}^{++}(x, r^{+}, r^{-}) = \bigcup_{\mu_{ij}^{++} \in m_{i}^{++}} \mu_{ij}^{++}(x, r^{+}, r^{-}) $$

$$ m_{i}^{+-}(x, r^{+}, r^{-}) = \bigcup_{\mu_{ij}^{+-} \in m_{i}^{+-}} \mu_{ij}^{+-}(x, r^{+}, r^{-}) $$

$$ m_{i}^{-+}(x, r^{+}, r^{-}) = \bigcup_{\mu_{ij}^{-+} \in m_{i}^{-+}} \mu_{ij}^{-+}(x, r^{+}, r^{-}) $$

$$ m_{i}^{--}(x, r^{+}, r^{-}) = \bigcup_{\mu_{ij}^{--} \in m_{i}^{--}} \mu_{ij}^{--}(x, r^{+}, r^{-}) $$

Let the following equations describe $C$:

$$ x_{n+1} = r_{n}^{+}(x_{n}) \setminus r_{n}^{-}(x_{n}) $$

$$ r_{n+1}^{+} = m_{n}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-}) \setminus m_{n}^{+-}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ r_{n+1}^{-} = m_{n}^{-+}(x_{n}, r_{n}^{+}, r_{n}^{-}) \setminus m_{n}^{--}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ m_{n+1}^{++} = m_{n}^{++} $$

$$ m_{n+1}^{+-} = m_{n}^{+-} $$

$$ m_{n+1}^{-+} = m_{n}^{-+} $$

$$ m_{n+1}^{--} = m_{n}^{--} $$

This set of equations can be simplified:

$$ x_{n+1} = r_{n}^{+}(x_{n}) \setminus r_{n}^{-}(x_{n}) $$

$$ r_{n+1}^{+} = m_{0}^{++}(x_{n}, r_{n}^{+}, r_{n}^{-}) \setminus m_{0}^{+-}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

$$ r_{n+1}^{-} = m_{0}^{-+}(x_{n}, r_{n}^{+}, r_{n}^{-}) \setminus m_{0}^{--}(x_{n}, r_{n}^{+}, r_{n}^{-}) $$

There are two deltas or differences to consider between the sets of mathematical expressions $x_{n}$ and $x_{n+1}$. Firstly, there is the set of mathematical expressions that were added to $x_{n}$ to result in $x_{n+1}$. Secondly, there is the set of mathematical expressions that were removed from $x_{n}$ to result in $x_{n+1}$.

$$ \Delta_{x_{n+1} \leftarrow x_{n}}^{+} = x_{n+1} \setminus x_{n} $$

$$ \Delta_{x_{n+1} \leftarrow x_{n}}^{-} = x_{n} \setminus x_{n+1} $$

## Abstract Rewriting Systems

[Rewriting](https://en.wikipedia.org/wiki/Rewriting), [Abstract rewriting system](https://en.wikipedia.org/wiki/Abstract_rewriting_system)

## Lindenmayer Systems

[L-system](https://en.wikipedia.org/wiki/L-system)

## Rule Induction

[Rule induction](https://en.wikipedia.org/wiki/Rule_induction)

## Grammar Induction

[Grammar induction](https://en.wikipedia.org/wiki/Grammar_induction), [Grammar-based code](https://en.wikipedia.org/wiki/Grammar-based_code)

## Tree Automata

[Tree automaton](https://en.wikipedia.org/wiki/Tree_automaton)

## Reverse Mathematics

[Reverse mathematics](https://en.wikipedia.org/wiki/Reverse_mathematics)

## Differentiable Self-organizing Systems

[https://distill.pub/2020/selforg/](https://distill.pub/2020/selforg/), [https://distill.pub/2020/growing-ca/](https://distill.pub/2020/growing-ca/)

## Graph Neural Networks

[Graph neural network](https://en.wikipedia.org/wiki/Graph_neural_network), [Hypergraph](https://en.wikipedia.org/wiki/Hypergraph)

## Systems Biology

What if artificial-intelligence systems controlling the iterated computation of sets of rules upon sets of expressions could focus computation, from operating upon entire sets of rules and entire sets of expressions, to operating upon contextually relevant subsets of rules and on contextually relevant subsets of expressions?

Let us consider a task of reconstructing portions of graphs of or sets of expressions and rules after perturbative events. One can observe [differentiable cellular automata](https://distill.pub/2020/growing-ca/) for an example of a self-organizing system capable of self-repair.

An analogy can be drawn with the [regulation of gene expression](https://en.wikipedia.org/wiki/Regulation_of_gene_expression) by [gene regulatory networks](https://en.wikipedia.org/wiki/Gene_regulatory_network) in living cells.

That is, only a subset of the rules and the expressions would need to be "expressed", and thus computed, at each iteration.

## Multi-agent Systems

Similarly, [multi-agent systems](https://en.wikipedia.org/wiki/Multi-agent_system) could create, select, and orchestrate specialized [agents](https://en.wikipedia.org/wiki/Intelligent_agent) which operate upon graphs of or sets of expressions and rules.

## Truth and Paradox

For some systems, the expressions in sets $x$ can be interpreted as being intended to be "true".

[Truth](https://en.wikipedia.org/wiki/Truth), [Paradox](https://en.wikipedia.org/wiki/Paradox), [Paradoxes and Contemporary Logic](https://plato.stanford.edu/entries/paradoxes-contemporary-logic/), [Self-reference and Paradox](https://plato.stanford.edu/entries/self-reference/)

## Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
