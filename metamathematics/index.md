---
title: Metamathematics
---

## Introduction

This is a sketchpad for some [metamathematics](https://en.wikipedia.org/wiki/Metamathematics) ideas.

## Rules

There is an interesting generalization possible involving logic rules, [rewrite](https://en.wikipedia.org/wiki/Rewriting) rules, and the `INSERT` and `DELETE` commands of [query languages](https://en.wikipedia.org/wiki/Query_language). A useful analogy exists between these kinds of rules and these query language commands.

Here is an example rule: any individual ($x_{1}$) whose parent ($x_{2}$) has a brother ($x_{3}$) has an uncle ($x_{3}$).

$$ p(x_{1}, x_{2}), b(x_{2}, x_{3}) \rightarrow u(x_{1}, x_{3}) $$

Here is a SQL command resembling the logic rule:
```sql
INSERT INTO CurrentTable (s, p, o)
SELECT DISTINCT s1.s, 'u', s2.o
FROM CurrentTable s1, CurrentTable s2
WHERE s1.p = 'p' AND s2.p = 'b' AND s1.o = s2.s;
```

Here is a SPARQL command resembling the logic rule:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX ex:  <http://example.com/>

INSERT 
{
  GRAPH <http://example.com/current>
  {
    ?x1 ex:u ?x3.
  }
}
WHERE
{
  GRAPH <http://example.com/current>
  {
    ?x1 ex:p ?x2.
    ?x2 ex:b ?x3.
  }
}
```

Here is the logic rule rephrased as a rewrite rule:

$$ p(x_{1}, x_{2}), b(x_{2}, x_{3}) \rightarrow p(x_{1}, x_{2}), b(x_{2}, x_{3}), u(x_{1}, x_{3}) $$

As we are considering [rewriting](https://en.wikipedia.org/wiki/Rewriting) and [abstract rewriting systems](https://en.wikipedia.org/wiki/Abstract_rewriting_system), rules which intend to preserve their antecedents (or bodies) should copy these into their consequents (or heads). Broadly speaking, existing content (e.g., objects, expressions, rows, or subgraphs) which match specified patterns can optionally accompany any generated content intended to be placed in resultant sets, tables, or graphs.

Here is a SQL command resembling the rewrite rule:
```sql
INSERT INTO NextTable (s, p, o)
SELECT DISTINCT s1.s, 'u', s2.o
FROM CurrentTable s1, CurrentTable s2
WHERE s1.p = 'p' AND s2.p = 'b' AND s1.o = s2.s
UNION
SELECT DISTINCT s1.s, s1.p, s1.o
FROM CurrentTable s1, CurrentTable s2
WHERE s1.p = 'p' AND s2.p = 'b' AND s1.o = s2.s
UNION
SELECT DISTINCT s2.s, s2.p, s2.o
FROM CurrentTable s1, CurrentTable s2
WHERE s1.p = 'p' AND s2.p = 'b' AND s1.o = s2.s;
```

Here is a SPARQL command resembling the rewrite rule:
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX ex:  <http://example.com/>

INSERT 
{
  GRAPH <http://example.com/next>
  {
    ?x1 ex:p ?x2.
    ?x2 ex:b ?x3.
    ?x1 ex:u ?x3.
  }
}
WHERE
{
  GRAPH <http://example.com/current>
  {
    ?x1 ex:p ?x2.
    ?x2 ex:b ?x3.
  }
}
```

Note that the above rule examples pertain to additive rules. Here is an example of a subtractive rewrite rule:

$$ i(x_{1}, x_{2}), j(x_{2}, x_{3}) \rightarrow \overline{k(x_{1}, x_{3})} $$

This differs from adding expressions with logical negations to sets, tables, or graphs, it subtracts expressions if they are present. One can observe that the SPARQL command resembling it utilizes `DELETE`.

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX ex:  <http://example.com/>

DELETE
{
  GRAPH <http://example.com/next>
  {
    ?x1 ex:k ?x3.
  }
}
WHERE
{
  GRAPH <http://example.com/current>
  {
    ?x1 ex:i ?x2.
    ?x2 ex:j ?x3.
  }
}
```

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

$$ \left\lvert X_{n+1} \right\rvert = \left\lvert R_{n}^{+}(X_{n}) \right\rvert - \left\lvert R_{n}^{+}(X_{n}) \cap R_{n}^{-}(X_{n}) \right\rvert $$

## Abstract Rewriting Systems

[Abstract rewriting system](https://en.wikipedia.org/wiki/Abstract_rewriting_system), [Rewriting](https://en.wikipedia.org/wiki/Rewriting)

[Iterated function system](https://en.wikipedia.org/wiki/Iterated_function_system), [L-system](https://en.wikipedia.org/wiki/L-system)

## Knowledge Graph Completion

[Knowledge graph](https://en.wikipedia.org/wiki/Knowledge_graph)

Chen, Zhe, Yuehan Wang, Bin Zhao, Jing Cheng, Xin Zhao, and Zongtao Duan. "Knowledge graph completion: A review." _IEEE Access_ 8 (2020): 192435-192456. [[PDF](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9220143)]

## Rule Induction

[Rule induction](https://en.wikipedia.org/wiki/Rule_induction)

[Inductive logic programming](https://en.wikipedia.org/wiki/Inductive_logic_programming)

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

[Multi-agent systems](https://en.wikipedia.org/wiki/Multi-agent_system) could create, select, and orchestrate specialized [agents](https://en.wikipedia.org/wiki/Intelligent_agent) which operate upon collections of expressions and rules.

Intelligent agents in systems could all cooperate upon singular collections of expressions and rules, cooperate in groups upon multiple workspaces, or cooperate in complex orchestrations with groups and inter-group communication. Agents organized into groups could access and make use of inter-group resources and send contents and discoveries from their workspaces to these inter-group resources.

## Systems of Systems

[System of systems](https://en.wikipedia.org/wiki/System_of_systems)

## Bibliography

Silver, Charles L. _From Symbolic Logic... To Mathematical Logic_. Dubuque, IA: Brown (William C.), 1994.

Wolfram, Stephen. _Metamathematics: Foundations & Physicalization_. Champaign, IL: Wolfram Media, 2022.
