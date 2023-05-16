# PyTestrix
----------------------------
We will creating a Tetris game in Python.

We need the pygame library to create the game window and handle game events. You can install it using pip.
```
import pygame
import random
import time
```
Now we will create a game window using the pygame library. You can set the window size and background color according to your preference.
```
pygame.init()

# Set up game window
WINDOW_WIDTH = 640
WINDOW_HEIGHT = 480
WINDOW_TITLE = 'Colorful Tetris'
WINDOW_BG_COLOR = (255, 255, 255)
window = pygame.display.set_mode((WINDOW_WIDTH, WINDOW_HEIGHT))
pygame.display.set_caption(WINDOW_TITLE)
```
Then we will define the game objects such as the tetrominoes and the game board. You can use lists to store the different shapes and colors of the tetrominoes, and a 2D list to store the state of the game board.
```
# Define game objects
BLOCK_SIZE = 20
TETROMINOES = [
    ((0, 0), (1, 0), (2, 0), (3, 0)), # I shape
    ((0, 0), (0, 1), (1, 0), (1, 1)), # O shape
    ((0, 0), (1, 0), (1, 1), (2, 1)), # S shape
    ((0, 1), (1, 1), (1, 0), (2, 0)), # Z shape
    ((0, 0), (0, 1), (0, 2), (1, 1)), # T shape
    ((0, 1), (1, 1), (2, 1), (2, 0)), # L shape
    ((0, 0), (1, 0), (2, 0), (2, 1))  # J shape
]
TETROMINO_COLORS = [
    (0, 255, 255), # I shape
    (255, 255, 0), # O shape
    (0, 255, 0),   # S shape
    (255, 0, 0),   # Z shape
    (255, 0, 255), # T shape
    (255, 165, 0), # L shape
    (0, 0, 255)    # J shape
]
ROWS = WINDOW_HEIGHT // BLOCK_SIZE
COLS = WINDOW_WIDTH // BLOCK_SIZE
board = [[0] * COLS for _ in range(ROWS)]
```
Now, we will create a Tetromino class to represent each tetromino in the game. The class will have methods to move the tetromino down, left, right, and rotate it.
```
class Tetromino:
    def __init__(self, shape, color):
        self.shape = shape
        self.color = color
        self.x = COLS // 2 - 2
        self.y = 0
        
    def move_down(self):
        self.y += 1
        
    def move_left(self):
        self.x -= 1
        
    def move_right(self):
        self.x += 1
        
    def rotate(self):
        rotated_shape = []
        for block in self.shape:
            x, y = block
            # Rotate 90 degrees counterclockwise
            rotated_x = -y
            rotated_y = x
            rotated_shape.append((rotated_x, rotated_y))
        self.shape = rotated_shape
```
Then we will create functions to handle game events, update the game state, draw the game objects on the screen, and check for collisions.
```
def handle_events():
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                tetromino.move_left()
            elif event.key == pygame.K_RIGHT:
                tetromino.move_right()
            elif event.key == pygame.K_DOWN:
                tetromino.move_down()
            elif event.key == pygame.K_UP:
                tetromino.rotate()

def update_game():
    # Update game logic here
    pass

def draw_game():
    # Draw game objects on the screen here
    pass

def check_collision():
    # Check for collision with the game board here
    pass
```
And then we will implement the game loop that will continuously update the game state, handle events, draw the game objects, and check for collisions.
```
def game_loop():
    clock = pygame.time.Clock()
    game_over = False
    tetromino = Tetromino(random.choice(TETROMINOES), random.choice(TETROMINO_COLORS))

    while not game_over:
        handle_events()
        update_game()
        draw_game()
        check_collision()
        
        pygame.display.update()
        clock.tick(10)  # Set desired frames per second

game_loop()
```
Now we will implement points and levels for the game. We will add variables to keep track of the player's points and level. Increment the points when a line is cleared, and increase the level when a certain number of points are reached.
```
points = 0
level = 1

def clear_line():
    # Clear completed lines and update points

def increase_level():
    # Increase the level based on points

def update_game():
    # Update game logic here
    clear_line()
    increase_level()

def draw_game():
    # Draw game objects on the screen here
    # Draw points and level on the screen
    pass
```
Now we can use a text input field to allow the player to enter their name when they break the record points. You can use the pygame_textinput library to create the text input field.
```
import pygame_textinput

def enter_name():
    pygame.init()
    screen = pygame.display.set_mode((WINDOW_WIDTH, WINDOW_HEIGHT))
    pygame.display.set_caption("Enter Your Name")
    
    textinput = pygame_textinput.TextInput()
    clock = pygame.time.Clock()
    name = None

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
                
        screen.fill((255, 255, 255))
        events = pygame.event.get()
        for event in events:
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        if textinput.update(events):
            name = textinput.get_text()
            break

        screen.blit(textinput.get_surface(), (10, 10))
        pygame.display.update()
        clock.tick(30)
    
    return name

record_points = 1000  # Example value for record points
current_points = 500  # Example value for current points

if current_points > record
if current_points > record_points:
    record_points = current_points
    player_name = enter_name()
    print("Congratulations, you broke the record!")
    print("Player Name:", player_name)
    print("Record Points:", record_points)
else:
    print("Current Points:", current_points)
    print("Record Points:", record_points)
```
This code snippet checks if the current points exceed the record points. If so, it prompts the player to enter their name using the enter_name() function. Once the player enters their name, it displays a congratulatory message along with the player's name and the new record points. If the current points are not higher than the record points, it simply displays the current and record points.
