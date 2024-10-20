# Sylvia the Snake 🐍

"Sylvia the Snake" is a simple, fun snake game built using Python's `tkinter` library. The player controls the snake as it moves around the game board to eat food while avoiding collisions with the walls or itself. Each time the snake eats the food, it grows, and the game speeds up, making it more challenging over time.

## Features

- Classic snake gameplay
- Controls for moving the snake up, down, left, and right
- The snake grows each time it eats food
- Real-time score display
- Game over detection when the snake collides with the wall or itself
- Simple GUI using Python's `tkinter`

## Game Rules

- **Objective**: The goal is to make the snake as long as possible by eating the food that appears on the screen.
- **Controls**: 
  - Arrow keys (`Left`, `Right`, `Up`, `Down`) to move the snake in the desired direction.
- **Losing Condition**: 
  - The game ends if the snake collides with the game boundaries or with itself.

## Requirements

- Python 3.x
- `tkinter` library (This is generally included with Python installations)

## How to Run

1. Make sure you have Python installed. You can check the version by running:
    ```bash
    python --version
    ```

2. If Python is installed, ensure `tkinter` is available. Usually, `tkinter` is included by default in most Python installations. You can test it by running:
    ```python
    import tkinter
    ```

3. Clone the repository or download the code files.

4. Run the game by executing the Python script:
    ```bash
    python sylvia_the_snake.py
    ```

5. Control the snake using the **arrow keys** to change direction, and try to eat as much food as possible without crashing!

## Code Overview

### Main Components:

- **Snake Class**: 
    - Handles the creation of the snake body and its movement. The snake is made of squares, which are updated as the game progresses.
- **Food Class**: 
    - Randomly generates food at different locations on the board, represented as a red square.
- **next_turn Function**: 
    - This function handles the snake's movement in each turn, updates the game, and checks whether the snake has eaten the food or collided with the wall or itself.
- **change_direction Function**: 
    - Changes the direction of the snake based on user input (arrow keys).
- **check_collisions Function**: 
    - Detects if the snake has collided with the wall or its own body.
- **game_over Function**: 
    - Handles the end of the game, showing a "GAME OVER" message when the snake crashes.

## Game Mechanics

- **Game Speed**: The game speed is controlled by the `SPEED` variable. The snake moves faster as it grows longer.
- **Space Size**: Each part of the snake and the food is represented by a square of size `50x50`.
- **Score**: The current score is displayed at the top of the window and updates each time the snake eats the food.
- **Colors**:
    - **Snake**: Blue
    - **Food**: Red
    - **Background**: Black

## Future Enhancements

- Adding difficulty levels that increase the speed or add obstacles
- Implementing a high score tracker
- Adding different snake colors or themes

## Full Code

```python
from tkinter import *
import random

GAME_WIDTH = 700
GAME_HEIGHT = 700
SPEED = 159
SPACE_SIZE = 50
BODY_PARTS = 3
SNAKE_COLOUR = "BLUE"
FOOD_COLOUR = "RED"
BACKGROUND_COLOUR = "BLACK"

class Snake:
    def __init__(self):
        self.body_size = BODY_PARTS
        self.coordinates = []
        self.squares = []

        for i in range(0, BODY_PARTS):
            self.coordinates.append([0, 0])

        for x, y in self.coordinates:
            square = canvas.create_rectangle(x, y, x + SPACE_SIZE, y + SPACE_SIZE, fill=SNAKE_COLOUR, tag="snake")
            self.squares.append(square)

class Food:
    def __init__(self):
        x = random.randint(0, (GAME_WIDTH / SPACE_SIZE) - 1) * SPACE_SIZE
        y = random.randint(0, (GAME_HEIGHT / SPACE_SIZE) - 1) * SPACE_SIZE

        self.coordinates = [x, y]

        canvas.create_rectangle(x, y, x + SPACE_SIZE, y + SPACE_SIZE, fill=FOOD_COLOUR, tag="food")

def next_turn(snake, food):
    x, y = snake.coordinates[0]

    if direction == "up":
        y -= SPACE_SIZE
    elif direction == "down":
        y += SPACE_SIZE
    elif direction == "left":
        x -= SPACE_SIZE
    elif direction == "right":
        x += SPACE_SIZE

    snake.coordinates.insert(0, (x, y))
    square = canvas.create_rectangle(x, y, x + SPACE_SIZE, y + SPACE_SIZE, fill=SNAKE_COLOUR)
    snake.squares.insert(0, square)

    if x == food.coordinates[0] and y == food.coordinates[1]:
        global score
        score += 1
        label.config(text="Score:{}".format(score))
        canvas.delete("food")
        food = Food()
    else:
        del snake.coordinates[-1]
        canvas.delete(snake.squares[-1])
        del snake.squares[-1]

    if check_collisions(snake):
        game_over()
    else:
        window.after(SPEED, next_turn, snake, food)

def change_direction(new_direction):
    global direction
    if new_direction == "left":
        if direction != "right":
            direction = new_direction
    elif new_direction == "right":
        if direction != "left":
            direction = new_direction
    elif new_direction == "up":
        if direction != "down":
            direction = new_direction
    elif new_direction == "down":
        if direction != "up":
            direction = new_direction

def check_collisions(snake):
    x, y = snake.coordinates[0]
    if x < 0 or x >= GAME_WIDTH or y < 0 or y >= GAME_HEIGHT:
        return True

    for body_part in snake.coordinates[1:]:
        if x == body_part[0] and y == body_part[1]:
            return True

    return False

def game_over():
    canvas.delete(ALL)
    canvas.create_text(canvas.winfo_width() / 2, canvas.winfo_height() / 2, text="GAME OVER", fill="red", tag="gameover")

window = Tk()
window.title("Sylvia the Snake")
window.resizable(False, False)

score = 0
direction = "down"

label = Label(window, text="Score:{}".format(score))
label.pack()

canvas = Canvas(window, bg=BACKGROUND_COLOUR, height=GAME_HEIGHT, width=GAME_WIDTH)
canvas.pack()

window.update()

window_width = window.winfo_width()
window_height = window.winfo_height()
screen_width = window.winfo_screenwidth()
screen_height = window.winfo_screenheight()

x = int((screen_width / 2) - (window_width / 2))
y = int((screen_height / 2) - (window_height / 2))

window.geometry(f"{window_width}x{window_height}+{x}+{y}")

window.bind('<Left>', lambda event: change_direction("left"))
window.bind('<Right>', lambda event: change_direction("right"))
window.bind('<Up>', lambda event: change_direction("up"))
window.bind('<Down>', lambda event: change_direction("down"))

snake = Snake()
food = Food()

next_turn(snake, food)

window.mainloop()
