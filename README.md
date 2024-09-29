import pygame
import random

# Pygame ni boshlash
pygame.init()

# O’yin oynasining o’lchovlari
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Hamster Kombat")

# Ranglar
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Hamster klassi
class Hamster(pygame.sprite.Sprite):
    def __init__(self, x, y):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(WHITE)
        self.rect = self.image.get_rect(center=(x, y))
        self.health = 100

    def update(self):
        # Harakat logikasi
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            self.rect.x -= 5
        if keys[pygame.K_RIGHT]:
            self.rect.x += 5
        if keys[pygame.K_UP]:
            self.rect.y -= 5
        if keys[pygame.K_DOWN]:
            self.rect.y += 5

# O’yin loopi
def main():
    running = True
    hamster = Hamster(WIDTH // 2, HEIGHT // 2)
    all_sprites = pygame.sprite.Group()
    all_sprites.add(hamster)

    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        all_sprites.update()

        # Ekranni tozalash
        screen.fill(BLACK)
        all_sprites.draw(screen)

        pygame.display.flip()
        pygame.time.delay(30)

    pygame.quit()

if __name__ == "__main__":
    main()
