# Building a Caro Game Application Using the Pygame Library

The project focuses on developing a Caro game (also known as Gomoku) using Python's Pygame library. Caro is a popular two-player strategy game where the objective is to align five consecutive marks on a grid. The application allows users to play in multiple modes, including Player vs. Player (PvP) and Player vs. Computer (PvC), with adjustable difficulty levels—Easy, Medium, and Hard. The AI opponent is implemented using the Minimax algorithm, which ensures strategic gameplay by evaluating all possible moves to select the optimal one. The project also features customizable options such as grid size, interface themes (light/dark mode), and difficulty levels, providing an enhanced user experience.

Through this project, foundational game development techniques and advanced algorithmic logic are combined to deliver a fully functional, interactive Caro game application.

## Table of Contents  
- [Installation](#installation)  
- [Usage](#usage)  
- [Features](#features)  
- [Solution Principle](#solution-principle)  
- [The Structure of the Project: How It Is Divided into Functions](#the-structure-of-the-project-how-it-is-divided-into-functions)  
- [Functions Used and Their Interrelationships](#functions-used-and-their-interrelationships)  
- [The Use of External Libraries](#the-use-of-external-libraries)   
- [Credits](#credits)  
- [Project requirements checklists](#project-requirements-checklists)  
- [Reference](#reference)  


## Installation  

To install the necessary dependencies, run the following command: 

## Usage
To start the project, run the following script:

## Features
- 1- **Customizable Game Board**: Choose board sizes (3x3, 10x10, 15x15).
- 2- **Multiple Game Modes**: Play Player vs. Player (PVP) or Player vs. Computer (PVC).
- 3- **Adjustable AI Difficulty**: Select difficulty levels (Easy, Medium, Hard).
- 4- **Dynamic Themes**: Switch between light and dark board themes.

![Alt text](PythonCaroGame\Image\GameCaro.png)

## Solution Principle

The solution is built upon three core principles: game logic design, artificial intelligence implementation, and user interface development.

### Game Logic Design
The game board is constructed using a 2D array to represent the grid, where each cell reflects the state of the game (empty, player move, or AI move). Core logic includes:
- Validating player moves.
- Detecting win conditions by checking consecutive marks horizontally, vertically, and diagonally.
- Determining draw states when no moves remain.

### Artificial Intelligence Implementation
The AI opponent is implemented using the **Minimax algorithm**, a decision-making strategy in game theory that explores all possible future moves to determine the optimal move. To enhance performance, the algorithm incorporates **Alpha-Beta Pruning**, which eliminates unnecessary calculations, reducing computational cost.

The AI provides three difficulty levels:
- **Easy**: Random moves for simplicity.
- **Medium**: Combines random moves and basic Minimax for intermediate challenges.
- **Hard**: Utilizes the optimized Minimax with Alpha-Beta pruning for advanced decision-making.

### User Interface Development
The interface is created using the **Pygame** library, ensuring smooth visuals and interactivity. Key features include:
- **Customizable Game Board**: Users can select grid sizes (3x3, 10x10, 15x15).
- **Game Modes**: Player vs. Player (PvP) or Player vs. Computer (PvC) modes are supported.
- **Visual Customization**: Options like light/dark theme enhance user experience.
- **Interactive Menus**: Users can easily navigate settings and game options through an intuitive menu system.

## The Structure of the Project: How It Is Divided into Functions

The project is modularized into multiple classes and functions to ensure clarity, maintainability, and reusability. The key components include:

### **Game Logic**
- **`BasicBoardLogic` Class**: Implements the fundamental game rules and board management.
  - `markSquare(playerId, row, col)`: Marks a move on the board.
  - `checkLineFromPos(playerId, row, col, changeRow, changeCol)`: Checks for winning lines in any direction.
  - `getWinningState()`: Determines if a player has won.
  - `getEmptySquares()`: Returns all available empty cells.
  - `isFull()`: Checks if the board is full.
  - `copyBoard()`: Copies the current board state for AI calculations.

- **`AdvancedBoardLogic` Class** (inherits from `BasicBoardLogic`):  
  Adds advanced logic to evaluate moves:
  - `getScoreOfPosition(playerId, row, col)`: Calculates the score of a move based on its strategic value.

### **Artificial Intelligence**
- **`AI` Class**: Handles the computer opponent logic using Minimax and Alpha-Beta Pruning.
  - `minimax(board, isMaximizing, depth)`: Standard Minimax algorithm to find the best move.
  - `minimax_update(board, isMaximizing, alpha, beta, depth)`: Optimized Minimax using Alpha-Beta pruning.
  - `random_Level(main_board)`: Selects a random move for the Easy difficulty.
  - `mostMove(main_board)`: Evaluates and returns the most favorable move.
  - `easyLevel(main_board)`: Implements logic for Easy AI.
  - `mediumLevel(main_board)`: Combines random moves and Minimax for Medium AI.
  - `hardLevel(main_board)`: Uses Minimax with Alpha-Beta Pruning for Hard AI.

### **User Interface**
- **`BoardGUI` Class**: Manages the graphical rendering of the game.
  - Draws the game board grid.
  - Marks player moves on the board.
  - Highlights winning lines when a player wins.

- **`GameAction` Class**: Handles gameplay actions and controls.
  - Initializes Player vs. Player (PvP) and Player vs. Computer (PvC) game modes.
  - Updates the game state based on user input or AI decisions.

- **`Menu` Class**: Manages the main menu and game settings.
  - Allows users to configure the grid size, difficulty level, and game mode.
  - Provides options for light/dark themes.

### **Main Program**
- The main program ties all components together:
  - Initializes the game.
  - Displays the menu and retrieves user preferences.
  - Starts the game loop, managing player moves, AI moves, and UI updates.

## Functions Used and Their Interrelationships

Below is an overview of key functions and their relationships:

### **Game Logic Functions**  
Handled within the `BasicBoardLogic` and `AdvancedBoardLogic` classes:
- **`markSquare(playerId, row, col)`**  
   Marks a move on the board. This function is fundamental as it updates the game state after each move.  
   _Interrelationship_: Called during each player's turn or by the AI when choosing a move.

- **`checkLineFromPos(playerId, row, col, changeRow, changeCol)`**  
   Checks for consecutive marks (horizontal, vertical, diagonal).  
   _Interrelationship_: Called by `getWinningState()` to verify if a player has won.

- **`getWinningState()`**  
   Determines if a player has achieved victory.  
   _Interrelationship_: Relies on `checkLineFromPos()` and is called after every move.

- **`getEmptySquares()`**  
   Returns all unoccupied cells on the board.  
   _Interrelationship_: Essential for the AI to identify valid moves.

- **`isFull()`**  
   Checks if the board is completely filled (draw condition).  
   _Interrelationship_: Called at the end of each move to determine if the game is over.

- **`copyBoard()`**  
   Creates a duplicate of the board state for AI simulations.  
   _Interrelationship_: Used by the AI to recursively explore future moves without modifying the main game state.

### **AI Functions**  
Within the `AI` class, these functions implement the computer opponent's logic:
- **`minimax(board, isMaximizing, depth)`**  
   Implements the Minimax algorithm to find the best move.  
   _Interrelationship_: Uses `copyBoard()` to simulate moves and `getEmptySquares()` to iterate over possible moves.

- **`minimax_update(board, isMaximizing, alpha, beta, depth)`**  
   An optimized version of Minimax with Alpha-Beta Pruning.  
   _Interrelationship_: Reduces unnecessary branches during recursion for better performance.

- **`random_Level(main_board)`**  
   Returns a random move for the **Easy** difficulty mode.  
   _Interrelationship_: Relies on `getEmptySquares()` to identify valid moves.

- **`mostMove(main_board)`**  
   Identifies the most advantageous move for the AI.  
   _Interrelationship_: Used in **Medium** and **Hard** difficulty levels to evaluate board positions.

- **`easyLevel()`, `mediumLevel()`, `hardLevel()`**  
   Implements the AI behavior based on difficulty.  
   _Interrelationship_: Each function calls the appropriate move-selection function (`random_Level`, `minimax`, or `minimax_update`).

### **User Interface Functions**  
Within the `BoardGUI`, `GameAction`, and `Menu` classes:
- **`drawBoardGames()`**  
   Renders the game grid.  
   _Interrelationship_: Initializes the board and updates the grid at the start of the game.  

- **`markSquare()`**  
   Marks the player’s move, checks for a winning state, and triggers visual updates.  
   _Interrelationship_: Calls `drawPlayerMark()` to render the move and `drawWinningLine()` if a winning state is detected.  

- **`drawPlayerMark()`**  
   Draws the player’s symbol (cross or circle) on the board.  
   _Interrelationship_: Called by `markSquare()` after a move.  

- **`drawWinningLine()`**  
   Draws a line indicating the winning move (horizontal, vertical, or diagonal).  
   _Interrelationship_: Called by `markSquare()` when a winning condition is found.  

## The Use of External Libraries  

- **Pygame** is the core library used to build the graphical user interface and manage game events. 
- **Pygame-menu** is for menus

## Credits
This project uses the following open-source packages and resources:
- Python
- Pygame
- Pygame-menu

## Project requirements checklists

- [x] **The project is written in Python**
- [x] **The project includes at least 5 functions**: resetGame, runGamePVP, runGameAI (GameAction), initPVPGame, initPVCGame (MainMenu)
- [x] **The project involves reading from and writing to a file**: background_color=pygame_menu.baseimage.BaseImage(r"./Image/background.jpg")
- [x] **The minimum length of the project is approximately 100 lines of code / author (so a pair project should be about 200 lines long)**
- [x] **The project uses a list and a dictionary**: light_theme {} (LightTheme), items [] (MainMenu) 

## Reference

- Coding Spot, “Coding an Unbeatable Tic Tac Toe AI Using Python and the Minimax Algorithm”, https://www.youtube.com/watch?v=Bk9hlNZc6sE&ab_channel=CodingSpot
- Sebastian Lague, “Algorithms Explained – minimax and alpha-beta pruning”,https://www.youtube.com/watch?v=l-hh51ncgDI&ab_channel=SebastianLague
- Pygame_menu, “Pygame menu documents”, https://pygame-menu.readthedocs.io/en/4.2.8/
- Pygame, “Pygame documents”, https://www.pygame.org/docs/
- Coding Spot, “Python tictactoe ai”, https://github.com/AlejoG10/python-tictactoe-ai-y