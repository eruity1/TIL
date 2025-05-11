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

    While openSet is not empty:
        current = node in openSet with the lowest fScore value

        If current == goal:
            Return reconstruct_path(cameFrom, current)

        Remove current from openSet
        Add current to closedSet

        For each neighbor of current in graph:
            If neighbor is in closedSet:
                continue

            tentative_gScore = gScore[current] + cost(current, neighbor)

            If neighbor is not in openSet:
                Add neighbor to openSet

            If tentative_gScore >= gScore[neighbor]:
                continue since this is not the betteer path

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