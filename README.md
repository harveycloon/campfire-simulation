# campfire-simulation
import pygame
import random

# Initialize pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("🔥 Campfire Simulation 🔥")

# Colors
BLACK = (0, 0, 0)
ORANGE = (255, 140, 0)
YELLOW = (255, 215, 0)
RED = (255, 69, 0)

# Fire particles list
particles = []

class FireParticle:
    def __init__(self, x, y):
        self.x = x + random.randint(-10, 10)
        self.y = y
        self.size = random.randint(5, 10)
        self.color = random.choice([ORANGE, YELLOW, RED])
        self.velocity = random.uniform(-1, -0.3)

    def move(self):
        self.y += self.velocity
        self.size -= 0.1
        if self.size <= 0:
            particles.remove(self)

    def draw(self, screen):
        pygame.draw.circle(screen, self.color, (int(self.x), int(self.y)), int(self.size))

running = True
clock = pygame.time.Clock()

while running:
    screen.fill(BLACK)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Generate fire particles
    if len(particles) < 100:
        particles.append(FireParticle(WIDTH//2, HEIGHT//2))
    
    # Update and draw particles
    for particle in particles[:]:
        particle.move()
        particle.draw(screen)
    
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
ewasr
