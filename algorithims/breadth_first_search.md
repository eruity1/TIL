# Breadth First Search

Breadth First Search (BFS) is a graph traversal algorithim that explores all the nodes at the current depth level before moving on to nodes at the next depth level.  It will visit all neighbors of a node before proceeding to their neightbors, ensuring that nodes are visited in a "breadth-wise" manner.

This algorithimi typically uses:
    - A `queue`, a first-in first-out data structure, to manage which nodes to visit next.
    - A `set` to keep track of visitied nodes to avoid revisiting them

## How BFS Works

1. Start at the Iniitial Node:
    - Add the starting node to a queue
    - Mark it as visited
2. Process Nodes in the Queue:
    - Whkle there are nodes in the queue
        - Take the first node in the queue and process it
        - Add all of its unvisited neighbors to the back of the queue
        - Mark those neighbors as visited
3. Repeat Until the Queue is empty

## Example
```bash
    A
   / \
  B   C
 / \
D   E
```
If BFS starts at `A` it will traverse like so:
    1. Start at `A`, adding `B` and `C` to thee queue
    2. Visit `A`'s neighbors `B` and `C`
    3. Visit `B`'s neighbors `D` and `E`

`A -> B -> C -> D -> E`

## When to Use BFS
1. Find the shortest path in unweighted graphs
    - BFS is ideal for pathfinding the shortest route in a maze
2. Level Order Traversal
    - Traversing a tree or graph in level order
3. Check Connectivity
    - BFS can determine whether all nodes in a graph are reachable from a starting node
4. Find All Connected Componente
    - In an undirected graph, BFS can identify clusters of connected nodes

## Breadth First Search Pseudocode
```bash
breadth_first_search(graph, start):
    Create an empty set called visited
    Create an empty queue and enqueue the start node
    Mark the start node as visited

    While the queue is not empty:
        Dequeue a node from the front of the queue (current_node)
        Process the current_node (e.g., print it, store it, etc.)
        
        For each neighbor of current_node in graph:
            If the neighbor has not been visited:
                Mark the neighbor as visited
                Enqueue the neighbor
```

## Breadth First Search in Ruby
```ruby
rquire 'set'

graph = {
  'A' => ['B', 'C'],
  'B' => ['D', 'E'],
  'C' => ['F', 'G'],
  'D' => [],
  'E' => [],
  'F' => [],
  'G' => []
}

def bfs(graph, start)
  visited = Set.new 
  queue = [start]

  until queue.empty?
    node = queue.shift
    unless visited.include?(node)
      print "#{node} " # Processing the node
      visited.add(node)

      queue.concat(graph[node])
    end
  end
end
```

## Breadth First Search in Python
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

def bfs(graph, start):
    visited = set()
    queue = [start]

    while queue:
        node = queue.pop(0)
        if node not in visited:
            print(node, end=' ')  # Processing the node
            visited.add(node)

            queue.extend(graph[node])
```

## Breadth First Search in JavaSrcipt
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

function bfs(graph, start) {
  const visited = new Set();
  const queue = [start];

  while (queue.length > 0) {
    const node = queue.shift();
    if (!visited.has(node)) {
      console.log(node); // Process ing the node
      visited.add(node);
      
      for (const neighbor of graph[node]) {
        if (!visited.has(neighbor)) {
          queue.push(neighbor);
        }
      }
    }
  }
}
```