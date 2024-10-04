# Ex.No: 11  Mini Project 
### DATE: 04/10/2024                                                                           
### REGISTER NUMBER : 212221240062
### AIM: 
To write a python program to simulate the 2048 game.
### Algorithm:
#### Step-1: 
Create a 4x4 grid filled with zeros (empty tiles).
#### Step-2: 
Randomly place two tiles (either a 2 or a 4) in two empty cells on the board.
#### Step-3: 
Display the current state of the board.
#### Step-4: 
Ask the player for input (w, s, a, d) to indicate the direction of the move (up, down, left, right).
#### Step-5: 
If the input is invalid, prompt the player to enter a valid move.
#### Step-6: 
After a valid move, add a new tile (either 2 or 4) at a random empty cell on the board.
#### Step-7: 
If there are no empty tiles left and no adjacent tiles can be merged, the game is over.
#### Step-8: 
If there are still possible moves or empty tiles, repeat the game loop.
### Program:
```
import random
import numpy as np

class Game2048:
    def __init__(self):
        self.size = 4
        self.board = np.zeros((self.size, self.size), dtype=int)
        self.add_new_tile()
        self.add_new_tile()

    def add_new_tile(self):
        empty_cells = list(zip(*np.where(self.board == 0)))
        if empty_cells:
            row, col = random.choice(empty_cells)
            self.board[row][col] = 2 if random.random() < 0.9 else 4

    def compress(self, row):
        """ Compress the row to move all non-zero elements to the left """
        new_row = [num for num in row if num != 0]
        new_row += [0] * (self.size - len(new_row))
        return new_row

    def merge(self, row):
        """ Merge tiles of the same value and shift them """
        for i in range(self.size - 1):
            if row[i] == row[i + 1] and row[i] != 0:
                row[i] *= 2
                row[i + 1] = 0
        return row

    def move_left(self):
        """ Perform a move to the left """
        for i in range(self.size):
            self.board[i] = self.compress(self.board[i])
            self.board[i] = self.merge(self.board[i])
            self.board[i] = self.compress(self.board[i])

    def move_right(self):
        """ Perform a move to the right """
        self.board = np.fliplr(self.board)
        self.move_left()
        self.board = np.fliplr(self.board)

    def move_up(self):
        """ Perform a move upwards """
        self.board = self.board.T
        self.move_left()
        self.board = self.board.T

    def move_down(self):
        """ Perform a move downwards """
        self.board = self.board.T
        self.move_right()
        self.board = self.board.T

    def is_game_over(self):
        """ Check if there are no more moves """
        if np.any(self.board == 0):
            return False
        for i in range(self.size):
            for j in range(self.size - 1):
                if self.board[i][j] == self.board[i][j + 1]:
                    return False
                if self.board[j][i] == self.board[j + 1][i]:
                    return False
        return True

    def play(self):
        """ Main loop to run the game """
        print("Welcome to 2048! Use w (up), s (down), a (left), d (right) to move. q to quit.")
        while True:
            print(self.board)
            move = input("Enter move: ").strip().lower()
            if move == 'a':
                self.move_left()
            elif move == 'd':
                self.move_right()
            elif move == 'w':
                self.move_up()
            elif move == 's':
                self.move_down()
            elif move == 'q':
                print("Game quit!")
                break
            else:
                print("Invalid move! Use w (up), s (down), a (left), d (right).")
                continue

            self.add_new_tile()

            if self.is_game_over():
                print("Game over! No more moves available.")
                print(self.board)
                break

# Start the game
if __name__ == "__main__":
    game = Game2048()
    game.play()
```
### Output:
![image](https://github.com/user-attachments/assets/7a5df342-de57-4dfc-bd79-e151a7977174)

### Result:
Thus the simple 2048 game was implemented using python
