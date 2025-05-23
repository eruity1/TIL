## A (A-Star)*

The A* algorithim is a graph traversal and pathfinding algorithim that fiinds the shortest path between two points.

A* combines two strategies:
1. Greedy Best-First Search: It uses a heuristic to estimate the cost of reaching the goal.
2. Dijkstra's Algorithim: It also accounts for the actual cost of the path taken so far.

By combining the two A* guarentees finding the shortest path, if one exists, while still being efficient.

## How A* works
A* uses the following cost function for each node:
```bash
f(n) = g(n) = h(n)
```
    - f(n): THe total estimated cost of the path through node `n`
    - g(n): The actual cost of the path from the start node to `n`
    - h(n): The heeuristic estimate of the coost from `n` to the goal

1. Initialize
    - Add a start node to a priority queue, where nodes are prioritized by their `f(n)` value.
    - Track visiteed nodes to avoid revisting them,
2. Expand Nodes
     - At each step, pick the node from the priority queue with the lowest `f(n)` value.
     - If this node is the goal, exit the algorithim
3. Update Costs
    - For each unvisitd neighbor of the current node:
        - Calculate `g(n)`, the cost to reach the neighbor from the start)
        - Calculate `h(n)`, heuristic estimate to the goal
        - Update `f(n) = g(n) = h(n)`
        - Id the neighbor is not yeet in the priority queue, add it.
4. Repeat
    - Coontinue expanding nodes until the goal is found or tthe priioority queue is empty

## Key Concepts
1. Heuristic (h(n)):
    - A heuristic is an estimate of the cost to reach the goal. It should be:
        - Admissible: Never overestimates the actual cost to the goal.
        - Consistent: For any two nodes a and b, the heuristic should satisfy: `h(a) ≤ cost(a, b) + h(b)`
    - Examples:
        - Manhattan Distance: For grid-like movement with no diagonals.
        - Euclidean Distance: For spatial paths with diagonal movement.
        - Haversine Formula: For geographical paths.
2. Priority Queue
     - Nodes are prioritized by their f(n) values, ensuring that the most promising node is explored first.
3. Completeness
     - A* is complete, meaning it will find a path if one exists.
4. Optimality
    - A* is optimal, meaning it will find the shortest path if the heuristic is admissible and consistent.

## When to Use A*
1. You Need the Shortest Path
    - A* guarantees finding the optimal path, unlike Greedy Best-First Search, which may not.
2. Heuristic is Reliable
    - A* performs well when you have a good heuristic that accurately estimates the distance to the goal.
3. Pathfinding in Weighted Graphs
     - A* is ideal for graphs with weighted edges (road networks) where the cost to travel between nodes varies.
4. Applications with Spatial Navigation
    - Robotics pathfinding, GPS navigation, and game AI (guiding characters in a game world).
5. When Efficiency is Important:
    - A* is faster than Dijkstra's algorithm because it uses the heuristic to guide the search, avoiding unnecessary exploration.

## A* PsuedoCode
```bash
def a_star(graph, start, goal, heuristic):
    Create an empty set to track visited nodes
    Create a priority queue and add the start to it
    Create a dictionary called gScore, where each node's cost is infinity
    Set gScore[start] = 0
    Create a dictionary called fScore, where each node's estimated cost is infinity
    Set fScore[start] = heuristic(start, goal)
    Create a dictionary called cameFrom to track the shortest path

    While the priority queue is not empty:
        current = node in priority queue with the lowest fScore value

        If current == goal:
            return reconstruct_path(cameFrom, current)

        Remove current from priority queue
        Add current to visited

        For each neighbor of current in graph:
            If neighbor is in visited:
                continue

            tentative_gScore = gScore[current] + cost(current, neighbor)

            If neighbor is not in priority queue:
                Add neighbor to priority queue

            If tentative_gScore >= gScore[neighbor]:
                continue since this is not the better path

            # This path is the best until now
            cameFrom[neighbor] = current
            gScore[neighbor] = tentative_gScore
            fScore[neighbor] = gScore[neighbor] + heuristic(neighbor, goal)

    return "No Path Found"

reconstruct_path(cameFrom, current):
    path = [current]
    While current in cameFrom:
        current = cameFrom[current]
        path.prepend(current)
    return path

```

## A* in Python
```python
import heapq

# grid (0 is walkable, 1 is an obstacle)
grid = [
    [0, 0, 0, 1, 0],
    [0, 1, 0, 1, 0],
    [0, 1, 0, 0, 0],
    [1, 0, 1, 1, 0],
    [0, 0, 0, 0, 0]
]

# Manhattan Distance
def heuristic(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

def a_star(grid, start, goal):
    rows, cols = len(grid), len(grid[0])
    open_set = []
    heapq.heappush(open_set, (0, start))
    came_from = {}

    g_score = {start: 0}
    f_score = {start: heuristic(start, goal)}

    while open_set:
        # Get node with the lowest f_score
        _, current = heapq.heappop(open_set)

        if current == goal:
            return reconstruct_path(came_from, current)
        
        for dx, dy in [(-1, 0), (1, 0), (0, -1), (0, 1)]: #neighboring directions
            neighbor = (current[0] + dx, current[1] + dy)

            if 0 <= neighbor[0] < rows and 0 <= neighbor[1] < cols and grid[neighbor[0]][neighbor[1]] == 0:
                tentative_g_score = g_score[current] + 1 #uniform cost for movement

                if neighbor not in g_score or tentative_g_score < g_score[neighbor]:
                    came_from[neighbor] = current
                    g_score[neighbor] = tentative_g_score
                    f_score[neighbor] = tentative_g_score + heuristic(neighbor, goal)
                    heapq.heappush(open_set, (f_score[neighbor], neighbor))
    
    # If no path is found
    return None

def reconstruct_path(came_from, current):
    path = [current]
    whiile current in came_from:
        current = came_from[current]
        path.append(current)
    path.reverse()
    return path

start = (0, 0)
goal = (4, 4)

path = a_star(grid, start, goal)
if path:
    print("Path found:", path)
else:
    print("No path found.")
```

Output:
```bash
Path found: [(0, 0), (0, 1), (0, 2), (1, 2), (2, 2), (2, 3), (2, 4), (3, 4), (4, 4)]
```

## A* in Ruby
```ruby
require 'set'

GRID = [
  [0, 0, 0, 1, 0],
  [0, 1, 0, 1, 0],
  [0, 1, 0, 0, 0],
  [1, 0, 1, 1, 0],
  [0, 0, 0, 0, 0]
]

# Manhattan distance
def heuristic(a, b)
  (a[0] - b[0]).abs + (a[1] - b[1]).abs
end

def neighbors(pos, grid)
  x, y = pos
  deltas = [[-1,0],[1,0],[0,-1],[0,1]]
  deltas.map { |dx, dy| [x+dx, y+dy] }
        .select { |nx, ny| nx.between?(0, grid.size-1) && ny.between?(0, grid[0].size-1) && grid[nx][ny] == 0 }
end

def reconstruct_path(came_from, current)
  path = [current]
  while came_from[current]
    current = came_from[current]
    path << current
  end
  path.reverse
end

def a_star(grid, start, goal)
  open_set = [[heuristic(start, goal), start]]
  g_score = Hash.new(Float::INFINITY)
  g_score[start] = 0
  f_score = Hash.new(Float::INFINITY)
  f_score[start] = heuristic(start, goal)
  came_from = {}

  visited = Set.new

  until open_set.empty?
    open_set.sort_by!(&:first)
    _, current = open_set.shift

    return reconstruct_path(came_from, current) if current == goal

    visited.add(current)

    neighbors(current, grid).each do |neighbor|
      next if visited.include?(neighbor)
      tentative_g = g_score[current] + 1
      if tentative_g < g_score[neighbor]
        came_from[neighbor] = current
        g_score[neighbor] = tentative_g
        f_score[neighbor] = tentative_g + heuristic(neighbor, goal)
        open_set << [f_score[neighbor], neighbor] unless open_set.any? { |_, n| n == neighbor }
      end
    end
  end

  nil
end

start = [0, 0]
goal = [4, 4]
path = a_star(GRID, start, goal)
if path
  puts "Path found: #{path.inspect}"
else
  puts "No path found."
end
```

Output:
```bash
Path found: [[0, 0], [0, 1], [0, 2], [1, 2], [2, 2], [2, 3], [2, 4], [3, 4], [4, 4]]
```