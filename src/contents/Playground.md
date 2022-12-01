---
author: Milan tavernier
datetime: 2022-12-29T10:57:00Z
title: The Playground
slug: the-playground
featured: true
draft: false
tags:
  - docs
  - game
  - pong
ogImage: ""
description: Here, you can play some games in the site !
---

# Pong

<script type="text/python">
from gamebuino_meta import begin, waitForUpdate, display, color, buttons, collide

# Taille, vitesse et position initiale de la balle :
ball_size = 3
ball_x_speed = 1
ball_y_speed = 1
ball_x_position = 20
ball_y_position = 20

# Taille initiale de la raquette du joueur :
player_height = 12
player_width = 3
player_speed = 2

# Position initiale de la raquette :
player_x_position = 10
player_y_position = 30

# Score
score = 0

while True:
    waitForUpdate()
    display.clear()

    # Si on presse les boutons UP ou DOWN, nous déplaçons la raquette vers le haut, ou vers le bas :
    if buttons.repeat(buttons.UP, 0):
        player_y_position = player_y_position - player_speed

    if buttons.repeat(buttons.DOWN, 0):
        player_y_position = player_y_position + player_speed

    # Nous déplaçons la balle
    ball_x_position = ball_x_position + ball_x_speed
    ball_y_position = ball_y_position + ball_y_speed

    # Vérification si la balle entre en collision avec le haut, bas ou droite de l'écran
    # Si c'est le cas, nous inversons sa direction
    if ball_y_position <= 0:
        ball_y_speed = -ball_y_speed

    if ball_y_position >= 64 - ball_size:
        ball_y_speed = -ball_y_speed

    if ball_x_position + ball_size >= 80:
        ball_x_speed = -ball_x_speed

    # Nous testons s'il y a collision entre la balle et la raquette du joueur
    if collide.rectRect(ball_x_position, ball_y_position, ball_size, ball_size, 
                        player_x_position, player_y_position, player_width, player_height):
        ball_x_speed = -ball_x_speed
        score = score + 1

    # Vérifier si la balle est sortie de l'écran
    if ball_x_position <= 0:
        score = 0  # Nous remettons le score à 0
        ball_x_speed = -ball_x_speed
				
    # Empêcher la raquette de sortir de l'écran
    if player_y_position <= 0:
        player_y_position = 0
    
    if player_y_position >= 64 - player_height:
        player_y_position = 64 - player_height

    # Affichage de la balle
    display.fillRect(ball_x_position, ball_y_position, ball_size, ball_size)

    # Affichage de la raquette du joueur
    display.fillRect(player_x_position, player_y_position, player_width, player_height)
</script>
