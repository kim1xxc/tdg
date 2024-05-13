# tdgimport pygame 
import winsound
from player import player
from fire import fireball
from NPC import npc
#from enemy import enemy
pygame.init()
pygame.display.set_caption("top down grid game")
screen = pygame.display.set_mode((1200, 800))
clock = pygame.time.Clock()
gameover = False
mapNum = 1
winsound.PlaySound('life.wav', 0)
p1 = player()
ball = fireball()
bob = npc()
ticker = 0
#constantsw
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
SPACE = 4
w = 5
keys = [False,False,False,False, False]


map = [[2,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,0,0,2,2,4,0,2,0,0,0,0,3,0,2,2,2,2,0,0,0,2],
       [2,0,0,0,0,2,2,0,0,2,0,2,2,2,2,0,0,0,0,2,0,0,0,2],
       [2,0,0,2,2,2,2,0,0,2,0,2,4,0,0,0,2,2,0,2,0,0,0,2],
       [2,2,0,0,0,0,0,0,0,2,0,2,2,0,0,0,0,0,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,2,0,2,0,0,2,0,2,2,2,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,0,0,0,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,2,2,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,3,0,2,0,0,2,2,2,0,0,2,0,0,0,2],
       [2,2,2,3,2,2,2,2,2,2,2,2,0,0,0,0,0,1,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,2,2,2,2,2,3,2,0,0,0,2],
       [2,3,2,2,2,2,0,2,2,2,2,2,2,2,2,2,2,2,0,2,0,0,0,2],
       [2,0,2,0,2,0,0,2,2,4,0,1,0,0,0,0,0,2,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,2,2,2,2,2,2,2,2,2,3,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,5],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]

map2 = [[2,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,0,0,0,0,0,0,2,2,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,2,0,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]


wall = pygame.image.load('wall.png')
brick = pygame.image.load('brick.png')
door = pygame.image.load('door.png')
chest = pygame.image.load('chest.png')
exitdoor = pygame.image.load('exit.door.png')


while not gameover:
    clock.tick(60)
    ticker +=1

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            gameover = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = True
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = True
            elif event.key == pygame.K_UP:
                keys[UP] = True
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = True
            elif event.key == pygame.K_SPACE:
                keys[SPACE] = True
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = False
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = False
            elif event.key == pygame.K_UP:
                keys[UP] = False
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = False
            elif event.key == pygame.K_SPACE:
                keys[SPACE] = False    
        
 #physics-----------------------------------------------------------------------------------------
    ball.move()
    p1.move(keys, map)
   
    bob.move(map,ticker,p1.xpos,p1.ypos)

    if mapNum == 1:
        if map[int((p1.ypos ) / 50)][int( (p1.xpos) / 50)] ==5:
            mapNum = 2
            p1.xpos = 50
    
    if mapNum == 2:
        if map2[int((p1.ypos ) / 50)][int( (p1.xpos) / 50)] ==5:
            map2Num = 1
            p1.xpos = 1100

    
   
    if mapNum == 1:
        p1.move(keys , map)
    elif mapNum ==2:
        p1.move(keys , map2)
    
    if keys[SPACE] == True:
        print(p1.direction)
        ball.shoot(p1.xpos, p1.ypos, p1.direction)
    

 #renders-----------------------------------------------------------------------------------------
    


    screen.fill((0,0,0))

    p1.draw(screen)
    

    #draw FIRE
    if ball.isAlive == True:
        ball.draw(screen)
    if mapNum == 1:
        for i in range(16):
                for j in range(24):
                    if map[i][j] == 2:
                        screen.blit(brick, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 1:
                        screen.blit(wall, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 3:
                        screen.blit(door, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 4:
                        screen.blit(chest, (j * 50, i * 50), (0, 0, 50, 50))
                    if<


#######################fireball

import pygame
import math
#constants
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
SPACE = 4
W = 5 

class fireball:
    def __init__(self):
        self.xpos = - 10
        self.ypos = -10
        self.isAlive = False
        self.direction = RIGHT

    def shoot(self, x, y, dir):
        self.xpos = x + 20
        self.ypos = y + 20
        self.isAlive = True
        self.direction = dir
        print("direction is ", dir, "in shoot")

    def move(self):
        print("direction is ", self.direction)
        if self.direction == RIGHT:
            self.xpos+=20
        elif self.direction == LEFT:
            self.xpos-=20
        if self.direction == DOWN:
            self.ypos+=20
        elif self.direction == UP:
            self.ypos-=20

    
    def draw(self, screen):
        pygame.draw.circle(screen, (250, 0, 0), (self.xpos, self.ypos), 10)
        pygame.draw.circle(screen, (250, 250, 0), (self.xpos, self.ypos), 5)

    def collide(self, x, y):
        #distance formula for circular collision
        if math.sqrt((self.xpos - x) ** 2 + (self.ypos - y) ** 2) < 25:
            print("collision!")
            return True
        else:
            return False

#npc###########################################################

import pygame
import random
import math
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3

class npc:
    def __init__(self):
        self.xpos = 100
        self.ypos = 100
        self.direction = RIGHT
        self.isAlive = True

    def draw(self, screen):
        if self.isAlive == True:
            pygame.draw.circle(screen, (255, 200, 255), (self.xpos, self.ypos), 20)
    def move(self, map, ticker,px,py):
        # randomly wander:
        if ticker % 40 == 0:
            num = random.randrange(0, 4)
            if num == 0:
                self.direction = RIGHT
            elif num == 1:
                self.direction = LEFT
        
        if map[int((self.ypos) / 50)][int((self.xpos - 10) / 50)] == 2 :
            self.xpos+=3

        #right collision
        if map[int((self.ypos) / 50)][int((self.xpos +30 + 5) / 50)] == 2 :
            self.xpos-=3

        #up colision
        if map[int((self.ypos-10) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos+=3

        #down collision
        if map[int((self.ypos+35) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos-=3

        # check for collision and change direction if you've bumped
        if self.direction == RIGHT and map[int((self.ypos) / 50)][int((self.xpos + 20) / 50)] == 2:
            self.direction = UP
            self.xpos -= 6
        if self.direction == LEFT and map[int((self.ypos) / 50)][int((self.xpos - 20) / 50)] == 2:
            self.direction = DOWN
            self.xpos += 6

        if self.direction == LEFT and map[int((self.ypos) / 50)][int((self.xpos + 20) / 50)] == 2:
            self.direction = DOWN
            self.xpos += 6
        if self.direction == RIGHT and map[int((self.ypos) / 50)][int((self.xpos - 20) / 50)] == 2:
            self.direction = UP
            self.xpos -= 6

        if self.direction == RIGHT:
            self.xpos += 3
        elif self.direction == LEFT:
            self.xpos -= 3
        if self.direction == UP:
            self.xpos += 3
        elif self.direction == DOWN:
            self.xpos -= 3

        #fireball############################

        import pygame


LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
SPACE = 4
W = 5

class player:
    def __init__(self):


        self.xpos = 450
        self.ypos = 415
        self.vx = 0
        self.vy = 0
        self.direction = RIGHT

    def draw(self,screen):
        pygame.draw.rect(screen, (255, 0, 255), (self.xpos, self.ypos, 30, 30))

    def move(self, keys, map):

        #left right movement
        if keys[LEFT] == True:
            self.vx = -3
            self.direction = LEFT

        elif keys[RIGHT] == True:
            self.vx = 3
            self.direction = RIGHT

        else:
            self.vx = 0

        #up down movement
        if keys[UP] == True:
            self.vy = -3
            self.direction = UP

        elif keys[DOWN] == True:
            self.vy = 3
            self.direction = DOWN
        else:
            self.vy = 0

        print("player direction is ", self.direction)
        #left collision
        if map[int((self.ypos) / 50)][int((self.xpos - 10) / 50)] == 2 :
            self.xpos+=3

        #right collision
        if map[int((self.ypos) / 50)][int((self.xpos +30 + 5) / 50)] == 2 :
            self.xpos-=3

        #up colision
        if map[int((self.ypos-10) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos+=3

        #down collision
        if map[int((self.ypos+35) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos-=3
        

        self.xpos+=self.vx  #updates x position with x velocity
        self.ypos+=self.vy




                    
