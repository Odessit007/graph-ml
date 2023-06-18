[Headers](#Introduction)

[Mathematical definitions](#Mathematical definitions)

[Neighbors and degrees](#Neighbors and degrees)
[Paths and cycles](#Paths and cycles)


<a name="introduction"/>
# Introduction
**Graph** is a data structure consisting of **nodes**, **edges** that connect nodes, and potentially additional data attached to nodes and/or edges.


Typical examples:
* social networks
* biological networks
* transportation networks
* computer networks
* ontologies
* knowledge graphs


Main graph types:
* by the presence of edge direction:
    * undirected graphs: the two nodes of an edge are "equal"; there is no notion of edge "from a to b" and "from b to a"
    * directed graphs (or digraphs): the edge is going "from" one node "to" another
* by the allowed number of edges between nodes:
    * simple graphs: each pair of nodes can have at most one edge
    * multigraphs: there can be more than one edge
* by the presence of edges connecting node with itself (**loops**):
    * with loops
    * without loops
* by the presence of weights:
    * weighted: there are numbers attached to edges
    * unweighted
* by the number of nodes:
    * finite: there is a finite number of nodes
    * infinite: there are infinitely many nodes
* by the possibility of changing over time:
    * dynamic: if nodes/edges can be added/removed over time
    * static: if the graph is given as is and not allowed to be changed


Here I consider only *finite* graphs.


# Mathematical definitions

A **simple undirected graph** is a pair $(V, E)$ where
* $V$ is a set of **nodes** (also called **vertices**)
* $E$ is a set of **edges** (also called **links**)
    * edges are represented as *unordered* pairs (or sets) of vertices: edge $\{a, b\}$ is the same as edge $\{b, a\}$
    
For **simple directed graph** $E$ contains of *ordered* pairs of vertices: $(a, b)$ and $(b, a)$ are two differente edges. There can be both of them, one of them, or none of them between any pair of nodes.
    
For **(un)directed multigraph** $E$ is a *multiset* instead of *set*, so the same pair can be present more than once.


A **weighted graph** is a triple $(V, E, w)$ where $w: E \rightarrow \mathbb{R}$ is a function that assigns **weight** $w(e)$ to each edge $e \in E$.


The **order** of a graph is the number of its vertices $|V|$.

The **size** of a graph is the number of its edges $E$.


### Density of a simple graph
**Graph density** of a simple undirected graph without loops is the ratio between the number of edges it actually has and the number of edges it *can* have:
$$D(G) = \frac{|E|}{\frac{|V| * (|V| - 1)}{2}} = \frac{2 |E|}{|V| (|V| - 1)}$$

For a simple undirected graph that can have loops,
$$D(G) = \frac{2 |E|}{|V| (|V| + 1)}$$

For a simple directed graph without loops,
$$D(G) = \frac{|E|}{|V| (|V| - 1)}$$

For a simple directed graph that can have loops,
$$D(G) = \frac{|E|}{|V|^2}$$


### Adjacency matrix

Two nodes $v'$ and $v''$ are called **adjacent** if there is an edge from $v'$ to $v''$.

Since for undirected graph, there is no notion of edge direction, the adjacency relation is symmetric for them: $v'$ is adjacent to $v''$ if and only if $v''$ is adjacent to $v'$. This is not necessarily the case for directed graphs.

An **adjacency matrix** of a simple graph $G$ is a matrix $A$ of size $|V| \times |V|$ such that
$$ A_{ij} =
\begin{cases}
1 & \text{there is an edge from {i}-th to {j}-th node} \\
0 & \text{otherwise}
\end{cases} $$

For multigraphs,
$$ A_{ij} = \text{the number of edges from {i}-th to {j}-th node} $$

For simple weighted graphs,
$$ A_{ij} =
\begin{cases}
1 & \text{the weight from an edge from {i}-th to {j}-th node} \\
0 & \text{if there is no edge}
\end{cases} $$

I couldn't find or come up with any meaningful definition of an adjacence matrix for weighted multigraphs.

The adjacency matrices of undirected graphs are always symmetric.

The adjacency matrices of simple graphs always have zeros on the main diagonal.


# Neighbors and degrees

**Neighbors** of node $v$ are nodes that have an edge to or from $v$.

**Ego graph** (or **neighborhood graph**) of node $v$ is a graph that consists of node $v$, its neighbors and all the edges between these nodes.

The **degree** of node $v$ in an undirected graph is the number of edges to/from node $v$.

If the graph is simple, there can be at most one edge between two nodes, so the degree in this case is the number of neighbors.

In directed graph there are two notions of degree:
* **in-degree**: the number of edges going o $v$
* **out-degree**: the number of edges going from $v$

All three degree definitions above are applicable for simple graphs and for multigraphs as well.


# Paths and cycles
A **path** is any sequence $v_0, e_1, v_1, ..., e_n, v_n$ where $v_i$ are nodes, $e_i$ are edges 
and each edge $e_i$ goes from $v_{i-1}$ to $v_i$.

This definition is applicable for both simple graphs and multigraphs as it allows to define
*which* edge was used. Since for simple graphs, there can be at most one edge, the definition
above is equivalent to the following: **path** in a simple graph is any sequence $v_0, ..., v_n$
where $v_i$ are nodes and there is an edge between node $v_{i-1}$ and $v_i$.

**Path length** is the number of edges in it.

An **empty path** of length 0 is a special case where the sequence consists of only a single node.

A **simple path** is a path that visits each node at most once
(except maybe the start and end nodes which are allowed to be the same).

A **cycle** is a path in which the start and end nodes are the same.


## Connectivity and acyclicity
An undirected graph is called
* **connected** if there's a path between any pair of nodes
  * if there's *at least one* path between any pair of nodes
* **acyclic** if there are no cycles in it
  * if there's *at most one* path between any pair of nodes
* a **tree** if it's undirected, connected and acyclic
  * if there's *exactly one* path between any pair of nodes

A directed graph is called (definitions from [Wikipedia](https://en.wikipedia.org/wiki/Connectivity_(graph_theory)))
* **weakly connected** if replacing all of its directed edges with undirected edges produces a connected undirected graph
* **unilaterally connected** (or **semiconnected**) if it contains a path from $a$ to $b$ OR a path from $b$ to $a$
for every pair of nodes $a$, $b$
* **strongly connected** if it contains a path from $a$ to $b$ AND a path from $b$ to $a$
for every pair of nodes $a$, $b$
* * **acyclic** if there are no cycles in it


## Reachability
Node $b$ is said to be **reachable** from node $a$ if there is a path from $a$ to $b$.
* every node is reachable from itself via an empty path, so reachability is a reflexive relation
* if there's path from $a$ to $b$ and path from $b$ to $c$ then concatenating them we get a path from $b$ to $c$,
thus reachability is a transitive relation
* for undirected graphs and strongly connected digraphs it's additionally a symmetric relation, and thus for these graphs
it's an equivalence relation. Equivalence classes are called **connected components**.


## DAGs
**DAG** is a Directed Acyclic Graph.

**Source** node in a DAG is such a node that it has no incoming edges (indegree 0).

**Sink** node in a DAG is such a node that it has no outcoming edges (outdegree 0).

This doesn't seem to be a common terminology, but if there's a single source in a DAG such that every other node is
reachable from it, we will call this node a **root** of the DAG.

Ontology graphs are DAGs, typically rooted. For HPO ontology the root is node HP:0000001 "All".

It's important to remember that nodes in DAG can have more than one path between them, but only in one direction.
In this example there are two paths from $a$ to $f$, but no path from $f$ to $a$ so acyclic property is not violated.
```
a -> b -> c
 \           \> f
  \-> d -> e -> f
```
