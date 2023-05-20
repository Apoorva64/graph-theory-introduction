# Graph Theory - Introduction

## What is a Graph?

A graph is a network that helps us visualize relationships between objects. A graph is made up of two things:

1. **Node** - A node is a vertex in a graph. It can represent anything like a person, a place, a city, etc.
2. **Edge** - An edge is a connection between two nodes. It can represent anything like a relationship, a road, etc.

## Why do we use Graphs?

Graphs are used to represent many real-life applications:

1. Social Networks
   In a social network, each person is represented by a node. If two people are friends, there is an edge between them.
   It is easy to find the shortest path between two people using a graph and recommend friends to people.
2. Maps
   In a map, each location is represented by a node. If there is a road between two locations, there is an edge between
   them. It is easy to find the shortest path between two locations using a graph.

## Terminology

1. **Neighbour** - Two nodes are neighbours if there is an edge between them.
2. **Weight** - The weight of an edge is the cost of going from one node to another.
3. **Degree** - The degree of a node is the number of edges connected to it.
4. **Path** - A path is a sequence of nodes connected by edges.
5. **Cycle** - A cycle is a path that starts and ends at the same node.
6. **Connected Graph** - A graph is connected if there is a path between every pair of nodes.
7. **Connected Component** - A connected component of a graph is a subgraph in which every pair of nodes is connected by
   a path.
8. **Disconnected Graph** - A graph is disconnected if there is no path between at least one pair of nodes.
9. **Weighted Graph** - A graph is weighted if each edge has a weight associated with it.
10. **Directed Graph** - A graph is directed if each edge has a direction associated with it.
11. **Undirected Graph** - A graph is undirected if each edge has no direction associated with it.
12. **Acyclic Graph** - A graph is acyclic if it has no cycles.
13. **Cyclic Graph** - A graph is cyclic if it has at least one cycle.
14. **Tree** - A tree is an undirected graph that is connected and acyclic.
15. **Forest** - A forest is an undirected graph that is disconnected and acyclic.
16. **Spanning Tree** - A spanning tree of a graph is a tree that connects all the nodes of the graph.

## Graph Representation

### Defining a Graph interface

#### Defining a Node

```java
public interface Node {
    String getLabel();
}
```

#### Defining an Edge

```java
public interface Edge {
    Node getSource();

    Node getDestination();
}
```

```java
public interface WeightedEdge extends Edge {
    int getWeight();
}
```

```java
public interface DirectedEdge extends Edge {
}
```

```java
public interface UndirectedEdge extends Edge {
}
```

```java
public interface WeightedDirectedEdge extends WeightedEdge, DirectedEdge {
}
```

```java
public interface WeightedUndirectedEdge extends WeightedEdge, UndirectedEdge {
}
```

#### Defining a Graph

```java

import java.util.Iterator;

public interface Graph<EdgeImpl extends Edge, NodeImpl extends Node> {
    void addEdge(EdgeImpl edge);

    void addNode(NodeImpl node);

    void removeEdge(EdgeImpl edge);

    void removeNode(NodeImpl node);

    Iterator<EdgeImpl> getEdges();

    Iterator<NodeImpl> getNodes();

    Iterator<EdgeImpl> getEdges(NodeImpl node);

    Iterator<NodeImpl> getNeighbours(NodeImpl node);

    int getDegree(NodeImpl node);

    int getWeight(EdgeImpl edge);

    int getWeight(NodeImpl source, NodeImpl destination);
}
```
### Graph Representation implementation


We are going to use the following directed graph as an example:

- 4 nodes(A, B, C, D)
- 7 edges(AB, AC, AD, BC, BD, CD, DA)
  Every edge has a weight of `1`.

Graphs are commonly represented in three ways:

1. Adjacency Matrix
   The adjacency matrix is a 2D array of size `V x V` where `V` is the number of vertices in a graph.
   The value of the cell `matrix[i][j]` is the cost of going from node `i` to node `j`. If there is no edge between two
   nodes, the value of the cell is `0`.

   |       | A | B | C | D |
            |-------|---|---|---|---|
   | **A** | 0 | 1 | 1 | 1 |
   | **B** | 0 | 0 | 1 | 1 |
   | **C** | 0 | 0 | 0 | 1 |
   | **D** | 1 | 0 | 0 | 0 |

2. Adjacency List
   The adjacency list is an array of linked lists where each element is a linked list of nodes.
   The index of the array represents a node and the linked list represents the nodes that are connected to it with the
   weight of the edge between them.
   To better understand this, let's look at the adjacency list of the above graph but by replacing the indices with the
   node names.
   ```json
   {
        "A": [["B", 1], ["C", 1], ["D", 1]],
        "B": [["C", 1], ["D", 1]],
        "C": [["D", 1]],
        "D": [["A", 1]]
   }
    ```
3. Edge List
   The edge list is an array of tuples where each tuple represents an edge between two nodes.
   The first element of the tuple is the source node and the second element is weight of the edge between the two nodes
   and the third element is the destination node.
    ```json
    [
          ["A", 1, "B"],
          ["A", 1, "C"],
          ["A", 1, "D"],
          ["B", 1, "C"],
          ["B", 1, "D"],
          ["C", 1, "D"],
          ["D", 1, "A"]
    ]
   ```
   