# Git Intro Project

───────┬──────────────────────────────────────────────────────────────────────────────────────────────
       │ File: factorial.py
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ #!/usr/bin/python3
   2   │
   3   │ import sys
   4   │
   5   │ def factorial(n):
   6   │     result = 1
   7   │     while n > 1:
   8   │         result *= n
   9   │         n -= 1
  10   │     return result
  11   │
  12   │ f = factorial(int(sys.argv[1]))
  13   │ print(f)
───────┴──────────────────────────────────────────────────────────────────────────────────────────────

────┬──────────────────────────────────────────────────────────────────────────────────────────────
       │ File: print_arguments.py
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ #!/usr/bin/python3
   2   │
   3   │ import sys
   4   │
   5   │ for arg in sys.argv[1:]:
   6   │     print(arg)
───────┴─────────────────────────

 File: change_background.html
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ <!DOCTYPE html>
   2   │ <html lang="en">
   3   │ <head>
   4   │     <meta charset="UTF-8">
   5   │     <title>Change Background Color</title>
   6   │
   7   │     <style>
   8   │         body {
   9   │             font-family: Arial, sans-serif;
  10   │             text-align: center;
  11   │             padding-top: 50px;
  12   │         }
  13   │         button {
  14   │             padding: 10px 20px;
  15   │             font-size: 16px;
  16   │             cursor: pointer;
  17   │         }
  18   │     </style>
  19   │ </head>
  20   │
  21   │ <body>
  22   │     <p>Click the button to change the background color</p>
  23   │
  24   │     <button id="colorButton">Change Color</button>
  25   │
  26   │     <script>
  27   │         document.getElementById("colorButton").addEventListener("click", function () {
  28   │             changeBackgroundColor();
  29   │         });
  30   │
  31   │         function changeBackgroundColor() {
  32   │             // Generate a random color
  33   │             var randomColor = "#" + Math.floor(Math.random() * 16777215).toString(16);
  34   │             // Change the background color of the body
  35   │             document.body.style.backgroundColor = randomColor;
  36   │         }
  37   │     </script>
  38   │ </body>
  39   │ </html>
───────┴───────────────────────────────────────────────────────

#!/usr/bin/python3

import random
import os

def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')


class Minesweeper:
    def __init__(self, width=10, height=10, mines=10):
        self.width = width
        self.height = height
        self.total_cells = width * height
        self.mine_count = mines

        self.mines = set(random.sample(range(self.total_cells), mines))
        self.revealed = [[False for _ in range(width)] for _ in range(height)]

    def print_board(self, reveal=False):
        clear_screen()
        print('  ' + ' '.join(str(i) for i in range(self.width)))
        for y in range(self.height):
            print(y, end=' ')
            for x in range(self.width):
                if reveal or self.revealed[y][x]:
                    if (y * self.width + x) in self.mines:
                        print('*', end=' ')
                    else:
                        count = self.count_mines_nearby(x, y)
                        print(count if count > 0 else ' ', end=' ')
                else:
                    print('.', end=' ')
            print()

    def count_mines_nearby(self, x, y):
        count = 0
        for dx in [-1, 0, 1]:
            for dy in [-1, 0, 1]:
                if dx == 0 and dy == 0:
                    continue
                nx, ny = x + dx, y + dy
                if 0 <= nx < self.width and 0 <= ny < self.height:
                    if (ny * self.width + nx) in self.mines:
                        count += 1
        return count

    def reveal(self, x, y):
        if (y * self.width + x) in self.mines:
            return False

        if self.revealed[y][x]:
            return True

        self.revealed[y][x] = True

        if self.count_mines_nearby(x, y) == 0:
            for dx in [-1, 0, 1]:
                for dy in [-1, 0, 1]:
                    nx, ny = x + dx, y + dy
                    if 0 <= nx < self.width and 0 <= ny < self.height:
                        self.reveal(nx, ny)

        return True

    def check_win(self):
        revealed_count = sum(
            self.revealed[y][x]
            for y in range(self.height)
            for x in range(self.width)
        )
        return revealed_count == self.total_cells - self.mine_count

    def play(self):
        while True:
            self.print_board()
            try:
                x = int(input("Enter x coordinate: "))
                y = int(input("Enter y coordinate: "))

                if not (0 <= x < self.width and 0 <= y < self.height):
                    print("Coordinates out of range.")
                    continue

                if not self.reveal(x, y):
                    self.print_board(reveal=True)
                    print("Game Over! You hit a mine.")
                    break

                if self.check_win():
                    self.print_board(reveal=True)
                    print("Congratulations! You've won the game.")
                    break

            except ValueError:
                print("Invalid input. Please enter numbers only.")


if __name__ == "__main__":
    game = Minesweeper()
    game.play()
-----------------------------------------------------------------------------------------

#!/usr/bin/python3

import sys

def factorial(n):
    """
    Function description:
    Computes the factorial of a number using recursion.

    Parameters:
    n (int): The number for which the factorial is calculated.
             Must be a non-negative integer.

    Returns:
    int: The factorial of the given number.
    """
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

f = factorial(int(sys.argv[1]))
print(f)
----------------------------------------------------------------------------------------------------

class Checkbook:
    def __init__(self):
        self.balance = 0.0

    def deposit(self, amount):
        self.balance += amount
        print("Deposited ${:.2f}".format(amount))
        print("Current Balance: ${:.2f}".format(self.balance))

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient funds to complete the withdrawal.")
        else:
            self.balance -= amount
            print("Withdrew ${:.2f}".format(amount))
            print("Current Balance: ${:.2f}".format(self.balance))

    def get_balance(self):
        print("Current Balance: ${:.2f}".format(self.balance))


def main():
    cb = Checkbook()

    while True:
        action = input(
            "What would you like to do? (deposit, withdraw, balance, exit): "
        ).lower()

        if action == 'exit':
            break

        elif action == 'deposit':
            try:
                amount = float(input("Enter the amount to deposit: $"))
                if amount < 0:
                    print("Amount must be positive.")
                    continue
                cb.deposit(amount)
            except ValueError:
                print("Invalid amount. Please enter a numeric value.")

        elif action == 'withdraw':
            try:
                amount = float(input("Enter the amount to withdraw: $"))
                if amount < 0:
                    print("Amount must be positive.")
                    continue
                cb.withdraw(amount)
            except ValueError:
                print("Invalid amount. Please enter a numeric value.")

        elif action == 'balance':
            cb.get_balance()

        else:
            print("Invalid command. Please try again.")


if __name__ == "__main__":
    main()
-------------------------------------------------------------------------------------------------
#!/usr/bin/python3

def print_board(board):
    print()
    for i, row in enumerate(board):
        print(" | ".join(row))
        if i < 2:
            print("-" * 5)
    print()


def check_winner(board):
    # Check rows
    for row in board:
        if row[0] != " " and row.count(row[0]) == 3:
            return True

    # Check columns
    for col in range(3):
        if board[0][col] != " " and \
           board[0][col] == board[1][col] == board[2][col]:
            return True

    # Check diagonals
    if board[0][0] != " " and \
       board[0][0] == board[1][1] == board[2][2]:
        return True

    if board[0][2] != " " and \
       board[0][2] == board[1][1] == board[2][0]:
        return True

    return False


def board_full(board):
    for row in board:
        if " " in row:
            return False
    return True


def tic_tac_toe():
    board = [[" "] * 3 for _ in range(3)]
    player = "X"

    while True:
        print_board(board)

        # Input validation
        try:
            row = int(input(f"Enter row (0, 1, or 2) for player {player}: "))
            col = int(input(f"Enter column (0, 1, or 2) for player {player}: "))
        except ValueError:
            print("Invalid input. Please enter numbers only.")
            continue

        if row not in range(3) or col not in range(3):
            print("Invalid position. Row and column must be 0, 1, or 2.")
            continue

        if board[row][col] != " ":
            print("That spot is already taken! Try again.")
            continue

        board[row][col] = player

        # Check win
        if check_winner(board):
            print_board(board)
            print(f"Player {player} wins!")
            break

        # Check draw
        if board_full(board):
            print_board(board)
            print("It's a draw!")
            break

        # Switch player
        player = "O" if player == "X" else "X"


if __name__ == "__main__":
    tic_tac_toe()
