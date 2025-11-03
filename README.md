# 8-Puzzle Solver using BFS

## Problem Statement

Solve the classic **8-puzzle problem** using **Breadth First Search (BFS)**.  
The puzzle is represented as a 3x3 grid containing numbers `1-8` and a blank space (`0`).  
The objective is to transform a given start state into the goal state by sliding the tiles.

---

## Approach

- Use a **queue** to explore the state space in a level-wise manner (BFS).
- At every state:
  - Find the position of the empty tile.
  - Generate all valid states by moving the tile (up, down, left, right).
  - Enqueue each new unvisited state.
- Stop when the goal state is found.

---

## Implementation Details

- Each state is a `vector<vector<int>>` (3x3 matrix).
- `std::queue` stores the current state frontier.
- `std::set` is used to avoid revisiting states.
- `findEmptyBox()` locates the position of the empty tile (0).
- The directions are defined as `(dx, dy)` pairs for moving the blank tile.

---

## Time and Space Complexity

### Time Complexity:
- **Worst-case:** O(9!)  
  - Each state is unique (up to 9! total).
  - BFS explores each state only once.
  - It ensures shortest path but visits many states.

### Space Complexity:
- O(9!) for the visited set and queue.
  - Each state is stored in memory.

---

## Use Cases
- Finds the shortest path to the goal (unlike DFS).
- Good for solving problems with minimal steps required.
- Demonstrates uninformed search algorithm in AI.

# 8-Puzzle Solver using DFS

## Problem Statement

Implement a program that solves the 8-puzzle problem using **Depth First Search (DFS)**.  
The puzzle consists of a 3x3 grid with tiles numbered from 1 to 8 and one empty space (0).  
The goal is to move the tiles to reach the goal state.

---

## Approach

- Use a **stack** for DFS traversal.
- At each state:
  - Locate the blank (0) tile.
  - Generate all valid moves (up, down, left, right).
  - Push each new state onto the stack if it hasn’t been visited.
- Continue until the goal state is reached or all states are exhausted.

---

## Implementation Details

- The puzzle state is stored as a `vector<vector<int>>`.
- We use a `set` to track visited states to avoid cycles.
- Each move swaps the blank tile with one of its neighbors.
- The `dfs()` function performs the core search logic.

---


## Time and Space Complexity

### Time Complexity:
- **Worst-case:** O((9!)²)  
  - Each state can lead to up to 4 moves.
  - Total possible states = 9! = 362,880.
  - In DFS, due to recursion and lack of optimal pruning, worst-case exploration can be exponential.

### Space Complexity:
- O(9!) for the visited set.
- O(H) for recursion stack in the worst-case path depth H (up to 9 levels deep).

---

## Use Cases
- Useful for understanding how uninformed search algorithms work.
- Demonstrates limitations of DFS (e.g., may not find shortest path, may go deep unnecessarily).
- Forms the basis for solving AI problems with state-space search.

# 8-Puzzle Solver using Greedy Best-First Search

## Problem Statement
The program solves the 8-puzzle problem using the **Greedy Best-First Search (GBFS)** algorithm with the **misplaced tiles heuristic**.  
It starts from an initial puzzle configuration and tries to reach the goal configuration by prioritizing states with fewer misplaced tiles.

---

## Approach
1. **Representation**:  
   - Puzzle is stored as a 3×3 matrix with `0` representing the empty space.
2. **Heuristic Function**:  
   - Counts the number of tiles that are not in their goal position (`misplaced tiles`).
3. **Greedy Best-First Search**:  
   - Maintains a priority queue sorted by heuristic value.
   - Expands the state with the smallest heuristic score.
4. **State Expansion**:  
   - Moves the empty space up, down, left, or right to generate new states.
5. **Cycle Prevention**:  
   - Uses a `visited` set to avoid revisiting the same state.

---

## Implementation Details
- **`print_board`**: Displays the current puzzle configuration in grid format.
- **`isGoal`**: Compares the current puzzle state with the goal state.
- **`findEmptyBox`**: Finds the position of the empty tile (`0`) in the puzzle.
- **`misplaced_tiles`**: Calculates the number of tiles out of place, ignoring the empty tile.
- **`boardToString`**: Converts the 2D board into a string for use in the visited set.
- **`greedyBestFirst`**:
  - Uses a **priority queue** to store states ordered by heuristic value.
  - Pops the best state, checks for goal, and generates valid moves.
  - Skips already visited states to prevent infinite loops.
- **`main`**:
  - Defines the initial and goal states.
  - Prints the starting state.
  - Calls `greedyBestFirst` to attempt solving.


## Time Complexity
- **Worst case**: \( O(b^d) \)  
  where:
  - \( b \) = branching factor (up to 4 for the 8-puzzle)  
  - \( d \) = depth of the shallowest goal node  
- GBFS may explore many nodes due to its lack of optimality guarantees.

## Space Complexity
- **O(n)** where n is the number of unique states stored in memory (visited set + priority queue).

---

## Use Cases
- Educational demonstration of heuristic search.
- Understanding strengths and weaknesses of GBFS.
- Introductory AI assignments for search algorithms.

---

## Limitations
- **Not Optimal**: May find a suboptimal path.
- **Not Complete**: May fail to find a solution even when one exists (depends on heuristic).
- **Performance**: Can still explore many unnecessary states for complex puzzles.
- **Heuristic Weakness**: Misplaced tiles heuristic doesn't consider distance, so it's less informed than Manhattan distance.

# 8-Puzzle Solver using Hill Climbing

## Problem Statement
This program solves the 8-puzzle problem using the **Hill Climbing** search algorithm with the **misplaced tiles heuristic**.  
The algorithm starts from an initial configuration and repeatedly moves to a neighbor with a lower heuristic value, stopping when no improvement is possible.

---

## Approach
1. **Representation**:  
   - The puzzle is stored as a 3×3 matrix, with `0` representing the empty space.
2. **Heuristic Function**:  
   - Counts the number of tiles not in their correct position (ignores the empty tile).
3. **Hill Climbing Search**:  
   - At each step, evaluates all possible moves of the empty tile.
   - Selects the neighbor with the smallest heuristic value.
4. **Termination Conditions**:  
   - Goal state reached.
   - No neighbor has a lower heuristic value (local maximum/plateau).

---

## Implementation Details
- **`print_board`**: Prints the current puzzle board state.
- **`isGoal`**: Checks if the current state matches the goal state.
- **`findEmptyBox`**: Finds coordinates of the empty tile (`0`).
- **`misplaced_tiles`**: Calculates heuristic (number of misplaced tiles).
- **`get_neighbors`**: Generates all possible states by moving the empty tile in up to 4 directions.
- **`hillClimbing`**:
  - Keeps track of the current state and its heuristic.
  - Selects the neighbor with the lowest heuristic.
  - Stops if no improvement is possible.
- **`main`**:
  - Defines start and goal states.
  - Calls `hillClimbing` to solve the puzzle.

---
## Time Complexity
- **Worst case**: \( O(b \times d) \)  
  where:
  - \( b \) = branching factor (up to 4 moves)  
  - \( d \) = number of steps taken until termination.
- Typically fast but may terminate prematurely.

## Space Complexity
- **O(1)** additional space (only current state and neighbors stored at each step).

---

## Use Cases
- Demonstrating the limitations of local search algorithms.
- Educational purposes for AI search methods.
- Comparing performance with other heuristics (e.g., Manhattan distance).

---

## Limitations
- **Local Optima**: Can get stuck in a local minimum.
- **Plateaus**: May stop if all neighbors have equal heuristic values.
- **No Backtracking**: Once stuck, it does not explore alternative paths.
- **Not Optimal**: May find a solution that is not the shortest.











# Magic Square Generator

## Problem Statement
Generate an *n x n* magic square—a square arrangement of numbers where the sums of numbers in each row, column, and diagonal are all equal. The program supports all valid sizes of *n* `(n ≥ 3, n ≠ 2)`.

---
## Approach
The solution uses different algorithms based on the parity of *n*:

- **Odd n:** Uses the `Siamese method (de la Loubere’s method)`, placing numbers sequentially with specific upward-right movement and wrap-around.
- **Doubly Even n (n divisible by 4):** Fills the square sequentially, then inverts certain positions based on a fixed pattern.
- **Singly Even n (even but not divisible by 4):** Divides the square into four quadrants filled with smaller odd-sized magic squares, then performs swaps in specific columns to fix the magic property.

Each method ensures the magic constant  `M = n * n² + 1` is maintained.

---
## Implementation Details
- The program reads input *n*.
- Validates input (n ≥ 3 and n ≠ 2).
- Calls the appropriate generation function based on *n*’s parity.
- Prints the generated magic square formatted neatly.
- Outputs the magic constant for verification.

---


## Time and Space Complexity

**Time Complexity:** O(n²) — Each method fills the n x n matrix once or twice.

**Space Complexity:** O(n²) — The square matrix stores n² integers.

---
## Use Cases
- Mathematical recreation and education.
- Generating magic squares for puzzles and games.
- Demonstrating combinatorial and parity-based algorithms.
- Teaching different algorithmic techniques for special cases.






# Tic-Tac-Toe Rule Based Implementation

## Problem Statement

Implement a **Tic-Tac-Toe** game where a human plays against an AI.  
The AI uses a heuristic-based strategy to decide moves and can play as either **X** (first player) or **O** (second player).  
The board is a 3x3 grid with positions numbered 1 to 9.

---

## Approach

- Represent the board as a vector of integers (size 10, index 1-9 used).
- Each cell holds:
  - `2` for empty
  - `3` for X
  - `5` for O  
  (Using prime numbers allows quick win detection via multiplication.)
- Track turns and alternate moves between human and AI.
- AI decision logic:
  - Attempt to win if possible.
  - Block opponent’s immediate winning moves.
  - Take center or corners as strategic moves.
  - Follow a heuristic plan depending on the turn number.
- The game ends when a player wins or all squares are filled (draw).

---

## Implementation Details

- `printBoard()` displays the current board state.
- `Go(int n)` places a move on the board if the cell is empty.
- `Posswin(int player)` checks if `player` can win on the next move.
- `checkWinner()` evaluates if there is a winner by checking all winning lines.
- `Make2()` helps the AI select strategic positions such as center or edges.
- `humanMove()` prompts and validates user input.
- `aiMove()` applies the AI heuristic logic to select moves.
- The main loop alternates turns, printing the board and checking for a winner after each move.

---

## Time and Space Complexity

- **Time Complexity:** O(1) per move — constant checks of 8 winning lines and up to 9 board positions.
- **Space Complexity:** O(1) — fixed-size board and auxiliary variables only.

---

## Use Cases

- Play Tic-Tac-Toe against a simple AI with basic strategic thinking.
- Demonstrates prime number technique for efficient win detection.
- Serves as a base for learning game AI heuristics.
- Can be extended to more advanced AI algorithms (minimax, alpha-beta pruning).

---

## Limitations

- Uses simple heuristics, not guaranteed optimal.
- Limited lookahead, no deep strategy.
- Fixed move rules can be predictable.
- No learning or adaptation.
- Detects draws only when board is full



# Tic-Tac-Toe with Magic Square Logic AI

## Problem Statement

Implement a **Tic-Tac-Toe** game where a human player competes against an AI opponent that leverages the mathematical properties of a **magic square** to make strategic decisions.  
The board is a 3x3 grid numbered 1 to 9, with each position mapped to a unique number in a magic square.  
The AI uses sums of 15 (a key property of the magic square) to detect winning moves and block the opponent effectively.  
The AI can play either as **X** (going first) or **O** (going second), based on user choice.

---

## Approach

- Represent the Tic-Tac-Toe board as a vector of size 10 (indexing positions 1 to 9 for convenience).  
- Each board position can hold:
  - `2` for empty,
  - `3` for X,
  - `5` for O.
- Use a predefined **magic square mapping** array to translate board positions to magic numbers:
    - Position: 1 2 3 4 5 6 7 8 9
    - Magic #: 8, 3, 4, 1, 5, 9, 6, 7, 2


- Track player moves by storing their chosen magic numbers.
- Detect possible winning or blocking moves by checking pairs of moves whose sums with a missing third number equal 15.
- On each AI turn:
- Try to win if possible.
- Block the opponent's winning move.
- Otherwise, choose the first available empty position.
- Determine the winner by checking if any combination of three magic numbers sums exactly to 15.

---

## Implementation Details

- **Board Representation:**  
A `vector<int>` of size 10, where indices 1 through 9 correspond to the board cells. Each cell holds 2 (empty), 3 (X), or 5 (O).

- **Magic Square Mapping:**  
`magicMap[10] = {0, 8, 3, 4, 1, 5, 9, 6, 7, 2};`  
Maps board indices to their magic square numbers.

- **Move Processing:**  
- `Go(int n)`: Marks the move at position `n` if empty and increments turn count.
- `getPlayerMoves(int player)`: Returns a vector of magic numbers for all positions occupied by the given player.
- `possWinMagic(int player)`: Checks if the player can win in the next move by looking for pairs summing to 15 minus the needed number; returns winning move position or 0 if none.
- `checkWinner()`: Checks if either player has a winning triple summing to 15.

- **Human Input:**  
Prompts for move until a valid, empty position is chosen.

- **AI Logic:**  
Uses magic square sums to find winning/blocking moves; otherwise, picks the first available spot.

- **Game Loop:**  
Alternates between AI and human moves, printing the board and checking for winners or draw.

## Time and Space Complexity

- **Time Complexity:** O(1) per move  
The AI and winner checks perform fixed operations over a small, constant-sized board and precomputed combinations.

- **Space Complexity:** O(1)  
Uses a fixed-size vector and arrays; no dynamic memory grows with input size.

---

## Use Cases
- Play Tic-Tac-Toe against an AI that uses mathematical properties (magic squares) to make optimal moves.
- Demonstrate how magic squares can simplify game logic and win detection.
- Educational example of integrating mathematical concepts into game AI.
- Foundation for expanding to more complex game AI or incorporating alternative board evaluation techniques.

---

## Limitations

- Better move detection but still one-move lookahead.
- No full game-tree search or advanced planning.
- Only detects draws at game end.
- Fixed symbol mapping limits flexibility.
- Magic square method only works for 3x3 Tic-Tac-Toe.












# Tic-Tac-Toe AI using Heuristic Board Evaluation

## Problem Statement
Build a Tic-Tac-Toe game where a human plays against an AI. The AI uses a heuristic evaluation function to choose the best move on each turn, aiming to maximize its chances of winning or blocking the opponent.

## Approach
- The game board is represented as a vector with values representing empty, X, or O.
- The AI evaluates each empty square based on:
  - Whether it’s center, corner, or edge (positional advantage).
  - The potential to complete or block winning lines (rows, columns, diagonals).
- Scores for each square are calculated by summing weights based on these criteria.
- The AI picks the move with the highest evaluation score.
- The game loops with alternating turns until a winner is found or the board is full.

## Implementation Details
- Board uses integers: `2` for empty, `3` for X, and `5` for O.
- Winning lines are predefined sets of indices.
- `evaluateSquare()` assigns scores based on position and line potential.
- AI selects the best scoring square each turn (`chooseBestMoveEval()`).
- Human input is validated for legality.
- The game checks for winner after every move using multiplication logic.
- The board is printed after every move with current markings.

## Time and Space Complexity

**Time Complexity:**  
- Each AI move evaluates up to 9 squares, checking 8 winning lines each.  
- Overall O(72) per AI turn (constant time).

**Space Complexity:**  
- O(1) extra space beyond fixed board and predefined winning lines.

## Use Cases
- Simple Tic-Tac-Toe AI for beginners.
- Demonstrates heuristic evaluation in games.
- Useful for understanding scoring strategies without deep search.
- Educational example of AI decision-making in turn-based games.

## Limitations
- No minimax or deep search implemented; only immediate state evaluated.
- AI can be outsmarted by strategic human players.
- No long-term prediction or planning.
- Draw detection only after board fills completely.
- Limited to standard 3x3 Tic-Tac-Toe.















# Water Jug Problem Solver (BFS Approach)

## Problem Statement
Given two jugs with known capacities and a target amount of water, determine if it is possible to measure exactly the target amount using the following operations:
- Fill a jug completely.
- Empty a jug.
- Pour water from one jug to the other until one is empty or the other is full.
---

## Approach
- Use **Breadth-First Search (BFS)** to explore all possible states in order of increasing steps.
- Represent each state as `(amountInJug1, amountInJug2)`.
- From each state, generate all possible next states:
  1. Fill either jug.
  2. Empty either jug.
  3. Pour water from one jug to the other.
- Keep track of visited states to avoid repeated processing.
- BFS ensures the shortest number of steps to reach the target.

---
## Implementation Details
- `waterJugBFS`: Implements BFS using a queue to explore states level-by-level.
- `visited`: A set to store visited states to prevent revisiting.
- `nextStates`: Generated from each state by applying all valid moves.
- Main function takes jug capacities and target amount, then runs BFS.

## Time Complexity
- Worst-case: **O(jug1Cap × jug2Cap)** — all possible states explored once.
- BFS ensures minimal steps to reach the target.

## Space Complexity
- **O(jug1Cap × jug2Cap)** for visited states and BFS queue.

---

## Use Cases
- Finding the shortest sequence of steps in the water jug problem.
- AI search algorithm demonstration.
- Teaching tool for BFS and state-space exploration.

---
## Limitations
- Requires both jug capacities and target to be integers.
- Not optimized for very large capacities (can consume high memory).
- BFS may still explore many unnecessary states if target is unreachable.













# Water Jug Problem Solver (DFS Approach)

## Problem Statement
Given two jugs with known capacities and a target amount of water, determine whether it is possible to measure exactly the target amount using only the following operations:
- Fill a jug completely.
- Empty a jug.
- Pour water from one jug to the other until one is empty or the other is full.

---
## Approach
- Use **Depth-First Search (DFS)** to explore all possible states of the two jugs.
- Represent each state as a pair `(amountInJug1, amountInJug2)`.
- From each state, generate all possible next states by:
  1. Filling either jug.
  2. Emptying either jug.
  3. Pouring water from one jug to the other.
- Keep track of visited states to avoid infinite loops.
- Stop when the target is found in either jug or in the total of both.

---
## Implementation Details
- `waterJugDFS`: Core DFS logic using a stack for state exploration and a set to track visited states.
- `nextStates`: Generated by performing all possible valid operations from the current state.
- Main function takes user input for jug capacities and target amount, then runs DFS.

## Time Complexity
- Worst-case: **O(jug1Cap × jug2Cap)** (all possible states).
- DFS may explore deeply into one branch before backtracking.

## Space Complexity
- **O(jug1Cap × jug2Cap)** for storing visited states.

---
## Use Cases
- Classic AI search problem for understanding state-space exploration.
- Puzzle solving and algorithm learning.
- Foundation for more complex water distribution and resource allocation problems.

---
## Limitations
- DFS does not guarantee the shortest sequence of steps.
- Can explore unnecessary states before finding a solution.
- Limited to integer capacities and target amounts.





# Path Finding Using A* Search Algorithm  

## Aim  
The aim of this project is to implement the **A\* Search Algorithm** to find the optimal path from an initial position to a goal position in a 2D grid, while avoiding obstacles (rivers). The algorithm guarantees an optimal solution by combining the cost to reach a node (g) with the estimated cost to reach the goal (h).  

---

## Data Structures Used  
1. **`vector<int>`** – Represents a position on the grid as `{row, col}`.  
2. **`priority_queue<Node>`** – Stores nodes to be expanded, ordered by `f = g + h`.  
3. **`unordered_map<string, vector<int>> (um)`** – Maps encoded positions to their coordinates.  
4. **`unordered_map<string, string> (parent)`** – Tracks parent of each state for path reconstruction.  
5. **`unordered_map<string, double> (g_cost)`** – Stores the best-known cost from start to a node.  
6. **`set<string>` (closed set)** – Keeps track of already expanded nodes.  
7. **`vector<vector<int>>` (river)** – Grid representation marking obstacles (`1` for river, `0` for free cell).  

---

## Algorithm – A* Search  
1. **Initialize**:  
   - Push the start node into the priority queue with `f = h(start)`.  
   - Set its `g_cost = 0`.  
2. **Loop until goal is found or queue is empty**:  
   - Pop node with smallest `f`.  
   - If it matches the goal, reconstruct the path.  
   - Otherwise, expand all valid neighbors:  
     - Compute step cost (`1` for straight, `1.5` for diagonal).  
     - Update `g_cost` and push into the queue if a better path is found.  
   - Mark node as visited in the closed set.  
3. **Path Reconstruction**: Trace parents back from goal to start.  
4. **Output**: Display path coordinates and visual grid with:  
   - `i` → initial  
   - `f` → goal  
   - `*` → path  
   - `#` → river (obstacle)  

---

## State Generation  
The blank position (agent) can move in **8 directions** if valid and not blocked:  
- Up `(x-1, y)`  
- Down `(x+1, y)`  
- Left `(x, y-1)`  
- Right `(x, y+1)`  
- Diagonal moves: `(x±1, y±1)`  

---

## Utility Functions  
- **`checkGoal(curr, goal)`** → Checks if current position equals the goal.  
- **`encode(curr)`** → Converts coordinates into a unique string key.  
- **`isValid(x,y,size,river)`** → Validates if a position is within bounds and not a river.  
- **`h_value(curr, goal)`** → Manhattan distance heuristic.  
- **`genMove(state, size, river)`** → Generates all valid moves.  
- **`Path(parent, goalKey, um, size, river, initial, goal)`** → Reconstructs and prints the final path.  
- **`solve(initial, goal, size, river)`** → Main A* implementation.  

---

## Use Cases  
- Pathfinding in **robotics and navigation systems**.  
- Route optimization in **maps and games**.  
- Grid-based **AI search problems**.  
- Demonstrating **informed search algorithms** in Artificial Intelligence.  

---

## Time Complexity  
- Each state expansion considers at most **8 neighbors**.  
- Priority queue operations: **O(log n)** per insertion.  
- Worst-case: **O(E log V)** where V = number of cells, E = number of edges (≤ 8V).  
- **Overall Complexity**: O(V log V).  

## Space Complexity  
- Stores `g_cost`, `parent`, and `um` for visited states: **O(V)**.  
- Each state requires O(1) space.  
- **Overall Space**: O(V).  

---

## Sample Output  

### Example 1 – With Obstacles  
Input:
```text
Enter size of matrix:5
Enter coordinates of initial position(indexed from 0):0 0
Enter  coordinates of goal position(indexed from 0):2 3
Enter size of river:3
Enter points of river:
Point 1:1 1
Point 2:2 2
Point 3:3 3
```
Output:
```text
Path Matrix:
i * . . . 
. # * . .
. . # f .
. . . # .
. . . . .

Path found:
(0,0) (0,1) (1,2) (2,3)
```


---

## Advantages of A*  
- Guarantees the **optimal path** if heuristic is admissible.  
- Efficient compared to uninformed searches like BFS/DFS.  
- Handles weighted costs (e.g., diagonal movement with cost 1.5).  

## Limitations  
- Memory-intensive for large grids.  
- Performance depends heavily on the heuristic.  
- May still explore many states in worst-case scenarios.  
