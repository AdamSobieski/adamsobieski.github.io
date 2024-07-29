---
title: Metamathematics
---

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

## Expressions

[Expression](https://en.wikipedia.org/wiki/Expression_(mathematics)), [Formula](https://en.wikipedia.org/wiki/Formula)

[Variable](https://en.wikipedia.org/wiki/Variable_(mathematics)), [Variable](https://en.wikipedia.org/wiki/Variable_(computer_science)), [Free variables and bound variables](https://en.wikipedia.org/wiki/Free_variables_and_bound_variables), [Propositional variable](https://en.wikipedia.org/wiki/Propositional_variable), [Predicate variable](https://en.wikipedia.org/wiki/Predicate_variable), [Unification](https://en.wikipedia.org/wiki/Unification_(computer_science))

[Well-defined expression](https://en.wikipedia.org/wiki/Well-defined_expression), [Well-formed formula](https://en.wikipedia.org/wiki/Well-formed_formula)

## Rules

[Pattern matching](https://en.wikipedia.org/wiki/Pattern_matching), [Query language](https://en.wikipedia.org/wiki/Query_language), [Relational algebra](https://en.wikipedia.org/wiki/Relational_algebra)

There are different kinds of rules. For instance, some rules operate on sets of expressions and others on graphs. Let us consider the following notations for rules:

$$ \rho_{1}(I, O) := e_{2} \in O \leftarrow e_{1} \in I $$

$$ \rho_{2}(I, O) := e_{3} \in O \leftarrow e_{1} \in I, e_{2} \in I $$

$$ \rho_{3}(I, O) := e_{6} \in O, e_{7} \in O \leftarrow e_{4} \in I, e_{5} \in I $$

$$ \dots $$

We could then define a set of rules

$$ R(I, O) = \left{\rho_{1}(I, O), \rho_{2}(I, O), \rho_{3}(I, O) \right}

Rules can involve multiple input and/or output sets:

$$ \rho_{2} \in R_{i+1}^{+} \leftarrow e_{1} \in X_{i}, \rho_{1} \in  R_{i}^{+} $$

When the sets being dealt with are clear in a context, notations can be simplified to:

$$ e_{2} \leftarrow e_{1} $$

$$ e_{3} \leftarrow e_{1}, e_{2} $$

$$ e_{6}, e_{7} \leftarrow e_{4}, e_{5} $$

Considering again the elaborated notation, we can explore scenarios resembling:

$$ e_{2} \in X_{i+1} \leftarrow e_{1} \notin X_{i} $$

$$ e_{2} \notin X_{i+1} \leftarrow e_{1} \in X_{i} $$

Which, more succinctly, could be expressed:

$$ e_{2} \leftarrow \overline{e_{1}} $$

$$ \overline{e_{2}} \leftarrow e_{1} $$

Note that rules can preserve their inputs across their transformations:

$$ e_{1}, e_{2} \leftarrow e_{1} $$

Certain additive [rules of inference](https://en.wikipedia.org/wiki/Rule_of_inference) should be carefully considered before being added to the types of systems under discussion. That is, something like [conjunction introduction](https://en.wikipedia.org/wiki/Conjunction_introduction):

$$ e_{1}, e_{2}, e_{1} \wedge e_{2} \leftarrow e_{1}, e_{2} $$

would result in a combinatorial amount of expressions being added per iteration.

Let us define the cardinality of a rule application as the cardinality of the set of expressions that it produces. If a rule's antecedent does not match any expressions, or if it otherwise produces the empty set, $\emptyset$, then the cardinality of that rule application is $0$.

$$ \left\lvert e_{2} \in X_{i+1} \leftarrow e_{1} \in X_{i} \right\rvert $$

For each time that $e_{1}$ matches an expression in $X_{i}$, output expressions are produced, and the number of distinct expressions $e_{2}$ is the cardinality of the rule application.

Towards analyzing the the computational complexities of rule applications, we can consider the ranks of their antecedents and consequents. Let the rank of a rule's antecedent be the number of comma-delimited expressions in it involving set $X$.

$$ rank_{X_{i}}(e_{2} \leftarrow e_{1}) = 1$$

$$ rank_{X_{i}}(e_{3} \leftarrow e_{1}, e_{2}) = 2 $$

So the rank of rules' antecedents can be obtained for rules involving multiple sets:

$$ rank_{X_{i}}(\rho_{2} \in R_{i+1}^{+} \leftarrow e_{1} \in X_{i}, \rho_{1} \in  R_{i}^{+}) = 1 $$

$$ rank_{R_{i}^{+}}(\rho_{2} \in R_{i+1}^{+} \leftarrow e_{1} \in X_{i}, \rho_{1} \in  R_{i}^{+}) = 1 $$

The number of comparisons or matches which need to be explored, computationally, by the application of a rule is the product of the cardinality each involved set raised to the power of the rank of the rule's antecedent with respect to that set.

$$ cost(e_{3} \in X_{i+1} \leftarrow e_{1} \in X_{i}, e_{2} \in X_{i}) = \left\lvert X_{i} \right\rvert^{2} $$

$$ cost(\rho_{2} \in R_{i+1}^{+} \leftarrow e_{1} \in X_{i}, \rho_{1} \in  R_{i}^{+}) = \left\lvert X_{i} \right\rvert \left\lvert R_{i}^{+} \right\rvert $$

## Iterated Computation

Let us consider a function, $C$, such that

$$ \left< X_{n+1}, R_{n+1}^{+}, R_{n+1}^{-}, M_{n+1}^{++}, M_{n+1}^{+-}, M_{n+1}^{-+}, M_{n+1}^{--} \right> = C\left( \left< X_{n}, R_{n}^{+}, R_{n}^{-}, M_{n}^{++}, M_{n}^{+-}, M_{n}^{-+}, M_{n}^{--} \right> \right) $$

where $X_{i}$ are sets of mathematical expressions, $R_{i}^{+}$ are sets of rules for adding mathematical expressions, $R_{i}^{-}$ are sets of rules for removing mathematical expressions, $M_{i}^{++}$ are sets of rules for adding rules to sets of additive rules, $M_{i}^{+-}$ are sets of rules for removing rules from sets of additive rules, $M_{i}^{-+}$ are sets of rules for adding rules to sets of subtractive rules, and $M_{i}^{\-\-}$ are sets of rules for removing rules from sets of subtractive rules.

Per the notation of [iterated functions](https://en.wikipedia.org/wiki/Iterated_function), we can write:

$$ \left< X_{n}, R_{n}^{+}, R_{n}^{-}, M_{n}^{++}, M_{n}^{+-}, M_{n}^{-+}, M_{n}^{--} \right> = C^{n}\left( \left< X_{0}, R_{0}^{+}, R_{0}^{-}, M_{0}^{++}, M_{0}^{+-}, M_{0}^{-+}, M_{0}^{--} \right> \right) $$

Let us use a syntax convention that $R_{n}^{+}( X_{n})$ means those expressions produced by applying the rules in set $R_{n}^{+}$ to a set of mathematical expressions $X_{n}$, and a syntax convention that $M_{n}^{++}(X_{n}, R_{n}^{+}, R_{n}^{-})$ means those rules produced by applying the rules in set $M_{n}^{++}$ to a set of mathematical expressions $X_{n}$ and sets of rules $R_{n}^{+}$ and $R_{n}^{-}$.

Let the resulting set of expressions from a set of rules, $R_{i}^{+}$, applied to a set of mathematical expressions, $x$, be the union of the resulting set from each individual rule, $\rho_{ij}^{+}$, contained in that set of rules, $R_{i}^{+}$, applied to that set, $x$.

$$ R_{i}^{+}(x) = \bigcup_{\rho_{ij}^{+} \in R_{i}^{+}} \rho_{ij}^{+}(x) $$

$$ R_{i}^{-}(x) = \bigcup_{\rho_{ij}^{-} \in R_{i}^{-}} \rho_{ij}^{-}(x) $$

Similarly with the set of rules $M_{i}^{++}$ and the individual rules, $\mu_{ij}^{++}$, contained in that set.

$$ M_{i}^{++}(x, y, z) = \bigcup_{\mu_{ij}^{++} \in M_{i}^{++}} \mu_{ij}^{++}(x, y, z) $$

$$ M_{i}^{+-}(x, y, z) = \bigcup_{\mu_{ij}^{+-} \in M_{i}^{+-}} \mu_{ij}^{+-}(x, y, z) $$

$$ M_{i}^{-+}(x, y, z) = \bigcup_{\mu_{ij}^{-+} \in M_{i}^{-+}} \mu_{ij}^{-+}(x, y, z) $$

$$ M_{i}^{--}(x, y, z) = \bigcup_{\mu_{ij}^{--} \in M_{i}^{--}} \mu_{ij}^{--}(x, y, z) $$

Let the following equations describe $C$:

$$ X_{n+1} = R_{n}^{+}(X_{n}) \setminus R_{n}^{-}(X_{n}) $$

$$ R_{n+1}^{+} = M_{n}^{++}(X_{n}, R_{n}^{+}, R_{n}^{-}) \setminus M_{n}^{+-}(X_{n}, R_{n}^{+}, R_{n}^{-}) $$

$$ R_{n+1}^{-} = M_{n}^{-+}(X_{n}, R_{n}^{+}, R_{n}^{-}) \setminus M_{n}^{--}(X_{n}, R_{n}^{+}, R_{n}^{-}) $$

$$ M_{n+1}^{++} = M_{n}^{++} $$

$$ M_{n+1}^{+-} = M_{n}^{+-} $$

$$ M_{n+1}^{-+} = M_{n}^{-+} $$

$$ M_{n+1}^{--} = M_{n}^{--} $$

This set of equations can be simplified:

$$ X_{n+1} = R_{n}^{+}(X_{n}) \setminus R_{n}^{-}(X_{n}) $$

$$ R_{n+1}^{+} = M_{0}^{++}(X_{n}, R_{n}^{+}, R_{n}^{-}) \setminus M_{0}^{+-}(X_{n}, R_{n}^{+}, R_{n}^{-}) $$

$$ R_{n+1}^{-} = M_{0}^{-+}(X_{n}, R_{n}^{+}, R_{n}^{-}) \setminus M_{0}^{--}(X_{n}, R_{n}^{+}, R_{n}^{-}) $$

There are two deltas or differences to consider between the sets of mathematical expressions $X_{n}$ and $X_{n+1}$. Firstly, there is the set of mathematical expressions that were added to $X_{n}$ to result in $X_{n+1}$. Secondly, there is the set of mathematical expressions that were removed from $X_{n}$ to result in $X_{n+1}$.

$$ \Delta_{X_{n+1} \leftarrow X_{n}}^{+} = X_{n+1} \setminus X_{n} $$

$$ \Delta_{X_{n+1} \leftarrow X_{n}}^{-} = X_{n} \setminus X_{n+1} $$

With cardinalities:

$$ \left\lvert \Delta_{X_{n+1} \leftarrow X_{n}}^{+} \right\rvert = \left\lvert X_{n+1} \right\rvert - \left\lvert X_{n+1} \cap X_{n} \right\rvert = \left\lvert X_{n+1} \cup X_{n} \right\rvert - \left\lvert X_{n} \right\rvert $$

$$ \left\lvert \Delta_{X_{n+1} \leftarrow X_{n}}^{-} \right\rvert = \left\lvert X_{n} \right\rvert - \left\lvert X_{n+1} \cap X_{n} \right\rvert = \left\lvert X_{n+1} \cup X_{n} \right\rvert - \left\lvert X_{n+1} \right\rvert $$

From which we can obtain:

$$ \left\lvert X_{n+1} \right\rvert = \left\lvert X_{n} \right\rvert + \left\lvert \Delta_{X_{n+1} \leftarrow X_{n}}^{+} \right\rvert - \left\lvert \Delta_{X_{n+1} \leftarrow X_{n}}^{-} \right\rvert $$

## Abstract Rewriting Systems

[Rewriting](https://en.wikipedia.org/wiki/Rewriting), [Abstract rewriting system](https://en.wikipedia.org/wiki/Abstract_rewriting_system)

## Lindenmayer Systems

[L-system](https://en.wikipedia.org/wiki/L-system)

## Knowledge Graph Completion

[Knowledge graph](https://en.wikipedia.org/wiki/Knowledge_graph)

Chen, Zhe, Yuehan Wang, Bin Zhao, Jing Cheng, Xin Zhao, and Zongtao Duan. "Knowledge graph completion: A review." _IEEE Access_ 8 (2020): 192435-192456. [[PDF](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9220143)]

## Tree Automata

[Tree automaton](https://en.wikipedia.org/wiki/Tree_automaton)

## Rule Induction

[Rule induction](https://en.wikipedia.org/wiki/Rule_induction)

## Grammar Induction

[Grammar induction](https://en.wikipedia.org/wiki/Grammar_induction), [Grammar-based code](https://en.wikipedia.org/wiki/Grammar-based_code)

## Ontology Induction

[Ontology learning](https://en.wikipedia.org/wiki/Ontology_learning)

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

For some systems, the expressions in sets $X$ can be interpreted as being intended to be "true".

[Truth](https://en.wikipedia.org/wiki/Truth), [Paradox](https://en.wikipedia.org/wiki/Paradox), [Paradoxes and Contemporary Logic](https://plato.stanford.edu/entries/paradoxes-contemporary-logic/), [Self-reference and Paradox](https://plato.stanford.edu/entries/self-reference/)

## Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
