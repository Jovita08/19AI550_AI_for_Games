# Ex.No: 4  Implementation of Snake game using Steering behaviors
### DATE: 04/08/24                                                                       
### REGISTER NUMBER : 212221240062
### AIM: 
To write a python program to simulate the snake game using steering behaviors
### Algorithm:
1. Start the program
2. Import the necessary modules
3. Initiate the pygame engine and window
4. Specify the necessary parameter for background,snake and food
5. Create a function for seeking behavior towards the target
6.  Move the snake towards the target by move function
7.  Increase the size of snake by wrap around function
8.  create a food at location randomly
9.  In main, create a game loop, move the snake towards the food,check the collision and increase the size
10.  Update the display
11.  Stop the program
 ### Program:
```python
import pygame
import math
import sys

# Initialize Pygame
pygame.init()

# Set up display
WIDTH, HEIGHT = 800, 600
window = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Kinematic Movement Example")

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
# Character settings
CHAR_SIZE = 20
MAX_SPEED = 5

# Character class
class Character:
    def _init_(self, x, y, color):
        self.position = pygame.Vector2(x, y)
        self.velocity = pygame.Vector2(0, 0)
        self.color = color

    def seek(self, target):
        desired_velocity = target - self.position
        if desired_velocity.length() > 0:  # Ensure the vector is not zero
            desired_velocity = desired_velocity.normalize() * MAX_SPEED
        self.velocity = desired_velocity

    def flee(self, target):
        desired_velocity = self.position - target
        if desired_velocity.length() > 0:  # Ensure the vector is not zero
            desired_velocity = desired_velocity.normalize() * MAX_SPEED
        self.velocity = desired_velocity

    def update(self):
        self.position += self.velocity

    def draw(self, surface):
        pygame.draw.circle(surface, self.color, (int(self.position.x), int(self.position.y)), CHAR_SIZE)

# Main function
def main():
    clock = pygame.time.Clock()
    player = Character(WIDTH // 2, HEIGHT // 2, WHITE)
    target = Character(WIDTH // 4, HEIGHT // 4, RED)

    running = True
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Get mouse position
        mouse_pos = pygame.Vector2(pygame.mouse.get_pos())

        # Basic controls: seek or flee based on mouse button
        if pygame.mouse.get_pressed()[0]:  # Left button - Seek
            player.seek(mouse_pos)
        elif pygame.mouse.get_pressed()[2]:  # Right button - Flee
            player.flee(mouse_pos)
        else:
            player.velocity = pygame.Vector2(0, 0)  # Stop if no button is pressed

        # Update player position
        player.update()

        # Draw everything
        window.fill(BLACK)
        player.draw(window)
        target.draw(window)
        pygame.display.flip()

        # Cap the frame rate
        clock.tick(60)

    pygame.quit()
    sys.exit()

if _name_ == "_main_":
    main()
```

### Output:

![Screenshot 2024-08-17 092026](https://github.com/user-attachments/assets/fae0ccb4-1ac5-4321-ac33-4e3e5ceaaa87)


### Result:
Thus the simple HotPotato game was implemented using Queue.