- 👋 Hi, I’m @6231cool
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
6231cool/6231cool is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import random

# Initialize Pygame
pygame.init()

# Set up the screen
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Retro Bowl")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)

# Player variables
player_width = 50
player_height = 50
player_x = screen_width // 2 - player_width // 2
player_y = screen_height - player_height
player_speed = 5

# Football variables
football_width = 30
football_height = 30
football_x = random.randint(0, screen_width - football_width)
football_y = 0
football_speed = 3

# Main game loop
running = True
while running:
    screen.fill(BLACK)

    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Player movement
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= player_speed
    if keys[pygame.K_RIGHT]:
        player_x += player_speed

    # Boundaries for player
    if player_x < 0:
        player_x = 0
    elif player_x > screen_width - player_width:
        player_x = screen_width - player_width

    # Football movement
    football_y += football_speed

    # Reset football if it goes off the screen
    if football_y > screen_height:
        football_x = random.randint(0, screen_width - football_width)
        football_y = 0

    # Collision detection
    if (player_x < football_x + football_width and
            player_x + player_width > football_x and
            player_y < football_y + football_height and
            player_y + player_height > football_y):
        # If collision detected, reset football
        football_x = random.randint(0, screen_width - football_width)
        football_y = 0

    # Draw player
    pygame.draw.rect(screen, WHITE, (player_x, player_y, player_width, player_height))

    # Draw football
    pygame.draw.rect(screen, GREEN, (football_x, football_y, football_width, football_height))

    pygame.display.flip()

    # Control game speed
    pygame.time.Clock().tick(60)

# Quit Pygame
pygame.quit()

