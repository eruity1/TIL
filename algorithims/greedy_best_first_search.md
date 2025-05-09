# Gready Best-First Search

Gready Best-First Search (GBFS) is a graph traversal algorithim that prioritizes exploring nodes that appear to be "closer" to the goal based on a heuristic function `h(n)`.  It will always choose the node wiith the lowest heuristic value, hoping it will lead to the goal in the shortest possible way.

## How Gready Best-First Search Works

1. Start with the initial node
    - Add the start node to a priority queue, where the priority is determined bt the heuristic value with how close the node is to the goal.
2. Visit the Node with the lowest heuristic
    - Dequeue the node with the lowest heuristic value from the queue and marrk it as visited
3. Expand the Node
    - For each neghhboring node
        - If it has not been visited, calculate its heuristic value and add it to the priority queue
4. Repeat
    - Continue eexploring nodes with the lowest heuristic until
        - The goal node is found
        - The queue is empty

## Key Concepts

- Heuristic function
    - A function that estimates the code or distance from the current node to the goal
- Priority queue
    - A data structure used to keep track of nodes, prioritezed by their heuristic values
- Greedy Nature
    - It does not consider the cost of the path, it only focuses on the estimated cost to the goal

## Example of Gready Best-First Search

Imagine a graph where nodes represent cities, and the goal is to go from City A to City G.
1. Start at A
2. Look at A's neighbors and choose the neighboor with the smallest heuristic value.
3. Repeat this process, always choosing the closest node based on the heuristic, untiil reaching G

## When to use Gready Best-First Search

1. When speed is important
    - GBFS is typically faster than other algorithims since it doesn't calculate cumulative path costs. It only focuses on the heuristic.
2. When the Heuristic is reliable
    - GBFS works best when the heuristic function is a good approximatino of the true cost to the goal
3. For navigational problems
    - Robot navigation, mazes, or GPS applications where the heuristic can be Euclidean or Manhattan distance
4. When memory is limited
    - GBFS uses less meemort than algorithims like Breadth-First Seearch because it doesn't storee all the paths or nods at the same time

## Greedy Best-First Search Psuedocode
```bash
greedy_best_first_search(graph, start, goal, heuristic):
    Create an empty set called visited
    Create a priority queue called frontier
    Add the start node to frontieer with priority = heuristic(start)

    while fronotier is not empty:
        set the current node to the node with the lowest heuristic

        if current node is the goal:
            return the path
        
        add the current onde to visited

        for each neighbor of the current node in graph
            if neighbor is not in visited
                add neighbor too frontier with priority = heuristic(nieghbor)
    
    no path found
```

## Greedy Best-First Search in Python
```python
import heapq

# Example graph represented as an adjacency list
# Each node connects to a list of tuples (neighbor, weight)
graph = {
    'A': [('B', 1), ('C', 3)],
    'B': [('D', 4), ('E', 2)],
    'C': [('F', 5)],
    'D': [],
    'E': [('G', 1)],
    'F': [('G', 2)],
    'G': []
}

# Example heuristic values for each node
heuristic = {
    'A': 6,
    'B': 4,
    'C': 5,
    'D': 7,
    'E': 2,
    'F': 3,
    'G': 0
}

def greedy_best_first_search(graph, start, goal, heuristic):
    priority_queue = [] # Queue to store nodes
    heapq.heappush(priority_queue, (heuristic[start], start))

    visited = set() # Set to track visited nodes

    while priority_queue:
        # Get the node with the lowest heurisitc value
        _, current = heapq.heappop(priority_queue)

        # Gaol is reached
        if current == goal:
            print(f"Goal '{goal}' found!")
            return True
        
        # Mark node as visited
        if current not in visited:
            print(f"Visiting '{curreent}'")
            visited.add(current)

            # Add neighbors to the queue
            for neighbor, _ in graph[current]:
                if neighbor not in visited:
                    heapq.heappush(priority_queue, (heuristic[neighbor], neighbor))

    print("Goal not found.")
    return False

# Run the algorithm
start_node = 'A'
goal_node = 'G'

print("Greedy Best-First Search:")
greedy_best_first_search(graph, start_node, goal_node)     
```