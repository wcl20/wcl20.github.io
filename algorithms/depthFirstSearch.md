---
layout: post
title: Depth First Search
---

## Problem
Depth First Search (DFS) algorithm traverses a graph in a depthward motion and uses a stack to remember to get the next vertex to start a search, when a dead end occurs in any iteration.

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

Method 1: Iterative Implementation using stack
```python
def depthFirstSearch(graph: Graph, start: int):
    # Create list of visited bool to avoid cycles
    visited = [False] * len(graph.nodes)
    # Create a stack
    stack = []
    # Append start node to stack
    stack.append(start)
    # Mark start node as visited
    visited[start] = True
    # While stack is not empty ...
    while stack:
        # Get item in stack
        node = stack.pop()
        # For each neighbour of the node ...
        for neighbour in graph.nodes[node]:
            # Visit later if not visited
            if not visited[neighbour]:
                stack.append(neighbour)
                # Mark neighbour as visited
                visited[neighbour] = True
```

Method 2: Recursive Approach
```python
def depthFirstSearch(graph: Graph, start: int):
    # Create list of visited bool to avoid cycles
    visited = [False] * len(graph.nodes)
    # Recursive method
    depthFirstSearchHelper(graph, start, visited)

def depthFirstSearchHelper(graph: Graph, node: int, visited: List[bool]):
    # Mark node as visited
    visited[node] = True
    # For each neighbour of the node ...
    for neighbour in graph.nodes[node]:
        # Visit later is not visited
        if not visited[neighbour]:
            # Mark neighbour as visited
            visited[neighbour] = True
            depthFirstSearchHelper(graph, neighbour, visited)
```

## Variations

Variation 1: DFS in 2D Matrix
```python
def depthFirstSearch(matrix: List[List[int]], start: (int, int)):
    # Get number of rows
    m = len(matrix)
    # Get number of columns
    n = len(matrix[0])
    # Create matrix of visited bool to avoid cycles
    visited = [[False for _ in range(n)] for _ in range(m)]
    # Create a stack
    stack = []
    # Append start node to stack
    stack.append(start)
    # While stack is not empty ...
    while stack:
        # Get first item in stack
        x, y = stack.pop()
        # Check x, y is in bound and not visited
        if m <= x or x < 0 or n <= y or y < 0 or visited[x][y]:
            continue
        # Mark node as visited
        visited[x][y] = True
        # Visit neighbour nodes in $3 \times 3$ window
        for i in range(x - 1, x + 2):
            for j in range(y - 1, y + 2):
                stack.append((i, j))   
```
