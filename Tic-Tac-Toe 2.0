import pygame, sys
import numpy as np

pygame.init()

# Board setup
WIDTH = 600
HEIGHT = WIDTH
LINE_WIDTH = 15
WIN_LINE_WIDTH = 20
BOARD_ROWS = 3
BOARD_COLS = 3
SQUARE_SIZE = WIDTH // BOARD_COLS
CIRCLE_RADIUS = SQUARE_SIZE // 3
CIRCLE_WIDTH = 15
CROSS_WIDTH = 20
SPACE = SQUARE_SIZE // 4

# Colors (Google Tic Tac Toe style)
BG_COLOR = (26, 188, 156)      # teal
LINE_COLOR = (22, 160, 133)    # darker teal
CIRCLE_COLOR = (255, 244, 224) # cream white
CROSS_COLOR = (83, 79, 79)     # dark gray
WINNER_COLOR = CROSS_COLOR      # Winner text always matches X color

# Screen setup
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption('Google Style Tic Tac Toe')
screen.fill(BG_COLOR)

# Board state
board = np.zeros((BOARD_ROWS, BOARD_COLS))

def draw_lines():
    pygame.draw.line(screen, LINE_COLOR, (0, SQUARE_SIZE), (WIDTH, SQUARE_SIZE), LINE_WIDTH)
    pygame.draw.line(screen, LINE_COLOR, (0, 2 * SQUARE_SIZE), (WIDTH, 2 * SQUARE_SIZE), LINE_WIDTH)
    pygame.draw.line(screen, LINE_COLOR, (SQUARE_SIZE, 0), (SQUARE_SIZE, HEIGHT), LINE_WIDTH)
    pygame.draw.line(screen, LINE_COLOR, (2 * SQUARE_SIZE, 0), (2 * SQUARE_SIZE, HEIGHT), LINE_WIDTH)

def draw_figures():
    for row in range(BOARD_ROWS):
        for col in range(BOARD_COLS):
            if board[row][col] == 1:
                pygame.draw.circle(screen, CIRCLE_COLOR,
                                   (int(col * SQUARE_SIZE + SQUARE_SIZE//2),
                                    int(row * SQUARE_SIZE + SQUARE_SIZE//2)),
                                   CIRCLE_RADIUS, CIRCLE_WIDTH)
            elif board[row][col] == 2:
                pygame.draw.line(screen, CROSS_COLOR,
                                 (col * SQUARE_SIZE + SPACE, row * SQUARE_SIZE + SPACE),
                                 (col * SQUARE_SIZE + SQUARE_SIZE - SPACE, row * SQUARE_SIZE + SQUARE_SIZE - SPACE),
                                 CROSS_WIDTH)
                pygame.draw.line(screen, CROSS_COLOR,
                                 (col * SQUARE_SIZE + SPACE, row * SQUARE_SIZE + SQUARE_SIZE - SPACE),
                                 (col * SQUARE_SIZE + SQUARE_SIZE - SPACE, row * SQUARE_SIZE + SPACE),
                                 CROSS_WIDTH)

def mark_square(row, col, player):
    board[row][col] = player

def available_square(row, col):
    return board[row][col] == 0

def is_board_full():
    return not (board == 0).any()

def animate_line(start, end, player):
    color = CIRCLE_COLOR if player == 1 else CROSS_COLOR
    steps = 50
    for i in range(1, steps+1):
        x = start[0] + (end[0] - start[0]) * i / steps
        y = start[1] + (end[1] - start[1]) * i / steps
        screen.fill(BG_COLOR)
        draw_lines()
        draw_figures()
        pygame.draw.line(screen, color, start, (int(x), int(y)), WIN_LINE_WIDTH)
        pygame.display.update()
        pygame.time.delay(15)

def show_winner(player, win_squares):
    """ Animate all winning squares combining to the center and display winner text """
    center_x = WIDTH // 2
    center_y = HEIGHT // 2
    steps = 30
    square_positions = []
    for (row, col) in win_squares:
        x = col * SQUARE_SIZE + SQUARE_SIZE // 2
        y = row * SQUARE_SIZE + SQUARE_SIZE // 2
        square_positions.append([x, y])

    # Animate winning squares moving toward center
    for i in range(1, steps + 1):
        screen.fill(BG_COLOR)
        draw_lines()
        for pos in square_positions:
            x = int(pos[0] + (center_x - pos[0]) * i / steps)
            y = int(pos[1] + (center_y - pos[1]) * i / steps)
            if player == 1:
                pygame.draw.circle(screen, CIRCLE_COLOR, (x, y), CIRCLE_RADIUS, CIRCLE_WIDTH)
            else:
                pygame.draw.line(screen, CROSS_COLOR,
                                 (x - CIRCLE_RADIUS, y - CIRCLE_RADIUS),
                                 (x + CIRCLE_RADIUS, y + CIRCLE_RADIUS), CROSS_WIDTH)
                pygame.draw.line(screen, CROSS_COLOR,
                                 (x - CIRCLE_RADIUS, y + CIRCLE_RADIUS),
                                 (x + CIRCLE_RADIUS, y - CIRCLE_RADIUS), CROSS_WIDTH)
        pygame.display.update()
        pygame.time.delay(30)

    # Draw proportional symbol in center (0.9× normal size)
    symbol_size = int(CIRCLE_RADIUS * 0.9)
    screen.fill(BG_COLOR)
    draw_lines()
    if player == 1:
        pygame.draw.circle(screen, CIRCLE_COLOR, (center_x, center_y), symbol_size, CIRCLE_WIDTH)
    else:
        pygame.draw.line(screen, CROSS_COLOR,
                         (center_x - symbol_size, center_y - symbol_size),
                         (center_x + symbol_size, center_y + symbol_size), CROSS_WIDTH)
        pygame.draw.line(screen, CROSS_COLOR,
                         (center_x - symbol_size, center_y + symbol_size),
                         (center_x + symbol_size, center_y - symbol_size), CROSS_WIDTH)

    # Winner text below symbol (always X color)
    font = pygame.font.SysFont(None, 60)
    winner_text = font.render("WINNER", True, WINNER_COLOR)
    text_rect = winner_text.get_rect(center=(center_x, center_y + 80))
    screen.blit(winner_text, text_rect)
    pygame.display.update()



def animate_draw():
    positions = [(r, c) for r in range(BOARD_ROWS) for c in range(BOARD_COLS)]
    center_x = WIDTH // 2
    center_y = HEIGHT // 2
    steps = 20

    for _ in range(3):
        screen.fill((255, 255, 255))
        draw_lines()
        draw_figures()
        pygame.display.update()
        pygame.time.delay(200)
        screen.fill(BG_COLOR)
        draw_lines()
        draw_figures()
        pygame.display.update()
        pygame.time.delay(200)

    for i in range(1, steps + 1):
        screen.fill(BG_COLOR)
        draw_lines()
        for (row, col) in positions:
            x = col * SQUARE_SIZE + SQUARE_SIZE // 2
            y = row * SQUARE_SIZE + SQUARE_SIZE // 2
            x = int(x + (center_x - x) * i / steps)
            y = int(y + (center_y - y) * i / steps)
            if board[row][col] == 1:
                pygame.draw.circle(screen, CIRCLE_COLOR, (x, y), CIRCLE_RADIUS, CIRCLE_WIDTH)
            elif board[row][col] == 2:
                pygame.draw.line(screen, CROSS_COLOR,
                                 (x - CIRCLE_RADIUS, y - CIRCLE_RADIUS),
                                 (x + CIRCLE_RADIUS, y + CIRCLE_RADIUS), CROSS_WIDTH)
                pygame.draw.line(screen, CROSS_COLOR,
                                 (x - CIRCLE_RADIUS, y + CIRCLE_RADIUS),
                                 (x + CIRCLE_RADIUS, y - CIRCLE_RADIUS), CROSS_WIDTH)
        pygame.display.update()
        pygame.time.delay(30)

    font = pygame.font.SysFont(None, 80)
    text = font.render("DRAW", True, (255, 255, 255))
    text_rect = text.get_rect(center=(center_x, center_y))
    screen.blit(text, text_rect)
    pygame.display.update()

def check_win(player):
    win_squares = []
    # Vertical
    for col in range(BOARD_COLS):
        if board[0][col] == player and board[1][col] == player and board[2][col] == player:
            win_squares = [(0, col), (1, col), (2, col)]
            animate_line((col * SQUARE_SIZE + SQUARE_SIZE//2, 15),
                         (col * SQUARE_SIZE + SQUARE_SIZE//2, HEIGHT - 15),
                         player)
            show_winner(player, win_squares)
            return True
    # Horizontal
    for row in range(BOARD_ROWS):
        if board[row][0] == player and board[row][1] == player and board[row][2] == player:
            win_squares = [(row, 0), (row, 1), (row, 2)]
            animate_line((15, row * SQUARE_SIZE + SQUARE_SIZE//2),
                         (WIDTH - 15, row * SQUARE_SIZE + SQUARE_SIZE//2),
                         player)
            show_winner(player, win_squares)
            return True
    # Asc diagonal
    if board[2][0] == player and board[1][1] == player and board[0][2] == player:
        win_squares = [(2,0),(1,1),(0,2)]
        animate_line((15, HEIGHT - 15), (WIDTH - 15, 15), player)
        show_winner(player, win_squares)
        return True
    # Desc diagonal
    if board[0][0] == player and board[1][1] == player and board[2][2] == player:
        win_squares = [(0,0),(1,1),(2,2)]
        animate_line((15, 15), (WIDTH - 15, HEIGHT - 15), player)
        show_winner(player, win_squares)
        return True
    return False

def restart():
    screen.fill(BG_COLOR)
    draw_lines()
    for row in range(BOARD_ROWS):
        for col in range(BOARD_COLS):
            board[row][col] = 0

draw_lines()
player = 1
game_over = False
winner = None

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            sys.exit()

        if event.type == pygame.MOUSEBUTTONDOWN and not game_over:
            mouseX = event.pos[0]
            mouseY = event.pos[1]
            clicked_row = int(mouseY // SQUARE_SIZE)
            clicked_col = int(mouseX // SQUARE_SIZE)
            if available_square(clicked_row, clicked_col):
                mark_square(clicked_row, clicked_col, player)
                draw_figures()
                if check_win(player):
                    game_over = True
                    winner = player
                elif is_board_full():
                    animate_draw()
                    game_over = True
                else:
                    player = 2 if player == 1 else 1

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_r:
                restart()
                player = 1
                game_over = False
                winner = None

    pygame.display.update()
