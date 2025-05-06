# Depth First Search

Depth First Search (DFS) is a graph traversal algorithim that explores as far as possible along each branch before backtracking.
DFS can be implimented using:
 - A stack, for an iterative implmentation
 - Recursion 

It uses these steps:
1. Start at the Root Node:
    - Select a starting node (the root node).
2. Visit the Node:
    - Mark the node as visited
    - Process the node (perform some operaion on it)
3. Explore Neighbors:
    - For each unvisited neight of the current node, repeating the process (1 - 3)
4. Backtrack:
    - If a node has no unvisited. neighbors, backtrack to the previous node and continue with its remaining neighbors.

## Example
```bash
    A
   / \
  B   C
 / \
D   E
```
- Starting at `A`, DFS would traverse to `B`, then to `D`, backtrack to `B`, visit `E`, and finally explore `C`.

## When to use DFS
DFS is particularly useful in scenarios where you need to explore all possible paths or deeply nested structures. Here are some common use cases:
1. Pathfinding Problems
    - Finding a path between two nodes in a maze or a graph.
    - Checking if a graph is connected.
2. Search Problem
    - Finding solutions in puzzles where you need to explore all possible configurations
3. Topological Sorting
    - Useful in Directed Acyclic Graphs for tasks like scheduling
4. Cycle Detection
    - Checking if a graph contains cycles
5. Connected Components
    - Identifying all connected components in a graph
6. Tree Traversal
    - Traversing trees in preorder, inorder, or postorder

## Depth First Search Pseudocode
```bash
# Recursive DFS
DFS(graph, node, visited)
  if node is not in visited
    Mark node as visited
    Process the node (e.g., print it or store it)
    for each neighbor in graph[node]
      DFS(graph, neighbor, visited)

# Iterative DFS 
DFS(graph, start)
  Create an empty set called visited
  Create a stack and push the start node onto it

  while stack is not empty
    node = stack.pop()
    if node is not in visited
      Mark node as visited
      Process the node (e.g., print it or store it)
      Push all unvisited neighbors of node onto the stack
```

## Depth First Search in Ruby
```ruby
require 'set'

graph = {
  'A' => ['B', 'C'],
  'B' => ['D', 'E'],
  'C' => ['F', 'G'],
  'D' => [],
  'E' => [],
  'F' => [],
  'G' => []
}

# Recursive DFS function
def dfs_recursive(graph, node, visited = Set.new)
  return if visited.include?(node)

  print "#{node} " # Processing the node
  visited.add(node)

  graph[node].each do |neighbor|
    dfs_recursive(graph, neighbor, visited)
  end
end

# Iterative DFS function
def dfs_iterative(graph, start)
  visited = Set.new
  stack = [start]

  until stack.empty?
    node = stack.pop
    next if visited.include?(node)

    print "#{node} " # Processing the node
    visited.add(node)

    stack.concat(graph[node].reverse)
  end
end
```

## Depth First Search in Python
```python
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F', 'G'],
    'D': [],
    'E': [],
    'F': [],
    'G': []
}

# Recursive DFS function
def dfs_recursive(graph, node, visited):
    if node not in visited:
        print(node, end=' ')  # Processing the node
        visited.add(node)
        for neighbor in graph[node]:
            dfs_recursive(graph, neighbor, visited)

# Iterative DFS function
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    
    while stack:
        node = stack.pop()
        if node not in visited:
            print(node, end=' ')  # Processing the node
            visited.add(node)
  
            stack.extend(reversed(graph[node]))
```

## Depth First Search in JavaScript
```javascript
const graph = {
  A: ['B', 'C'],
  B: ['D', 'E'],
  C: ['F', 'G'],
  D: [],
  E: [],
  F: [],
  G: []
};

// Recursive DFS function
function dfsRecursive(graph, node, visited = new Set()) {
  if (visited.has(node)) return;

  console.log(node); // Processing the node
  visited.add(node);

  for (const neighbor of graph[node]) {
    dfsRecursive(graph, neighbor, visited);
  }
}

// Iterative DFS function
function dfsIterative(graph, start) {
  const visited = new Set();
  const stack = [start];

  while (stack.length > 0) {
    const node = stack.pop();
    if (visited.has(node)) continue;

    console.log(node); // Processing the node
    visited.add(node);

    // Loop over neighbors in reverse
    for (let i = graph[node].length - 1; i >= 0; i--) {
      const neighbor = graph[node][i];
      stack.push(neighbor);
    }
  }
}
```