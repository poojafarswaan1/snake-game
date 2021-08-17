# snake-game
snake eats the food then length of snake will increase.

import pygame
import random

red=(255,0,0)
green=(0,255,0)
blue=(0,0,255)
black=(0,0,0)
white=(255,255,255)

width = 300
height = 400
fps = 30
exit_game=False
game_over=False
snake_x=50
snake_y=50
snake_size=15
food_x=random.randint(0,width)
food_y=random.randint(0,width)
food_size=8 
vel_x=0
vel_y=0
score=0
snake_list=[]
snake_length=1


pygame.init()
pygame.mixer.init()
win = pygame.display.set_mode((width, height))
pygame.display.set_caption("SNAKE GAME BY POOJA")
clock = pygame.time.Clock()

def mytext(text,color,x,y):
    font=pygame.font.SysFont('arial',25)
    screentext=font.render(text,True,color)
    win.blit(screentext,(x,y))

def plotsnake(window,color,snake_list,snake_size):
    for x,y in snake_list:
        pygame.draw.rect(window,color,(x,y,snake_size,snake_size))

while not exit_game:

    if game_over:
        win.fill(white)
        mytext("Game Over" ,blue,100,150)

        
        for event in pygame.event.get():
          if event.type == pygame.QUIT:
            exit_game=True


        clock.tick(fps)
        pygame.display.update()

            

    else:
        
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                exit_game=True
                
            if event.type == pygame.KEYDOWN:
                 if event.key == pygame.K_UP:
                     vel_y = -5
                     vel_x=0

                 if event.key == pygame.K_DOWN:
                     vel_y = 5
                     vel_x=0


                 if event.key == pygame.K_LEFT:
                     vel_y = 0
                     vel_x=-5

                 if event.key == pygame.K_RIGHT:
                     vel_y = 0
                     vel_x=5  


        snake_x=snake_x+vel_x
        snake_y=snake_y+vel_y

        if abs(snake_x-food_x)<5 and abs(snake_y-food_y)<5:
            score=score+10
            food_x=random.randint(0,width)
            food_y=random.randint(0,width)
            snake_length=snake_length+5

        head=[]
        head.append(snake_x)
        head.append(snake_y)
        snake_list.append(head)

        if len(snake_list)>snake_length:
            del snake_list[0]

        if head in snake_list[: -1]:
            game_over=True

        if snake_x<0 or snake_x>width or snake_y<0 or snake_y>height:
            game_over=True
            
        win.fill(black )
        mytext("score : " + str(score),blue,5,5)
        plotsnake(win,green,snake_list,snake_size)
        pygame.draw.rect(win,white,(food_x,food_y,food_size,food_size))

        clock.tick(fps)
        pygame.display.update()

pygame.quit()
quit()



