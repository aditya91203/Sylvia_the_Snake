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


Enjoy playing **Sylvia the Snake**! Feel free to modify and improve the game as you see fit.

# Sylvia_the_Snake
