import pygame
import random
import sys

# Inicializa o Pygame
pygame.init()

# Tela
largura = 400
altura = 600
tela = pygame.display.set_mode((largura, altura))
pygame.display.set_caption("Flappy Bird")

# Cores
BRANCO = (255, 255, 255)
AZUL = (0, 150, 255)
VERDE = (0, 200, 0)
VERMELHO = (255, 0, 0)

# Relógio
clock = pygame.time.Clock()

# Fonte
fonte = pygame.font.SysFont(None, 48)

# Jogador
passaro_x = 50
passaro_y = altura // 2
gravidade = 0.5
velocidade = 0
pulo = -10

# Cano
cano_largura = 70
cano_altura = random.randint(150, 400)
cano_x = largura
espaco_entre_canos = 200

# Pontuação
pontos = 0

def desenhar_passaro(y):
    pygame.draw.circle(tela, VERMELHO, (passaro_x, int(y)), 15)

def desenhar_canos(x, altura):
    pygame.draw.rect(tela, VERDE, (x, 0, cano_largura, altura))
    pygame.draw.rect(tela, VERDE, (x, altura + espaco_entre_canos, cano_largura, altura))

def mostrar_pontos(pontos):
    texto = fonte.render(str(pontos), True, BRANCO)
    tela.blit(texto, (largura // 2 - texto.get_width() // 2, 20))

# Game loop
while True:
    tela.fill(AZUL)

    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        if evento.type == pygame.KEYDOWN:
            if evento.key == pygame.K_SPACE:
                velocidade = pulo

    # Lógica do passaro
    velocidade += gravidade
    passaro_y += velocidade

    # Lógica dos canos
    cano_x -= 5
    if cano_x < -cano_largura:
        cano_x = largura
        cano_altura = random.randint(100, 400)
        pontos += 1

    # Colisões
    if passaro_y < 0 or passaro_y > altura:
        print("Game Over!")
        pygame.quit()
        sys.exit()

    if passaro_x + 15 > cano_x and passaro_x - 15 < cano_x + cano_largura:
        if passaro_y - 15 < cano_altura or passaro_y + 15 > cano_altura + espaco_entre_canos:
            print("Game Over!")
            pygame.quit()
            sys.exit()

    # Desenha tudo
    desenhar_passaro(passaro_y)
    desenhar_canos(cano_x, cano_altura)
    mostrar_pontos(pontos)

    pygame.display.update()
    clock.tick(60)