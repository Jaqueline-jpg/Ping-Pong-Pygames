

  <h1 align="center">Jogo de Ping Pong 🏓 </h1>

### Este é um projeto desenvolvido em aula de forma simples do jogo Pong implementado em Python usando a biblioteca Pygame.

![Fig.gsif](img/Ping-Pong.gif)

## Requisitos necessários
##### - Python 3.x e Pygame

# Instrução para a instação dos pacotes:⤵

```bash
pip install -r requirements.txt
```

### -Executando o jogo ▶

```bash
python main.py
```

### - Criar um executável
```python
# Instalar o pacote pyInstaller
pyinstaller --onefile ping-pong.py
```

## Estrutura do Código ⤵

### O código está dividido em dois arquivos principais:

##### - main.py: É o ponto de entrada do jogo. Inicializa o jogo e entra no loop principal.

##### - pong_classes.py: Define as classes principais do jogo, como Paddle, Ball e Game.
----------------------
# Set das variáveis
```python
import pygame
from pygame import mixer
import sys

#As linhas de código abaixo são usadas para 
#inicializar as bibliotecas Pygame e Mixer, respectivamente. Essas 
#funções devem ser chamadas no início do programa antes de usar os
#recursos dessas bibliotecas.
pygame.init()
mixer.init()

#Essas linhas de código definem constantes relacionadas ao tamanho da 
#tela, dimensões das raquetes e da bola, além das velocidades de movimento
# da raquete e da bola. Essas constantes são usadas para configurar o jogo 
#com os valores desejados
SCREEN_WIDTH =800
SCREEN_HEIGHT = 600
PADDLE_WIDTH = 10
PADDLE_HEIGHT = 60
BALL_SIZE = 10
PADDLE_SPEED = 4
BALL_SPEED = 5

WHITE = (255,255,255)
BLACK = (0,0,0)

font_file = "add path"
font = pygame.font.Font(font_file, 36)
score_a = 0
score_b = 0

mixer.music.load("add path")
mixer.music.set_volume(0.3)
collision_sound_A = mixer.Sound("add path")
collision_sound_B = mixer.Sound("add path")
point_sound = mixer.Sound("add path")

#a linha abixo sa a função play() do módulo Mixer do Pygame para
#reproduzir uma música em loop infinito.
mixer.music.play(-1) 

#Esse código cria uma janela de exibição na tela com uma largura e altura
screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT)) 

#Esse código define o título da janela do jogo como "Pong".
pygame.display.set_caption("Pong") 


#Neste trecho de código, são criados retângulos que representam as 
#raquetes e a bola do jogo Pong. As raquetes são posicionadas nas laterais
#da tela, enquanto a bola é posicionada no centro. As variáveis ball_dx e
#ball_dy controlam as velocidades horizontal e vertical da bola, 
# respectivamente, usando a constante BALL_SPEED.
paddle_a = pygame.Rect(20, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT//2, PADDLE_WIDTH, PADDLE_HEIGHT)
paddle_b = pygame.Rect(SCREEN_WIDTH - 20 - PADDLE_WIDTH, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT//2, PADDLE_WIDTH, PADDLE_HEIGHT)
ball =  pygame.Rect(SCREEN_WIDTH //2 - BALL_SIZE // 2, SCREEN_HEIGHT // 2 - BALL_SIZE//2, BALL_SIZE, BALL_SIZE)
ball_dx, ball_dy = BALL_SPEED, BALL_SPEED

```

# Renderização do Menu

```python
def main_menu():
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    game_loop()
                elif event.key == pygame.K_ESCAPE:
                    pygame.quit()
                    sys.exit()

        # Renderização do menu principal
        screen.fill(BLACK)
        title_font = pygame.font.Font(font_file, 36)  # Configuração da Fonte
        title_text = title_font.render("Pong", True, WHITE)
        title_rect = title_text.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4))

        screen.blit(title_text, title_rect) #Nesse código, um texto é exibido na tela do jogo.

        title_font = pygame.font.Font(font_file, 16)
        current_time = pygame.time.get_ticks() #Nesse código, uma fonte de texto é definida e o tempo atual do jogo é obtido.

        if current_time % 2000 < 1000:
            title_text1 = title_font.render("Pressione espaço para iniciar", True, WHITE)
            title_rect1 = title_text1.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4 + 60)) #Nesse código, são definidas as coordenadas de posicionamento de um objeto na tela.
            screen.blit(title_text1, title_rect1) #Nesse código, um texto é exibido em uma determinada posição na tela do jogo.
        
        pygame.display.flip()
```
#### Explicação da Estrutura a seguir:

```python
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    game_loop()
                elif event.key == pygame.K_ESCAPE:
                    pygame.quit()
                    sys.exit()
```

###### A estrutura de código fornecida cria um loop infinito que captura e trata eventos do Pygame. Permite capturar eventos do Pygame, como ações do usuário (como fechar a janela ou pressionar teclas), e tomar as medidas apropriadas em resposta a esses eventos. Vamos analisar a estrutura em detalhes:
    1. O loop while True: garante que o código dentro dele seja executado repetidamente até que o programa seja encerrado.

    2. A linha for event in pygame.event.get(): itera sobre todos os eventos capturados pelo Pygame no momento.

    3. O primeiro if verifica se o evento atual é do tipo pygame.QUIT, que é acionado quando o usuário fecha a janela do jogo. Nesse caso, as funções pygame.quit() e sys.exit() são chamadas para encerrar o jogo corretamente.

    4. O próximo if verifica se o evento atual é do tipo pygame.KEYDOWN, que é acionado quando uma tecla é pressionada. Em seguida, são verificadas as teclas específicas pressionadas:
###### Se a tecla pressionada for a tecla de espaço (pygame.K_SPACE), a função game_loop() é chamada. Presume-se que essa função seja responsável por iniciar ou reiniciar o loop principal do jogo.
###### Se a tecla pressionada for a tecla de escape (pygame.K_ESCAPE), as funções pygame.quit() e sys.exit() são chamadas para encerrar o jogo. 

</blockquote>

###### Abaixo podemos ver que esse bloco funciona da seguinte forma:
```python
current_time = pygame.time.get_ticks()
```
###### A função é chamada para obter o tempo em milissegundos desde que o jogo começou.

```python
if current_time % 2000 < 1000:
```
###### O trecho de código verifica se o resto da divisão da variável *current_time* por 2000 é menor que 1000. Se essa condição for verdadeira, significa que *current_time* está dentro do intervalo de 0 a 999 milissegundos após cada múltiplo de 2000 milissegundos. Essa verificação é usada para criar um efeito piscante.

# Game

  ```python
def game_loop():
    global ball_dx, ball_dy, score_a, score_b, ball #game_loop(), representa o loop principal do 
    #jogo. Ela opera em um escopo global e é 
    #responsável por controlar variáveis como 
    #ball_dx, ball_dy, score_a, score_b e ball.

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    return

        #retângulos brancos são desenhados nas 
        #posições das raquetes (paddle_a e paddle_b) 
        #e uma elipse branca é desenhada na posição da bola (ball).
        screen.fill(BLACK) 
        pygame.draw.rect(screen, WHITE, paddle_a)
        pygame.draw.rect(screen, WHITE, paddle_b)
        pygame.draw.ellipse(screen, WHITE, ball)
        pygame.draw.aaline(screen, WHITE, (SCREEN_WIDTH // 2, 0), (SCREEN_WIDTH // 2, SCREEN_HEIGHT))

        #para verificar quais teclas estão sendo pressionadas no momento
        keys = pygame.key.get_pressed()

        #Movimento Vertical Raquete A
        if keys[pygame.K_w] and paddle_a.top > 0:
            paddle_a.y -= PADDLE_SPEED
        if keys[pygame.K_s] and paddle_a.bottom < SCREEN_HEIGHT:
            paddle_a.y += PADDLE_SPEED

        #Movimento Vertical Raquete B
        if keys[pygame.K_UP] and paddle_b.top > 0:
            paddle_b.y -= PADDLE_SPEED
        if keys[pygame.K_DOWN] and paddle_b.bottom < SCREEN_HEIGHT:
            paddle_b.y += PADDLE_SPEED

        #Movimento Horizontal Raquete A
        if keys[pygame.K_a] and paddle_a.left > 0:
            paddle_a.x -= PADDLE_SPEED
        if keys[pygame.K_d] and paddle_a.right < SCREEN_WIDTH // 2 - 70:
            paddle_a.x += PADDLE_SPEED

        #Movimento Horizontal Raquete B
        if keys[pygame.K_UP] and paddle_b.left > 0:
            paddle_b.x -= PADDLE_SPEED
        if keys[pygame.K_DOWN] and paddle_b.right < SCREEN_WIDTH // 2 - 70:
            paddle_b.x += PADDLE_SPEED
      
        # Atualização da posição da bola
        ball.x += ball_dx
        ball.y += ball_dy


        if ball.colliderect(paddle_a):
            ball.left = paddle_a.right
            ball_dx = -ball_dx
            collision_sound_A.play()

        elif ball.colliderect(paddle_b):
            ball.right = paddle_b.left
            ball_dx = -ball_dx
            collision_sound_B.play()

        #Bola quando bate na extremidade da tela
        if ball.top <= 0 or ball.bottom >= SCREEN_HEIGHT:
            ball_dy = -ball_dy

        #Ponto para o Time B
        if ball.left <= 0:
            score_b += 1
            ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
            ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
            ball_dx = -ball_dx
            point_sound.play()
            # print(score_b)
            if score_b == 10: #Comente
                end_game(False)

        #Ponto para o Time A
        elif ball.right >= SCREEN_WIDTH:
            score_a += 1
            ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
            ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
            ball_dx = -ball_dx
            point_sound.play()
            # print(score_a)
            if score_a == 10: #Comente
                end_game(True)

        # Placar na Tela
        score_text = font.render(f"{score_a}  {score_b}", True, WHITE)
        score_rect = score_text.get_rect(center=(SCREEN_WIDTH // 2, 30))
        screen.blit(score_text, score_rect)

        # Atualizar a tela
        pygame.display.flip()

        # Controlar FPS
        clock = pygame.time.Clock()
        clock.tick(60)
```
  # Explicação Game
  ## Movimento Horizontal e vertical
  ###### Movimento Vertical:
  ###### Para o movimento vertical da raquete A (paddle_a), é verificado se as teclas "W" e "S" estão sendo pressionadas (keys[pygame.K_w] e keys[pygame.K_s]). Além disso, é verificado se a posição atual da raquete não ultrapassa os limites da tela (superior e inferior).
  ###### Se a tecla "W" for pressionada e a posição superior da raquete for maior que zero (paddle_a.top > 0), a posição vertical da raquete é diminuída (paddle_a.y -= PADDLE_SPEED), movendo-a para cima na tela.
  ###### Da mesma forma, se a tecla "S" for pressionada e a posição inferior da raquete for menor que a altura da tela (paddle_a.bottom < SCREEN_HEIGHT), a posição vertical da raquete é aumentada (paddle_a.y += PADDLE_SPEED), movendo-a para baixo na tela.

  ###### O movimento vertical da raquete B (paddle_b) é semelhante, mas usa as teclas de seta para cima e para baixo (pygame.K_UP e pygame.K_DOWN) e verifica as posições superior e inferior da raquete B (paddle_b.top e paddle_b.bottom).

###### Movimento Horizontal:

###### Para o movimento horizontal da raquete A (paddle_a), é verificado se as teclas "A" e "D" estão sendo pressionadas (keys[pygame.K_a] e keys[pygame.K_d]). Além disso, é verificado se a posição atual da raquete não ultrapassa a metade esquerda da tela menos 70 pixels (paddle_a.right < SCREEN_WIDTH // 2 - 70).

###### Se a tecla "A" for pressionada e a posição esquerda da raquete for maior que zero (paddle_a.left > 0), a posição horizontal da raquete é diminuída (paddle_a.x -= PADDLE_SPEED), movendo-a para a esquerda na tela.

###### Da mesma forma, se a tecla "D" for pressionada e a posição direita da raquete for menor que a metade esquerda da tela menos 70 pixels (paddle_a.right < SCREEN_WIDTH // 2 - 70), a posição horizontal da raquete é aumentada (paddle_a.x += PADDLE_SPEED), movendo-a para a direita na tela.

###### O movimento horizontal da raquete B (paddle_b) é semelhante, mas usa as teclas de seta para a esquerda e para a direita (pygame.K_LEFT e pygame.K_RIGHT) e verifica as posições esquerda e direita da raquete B (paddle_b.left e paddle_b.right).


## Sistema de Pontuação
```python
# Ponto para o Time A
elif ball.right >= SCREEN_WIDTH:
    score_a += 1
    ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
    ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
    ball_dx = -ball_dx
    point_sound.play()
    if score_a == 10:
        end_game(True)
```
##### Quando a bola ultrapassa a raquete B e o ponto é marcado para o Time A, a posição da bola é redefinida no centro da tela. O contador de pontos do Time A é incrementado em 1, e a direção horizontal da bola é invertida. Um som de ponto é reproduzido. Se o Time A atingir a pontuação máxima de 10 pontos, o jogo é encerrado com a vitória do Time A.

```python
# Ponto para o Time B
if ball.left <= 0:
    score_b += 1
    ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
    ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
    ball_dx = -ball_dx
    point_sound.play()
    if score_b == 10:
        end_game(False)
```
##### Quando a bola ultrapassa a raquete A e o ponto é marcado para o Time B, a posição da bola é redefinida no centro da tela. O contador de pontos do Time B é incrementado em 1, e a direção horizontal da bola é invertida. Um som de ponto é reproduzido. Se o Time B atingir a pontuação máxima de 10 pontos, o jogo é encerrado com a vitória do Time A.

#Fim de Jogo
```python
def end_game(winner): 
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    reset_game()
                    return
                elif event.key == pygame.K_ESCAPE:
                    pygame.quit()
                    sys.exit()

       # Essas linhas de código são responsáveis por 
       # parar a música, limpar a tela e definir qual 
       # mensagem de vitória será exibida com base no 
       # valor da variável winner.
        mixer.music.stop()
        screen.fill(BLACK)
        if winner:
            winner_text = "Player 2 Wins!"
        else:
            winner_text = "Player 1 Wins!"

        # Renderização da tela de fim de jogo
        winner_font = pygame.font.Font(font_file, 36)
        winner_render = winner_font.render(winner_text, True, WHITE)
        winner_rect = winner_render.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4))
        screen.blit(winner_render, winner_rect)
        pygame.display.flip()
```
##### A função end_game(winner) exibe a tela de fim de jogo, mostrando a mensagem de vitória da equipe vencedora e permite reiniciar o jogo ou encerrar o programa.

# Reiniciando o Jogo
```python
def reset_game():
    global paddle_a, paddle_b, ball, ball_dx, ball_dy, score_a, score_b

    paddle_a = pygame.Rect(20, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT // 2, PADDLE_WIDTH, PADDLE_HEIGHT)
    paddle_b = pygame.Rect(SCREEN_WIDTH - 20 - PADDLE_WIDTH, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT // 2, PADDLE_WIDTH, PADDLE_HEIGHT)
    ball = pygame.Rect(SCREEN_WIDTH // 2 - BALL_SIZE // 2, SCREEN_HEIGHT // 2 - BALL_SIZE // 2, BALL_SIZE, BALL_SIZE)
    ball_dx, ball_dy = BALL_SPEED, BALL_SPEED
    score_a, score_b = 0, 0
```
##### De forma resumida do código acima, quando a função reset_game() é chamada, ela redefine todas as variáveis do jogo para seus valores iniciais, preparando o jogo para um novo início. 


------------
Jaqueline ✌️

