# Game3
import pygame
import random
pygame.init()
screen_x = 800
screen_y = 800
screen = pygame.display.set_mode((screen_x, screen_y))
clock = pygame.time.Clock()
done = False
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
WHITE = (255, 255, 255)
colours = [WHITE, BLUE, RED]
squares = []
square_width = 80

class Square():
    def __init__(self, x, y, x_c, y_c):
        self.x = x
        self.y = y
        self.square_pos_x = x_c
        self.square_pos_y = y_c
        self.colour_number = 0
        self.rect = pygame.Rect(self.x, self.y, square_width, square_width)
    def draw(self):
        pygame.draw.rect(screen, colours[self.colour_number % 3], (self.x, self.y, square_width, square_width))
for i in range(10):
    for j in range(10):
        squares.append(Square(i * square_width, j * square_width, i + 1, j + 1))
        
def draw_lines():
    for i in range(10):
        pygame.draw.rect(screen, BLACK, (0, i * square_width, screen_x, 1))
        pygame.draw.rect(screen, BLACK, (i * square_width, 0, 1, screen_y))
while not done:
    clock.tick(25)
    screen.fill(WHITE)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True
        if event.type == pygame.MOUSEBUTTONDOWN:
            x, y = event.pos
            for sq in squares:
                if sq.rect.collidepoint(x, y):
                    sq.colour_number += 1
                    print(sq.square_pos_x, sq.square_pos_y)
    for sq in squares:
        sq.draw()
    draw_lines()
    pygame.display.flip()
pygame.quit()
