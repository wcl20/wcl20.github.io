---
layout: post
title: Breadth First Search
---

## Problem
Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root and explores all of the neighbour nodes at the present depth prior to moving on to the nodes at the next depth level.

Unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array.

Graph
```python
class Graph:
    def __init__(self, nodes):
        # Create a list to store neighbours for each node
        self.nodes = { node: [] for node in nodes }

    def addEdge(self, edge):
        # Get nodes connected by edge
        n1, n2 = edge
        # Undirected graph
        self.nodes[n1].append(n2)
        self.nodes[n2].append(n1)
```

## Solution

```python
def breadthFirstSearch(graph: Graph, start: int):
    # Create list of visited bool to avoid cycles
    visited = [False] * len(graph.nodes)
    # Create a queue
    queue = []
    # Append start node to queue
    queue.append(start)
    # Mark start node as visited
    visited[start] = True
    # While queue is not empty ...
    while queue:
        # Get first item in queue
        node = queue.pop(0)
        # For each neighbour of the node ...
        for neighbour in graph.nodes[node]:
            # Visit later if not visited
            if not visited[neighbour]:
                queue.append(neighbour)
                # Mark neighbour as visited
                visited[neighbour] = True
```

## Variations

Variation 1: Find shortest distance to all nodes using BFS. Returns shortest distance to each node from $start$.

```python
def breadthFirstSearch(graph: Graph, start: int) -> List[int]:
    # Create list of visited bool to avoid cycles
    visited = [False] * len(graph.nodes)
    # Create a list to store distances (-1 if node is unreachable)
    distances = [-1] * len(graph.nodes)
    # Create a queue
    queue = []
    # Append start node to queue
    queue.append(start)
    # Append special character to indicate end of a layer
    queue.append(-1)
    # Mark start node as visited
    visited[start] = True
    # Shortest distance to start is 0
    distances[start] = 0
    # Current layer
    distance = 1
    # While queue is not empty ...
    while queue:
        # Get first item in queue
        node = queue.pop(0)
        # Special character means end of a layer
        if node == -1:
            # Increment current layer
            distance += 1
            # Append special character to indicate end of a layer
            if queue:
                queue.append(-1)
        else:
            # For each neighbour of the node ...
            for neighbour in graph.nodes[node]:
                # Visit later if not visited
                if not visited[neighbour]:
                    queue.append(neighbour)
                    # Mark neighbour as visited
                    visited[neighbour] = True
                    # Shortest distance from $start$
                    distances[neighbour] = distance
    return distances      
```

Variation 2: BFS in 2D Matrix
```python
def breadthFirstSearch(matrix: List[List[int]], start: (int, int)):
    # Get number of rows
    m = len(matrix)
    # Get number of columns
    n = len(matrix[0])
    # Create matrix of visited bool to avoid cycles
    visited = [[False for _ in range(n)] for _ in range(m)]
    # Create a queue
    queue = []
    # Append start node to queue
    queue.append(start)
    # While queue is not empty ...
    while queue:
        # Get first item in queue
        x, y = queue.pop(0)
        # Check x, y is in bound and not visited
        if m <= x < 0 or n <= y < 0 or visited[x][y]:
            continue
        # Mark node as visited
        visited[x][y] = True
        # Visit neighbour nodes in $3 \times 3$ window
        for i in range(x - 1, x + 2):
            for j in range(y - 1, y + 2):
                queue.append((i, j))   
```
