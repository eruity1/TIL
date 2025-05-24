# Minimax

Minimax is a recursive algorithm used in decision making and game theory to determine the optimal movee for a player, assuming the opponent also plays optimally. It's widely used in two-player, turn-based games like chess, tic-tac-toe or checkers.
- Maximaizing player: Tries to maximize the score.
- Minimizing player: Tries to minimize the score.

# Depth-Limited Minimax

A depth-limited minimax algorithm is a variant where the recursion is stopped after a certain number of moves. Instead of searching all the ways to terminal game states it uses an evaluation function to estimate the desirability of non-terminal positions when the depth limit is reached.

## Why use Depth-Limit?

1. Performance: In complex games, like chess, the number of possible game states grows exponentially.
2. Speed: Limiting depth means you can make decisions quickly, which is important for real-time or resource-constrained environments.

## How Does Depth-Limited Minimax Work?

1. Recursion: At each node (game state), alternate between maximizing and minimizing.
2. Depth limit: If the maximum depth is reached or the game is over, return the evaluation of the current state.
3. Evaluation function: When stopping early, use a heuristic to estimate how favorable the current state is for the maximizing player.
4. Back up values: Each node’s value is determined by the best value it can force (max for maximizing, min for minimizing).

## When Should you use Depth-Limited Minimax?
1. Turn-based, two-player, zero-sum games
2. When the game tree it too large to search completely
3. When you need a move quickly
4. When you can design a meaningful evaluation function for intermediate game states

## Pseudocode
```bash
def minimax(node, depth, maximizingPlayer):
    if depth == 0 or node is a terminal node:
        return evaluate(node)

    if maximizingPlayer:
        maxEval = -infinity
        for each child of node:
            eval = minimax(child, depth - 1, false)
            maxEval = max(maxEval, eval)
        return maxEval
    else:
        minEval = +infinity
        for each child of node:
            eval = minimax(child, depth - 1, true)
            minEval = min(minEval, eval)
        return minEval
```
