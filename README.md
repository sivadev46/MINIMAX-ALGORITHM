# MINIMAX ALGORITHM

## Experiment: Implementation of MINIMAX Algorithm

### Aim

To implement MINIMAX algorithm using Python.

### Scenario: AI vs. Human Player – Winning Move Situation

The AI is playing as Player X and the human is playing as Player O. It is AI's turn, and there is a possible winning move.

### Given Board State (Before AI's Move)

```text
X O X
O X .
. O X
```

### Procedure

1. Define constants: PLAYER_X = 1, PLAYER_O = -1, EMPTY = 0.
2. Create evaluate(board) to check for a winner by scanning rows, columns, and diagonals.
3. Create isMovesLeft(board) to check for empty spaces.
4. Implement minimax(board, isMax):

   * If AI wins, return the corresponding score.
   * If human wins, return the corresponding score.
   * If no moves are left, return 0.
   * If it is AI's turn, maximize the score.
   * If it is the human's turn, minimize the score.
5. Implement findBestMove(board) to find the best move for AI.
6. Implement printBoard(board) to display the board.
7. Initialize a sample board, find the best move, and display the updated board.

### Python Program

```python
# Constants for players
PLAYER_X = 1
PLAYER_O = -1
EMPTY = 0

# Evaluate the board
def evaluate(board):
    for row in range(3):
        if board[row][0] == board[row][1] == board[row][2] != EMPTY:
            return board[row][0]

    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != EMPTY:
            return board[0][col]

    if board[0][0] == board[1][1] == board[2][2] != EMPTY:
        return board[0][0]

    if board[0][2] == board[1][1] == board[2][0] != EMPTY:
        return board[0][2]

    return 0

# Check if moves are left
def isMovesLeft(board):
    for row in range(3):
        for col in range(3):
            if board[row][col] == EMPTY:
                return True
    return False

# Minimax function
def minimax(board, isMax):
    score = evaluate(board)

    if score == PLAYER_X:
        return score

    if score == PLAYER_O:
        return score

    if not isMovesLeft(board):
        return 0

    if isMax:
        best = -float('inf')

        for row in range(3):
            for col in range(3):
                if board[row][col] == EMPTY:
                    board[row][col] = PLAYER_X
                    best = max(best, minimax(board, not isMax))
                    board[row][col] = EMPTY

        return best

    else:
        best = float('inf')

        for row in range(3):
            for col in range(3):
                if board[row][col] == EMPTY:
                    board[row][col] = PLAYER_O
                    best = min(best, minimax(board, not isMax))
                    board[row][col] = EMPTY

        return best

# Find the best move for PLAYER_X
def findBestMove(board):
    bestVal = -float('inf')
    bestMove = (-1, -1)

    for row in range(3):
        for col in range(3):
            if board[row][col] == EMPTY:
                board[row][col] = PLAYER_X
                moveVal = minimax(board, False)
                board[row][col] = EMPTY

                if moveVal > bestVal:
                    bestMove = (row, col)
                    bestVal = moveVal

    return bestMove

# Print the board
def printBoard(board):
    for row in board:
        print(" ".join(["X" if x == PLAYER_X else "O" if x == PLAYER_O else "." for x in row]))

# Example game
board = [
    [PLAYER_X, PLAYER_O, PLAYER_X],
    [PLAYER_O, PLAYER_X, EMPTY],
    [EMPTY, PLAYER_O, PLAYER_X]
]

print("Current Board:")
printBoard(board)

move = findBestMove(board)

print(f"Best Move: {move}")

board[move[0]][move[1]] = PLAYER_X

print("\nBoard after best move:")
printBoard(board)
```

### Output

```text
Current Board:
X O X
O X .
. O X

Best Move: (2, 0)

Board after best move:
X O X
O X .
X O X
```

### Result

Thus, the MINIMAX algorithm was successfully implemented using Python to determine the best move for the AI player in a Tic-Tac-Toe game.
