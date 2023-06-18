## Introduction
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


## Mathematical definitions

A **simple undirected graph** is a pair $(V, E)$ where
* $V$ is a set of **nodes** (also called **vertices**)
* $E$ is a set of **edges** (also called **links**)
    * edges are represented as *unordered* pairs (or sets) of vertices: edge $\{a, b\}$ is the same as edge $\{b, a\}$
    
For **simple directed graph** $E$ contains of *ordered* pairs of vertices: $(a, b)$ and $(b, a)$ are two differente edges. There can be both of them, one of them, or none of them between any pair of nodes.
    
For **(un)directed multigraph** $E$ is a *multiset* instead of *set*, so the same pair can be present more than once.


A **weighted graph** is a triple $(V, E, w)$ where $w: E \rightarrow \mathbb{R}$ is a function that assigns **weight** $w(e)$ to each edge $e \in E$.


The **order** of a graph is the number of its vertices $|V|$.

The **size** of a graph is the number of its edges $E$.


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


### Density of a simple graph
**Graph density** of a simple undirected graph without loops is the ratio between the number of edges it actually has and the number of edges it *can* have:
$$D(G) = \frac{|E|}{\frac{|V| * (|V| - 1)}{2}} = \frac{2 |E|}{|V| (|V| - 1)}$$

For a simple undirected graph that can have loops,
$$D(G) = \frac{2 |E|}{|V| (|V| + 1)}$$

For a simple directed graph without loops,
$$D(G) = \frac{|E|}{|V| (|V| - 1)}$$

For a simple directed graph that can have loops,
$$D(G) = \frac{|E|}{|V|^2}$$