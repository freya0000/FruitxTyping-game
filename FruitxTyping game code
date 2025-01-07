import pyxel
import random

SCREEN_WIDTH = 200
SCREEN_HEIGHT = 210
FRUIT_WIDTH = 16
FRUIT_HEIGHT = 16

pyxel.init(SCREEN_WIDTH, SCREEN_HEIGHT)

class Fruit:
    speed = 0.5
    def __init__(self):
        self.x = random.randint(5, 200 - 16 -5)
        self.y = 0
        self.kind = pyxel.rndi(1,12)

    def update(self):
        self.y += self.speed

    def draw(self):
        pyxel.blt(self.x, self.y, 0, 0, 16*self.kind, FRUIT_WIDTH, FRUIT_HEIGHT,6)

class Star :
    speed = 0.5
    def __init__ (self,x,y) :
        self.x = x
        self.y = y
    def update(self):
        self.y += self.speed

    def draw(self) :
        pyxel.blt(self.x, self.y, 0, 0, 0, 16, 16,6)

class Catcher:
    speed = 3
    def __init__(self):
        self.x = 100
        self.y = 210-32
    def move(self):
        if pyxel.btn(pyxel.KEY_RIGHT):
            self.x += self.speed
        if pyxel.btn(pyxel.KEY_LEFT):
            self.x -= self.speed
    def catch(self,item):
         #If hit!
        if (item.y >= 210-45 and self.x-20<=item.x<=self.x+24) :
            print("hit")
            return True
    def draw(self) :
        pyxel.blt(self.x,self.y,1,0,0,25,32,6)
        

class Game:
    def __init__(self):
        pyxel.load("Pictures_final.pyxres")
        pyxel.playm(0,loop=True)
        pyxel.mouse(True)
        
        #pyxel.load("assets.pyxres")

        self.fruits = [Fruit()]
        self.fruits_list_index = 0
        self.stars = []
        self.glow_x =  -20
        self.glow_y =  -20
        self.move_glow = False
        self.fruit_index = 1
        self.input_string = ""
        self.catcher = Catcher()
        self.point = 0
        self.counter_speed = 0
        self.lives = 5
        self.counter_heart = 0
        self.heart = False
        self.heart_y = 0
        self.heart_x = random.randint(0,190)

        self.time_interval = 75/Fruit.speed
        self.lastspawn_time = pyxel.frame_count
        self.game_mode = 0
        pyxel.run(self.update, self.draw)

    def update(self):
        #Can move catcher before game starts
        self.catcher.move()

        #Input to start game (Move from Start screen to Game screen)
        if pyxel.btn(pyxel.KEY_SPACE):
            self.game_mode = 1 
            self.lastspawn_time = pyxel.frame_count

        elif self.game_mode == 1 : #Game screen
            'Fruit spawn mechanic'
            #Every ... second, a new fruit spawns with random x coordinate
            #self.lastspawn_time = pyxel.frame_count
            if pyxel.frame_count - self.lastspawn_time >= self.time_interval :
                self.fruits.append(Fruit())
                self.lastspawn_time = pyxel.frame_count

            'Glow location'
            'if distance between mouse and fruit = 0,/ mouse in fruit vicinity,, self.glow_x and y move to that'
            if self.fruits == [] or self.fruits_list_index >= len(self.fruits): #make sure not out of range
                self.glow_x =  -20
                self.glow_y =  -20
            else :               
                self.glow_x =  self.fruits[self.fruits_list_index].x + 7
                self.glow_y =  self.fruits[self.fruits_list_index].y + 7

                if self.fruits[self.fruits_list_index].kind == 1:
                    for key in "abcdefghijklmnopqrstuvwxyz":
                        if pyxel.btnp(ord(key)):
                            self.lives -= 1
                            pyxel.playm(2)
                            # lose life if start typing on bomb
                            
            #know the position of the fruit in the fruit list
            for fruit in self.fruits :
                if  pyxel.btnp(pyxel.MOUSE_BUTTON_LEFT) and (fruit.x<=pyxel.mouse_x<=fruit.x+16) and (fruit.y<=pyxel.mouse_y<=fruit.y+16) :
                    self.fruits_list_index = self.fruits.index(fruit)


            'What happen to the fruits after it spawns'
            for fruit in self.fruits:
                fruit.update() #Fruits move downward
    
                # Remove fruit if it goes off-screen and minus 1 life (counted as miss)
                if fruit.y > SCREEN_HEIGHT:
                    if fruit.kind == 1 : #if it's bomb
                        pass
                    else:
                        print("miss")
                        self.lives -= 1
                        pyxel.playm(2)
                        print("lives = ", str(self.lives))
                    self.fruits.remove(fruit)
                    self.fruits_list_index -= 1
                
                if fruit.kind == 1 :
                    if self.glow_x == fruit.x + 7 and self.glow_y == fruit.y+7 :
                        print('bomb glows')
                        for key in "abcdefghijklmnopqrstuvwxyz":
                             if pyxel.btnp(ord(key)):
                                 self.lives -= 1
                                 self.fruits.remove(fruit)

                    if self.catcher.catch(fruit) == True :
                        self.lives -= 1
                        self.fruits.remove(fruit)

            if self.glow_y >= SCREEN_HEIGHT :
                self.fruits_list_index = 0

            'What happen to stars after it spawns (Fruit turn into star)'
            for s in self.stars :
                s.update() #Stars move downward just like fruits
                if self.catcher.catch(s) == True :
                    self.point += 1
                    pyxel.playm(1)
                    self.stars.remove(s)
                    self.counter_speed += 1
                    self.counter_heart += 1
                    print("counter :", self.counter_speed)
                if s.y > SCREEN_HEIGHT:
                    print("miss")
                    self.stars.remove(s)
                    pyxel.playm(2)
                    self.lives -= 1
                    print("lives = ", str(self.lives))

            'Special Milestone'
            #Every 5 catches, Speed will increase (velocity of the fruits), and the time gap for a new fruit to spawn also decrease
            if self.counter_speed == 5 :
                Fruit.speed += 0.1
                Catcher.speed += 0.3
                print('catcher speed',Catcher.speed)
                Star.speed += 0.1
                self.counter_speed = 0
                self.time_interval = 75/Fruit.speed
                print("speed"+str(Fruit.speed)+" time"+str(self.time_interval) )
            #Every 10 catches, a heart will fall from the sky, which when caught will give extra life
            if self.counter_heart == 10 :
                self.heart = True
                self.counter_heart = 0
                
            if self.heart == True :
                #print("heart")
                self.heart_y += 1
                if self.heart_y >= 210-35 and self.catcher.x<=self.heart_x<=self.catcher.x+24:
                    self.lives += 1
                    pyxel.playm(1)
                    #error : still count as catch even after the heart is out of screen (it is still going)
                    print("heart +1")
                    self.heart_x = random.randint(0,190)
                    self.heart_y = -10
                    self.heart = False
                elif self.heart_y >= 210 :
                    self.heart_x = random.randint(0,190)
                    self.heart_y = -10
                    self.heart = False


            'Typing Mechanic'
            #Handling letter input and backspace
            for key in "abcdefghijklmnopqrstuvwxyz":
                if pyxel.btnp(ord(key)):
                    self.input_string += key
            if pyxel.btnp(pyxel.KEY_BACKSPACE):
                    self.input_string = self.input_string[:-1]
            #Call the check method when pressing enter
            if pyxel.btn(pyxel.KEY_RETURN) :
                self.check()

            'Game over Mechanic'
            #Game is over when player run out of lives, move to Game over mode
            if self.lives == 0 :
                self.game_mode =2

        elif self.game_mode == 2 :
            #if  pyxel.btnp(pyxel.MOUSE_BUTTON_LEFT) and (62<=pyxel.mouse_x<=62+77) and (90<=pyxel.mouse_y<=90+24) :
                #self.game_mode = 0
            pyxel.mouse(False)
            if pyxel.btn(pyxel.KEY_R) :
                self.game_mode = 0
                self.__init__()
            

    ###################################
    # METHOD TO CHECK THE TYPED INPUT #
    ###################################

    def check(self) :
        #If the input correspond to the type or fruit,...  
        self.fruit_namelist = ["njasdjdjkjk(dont type)", "orange", "watermelon", "strawberry", "cherry", "grape", "avocado", "apple", "blueberry", "lemon", "kiwi", "banana"]  
        for fruit in self.fruits:
            if self.glow_x != -20 : #if glow is in frame
                fruit = self.fruits[self.fruits_list_index]
                self.fruit_index = fruit.kind - 1
                
                if self.fruit_namelist[self.fruit_index] == self.input_string:
                    self.stars.append(Star(fruit.x, fruit.y))
                    self.fruits.remove(fruit)
                    print('index', self.fruits_list_index)
                    print('len', len(self.fruits))
                self.input_string = ""
        

    def draw(self):
        if self.game_mode == 0 :
            pyxel.cls(6)
            pyxel.blt(100-89, 50, 2, 8, 115, 180, 27)
            pyxel.text(15, 90, "Type the name of the glowing fruit", 0)
            pyxel.text(15, 100, "Avoid bomb,", 0)
            pyxel.text(15, 110, "don't type anything when there is bomb", 0)
            pyxel.text(15, 120, "Click the next fruit to move the glow", 0)
            pyxel.text(60, 150, "Press SPACE to start", 0)
            self.catcher.draw()

        if self.game_mode == 1 :
            pyxel.cls(6)
            #heart, Corresponds to how much lives
            for i in range(self.lives) :
                pyxel.blt(187-12*i,3,1,0,32,10,16,6)
            # pyxel.blt(200-26,3,1,0,32,10,16,6)
            # pyxel.blt(200-38,3,1,0,32,10,16,6)


            #Draw the glow
            pyxel.circ(self.glow_x,self.glow_y,10,7)
            pyxel.circ(self.glow_x,self.glow_y,9,10)
            
            #Draw the falling fruits, stars, and hearts
            for fruit in self.fruits:
                fruit.draw()
            for star in self.stars :
                star.draw()
            if self.heart == True :
                pyxel.blt(self.heart_x,self.heart_y,1,0,32,10,16,6)
            
            #Texts - Answer input display and Points
            pyxel.text(5,5,self.input_string,0)   
            pyxel.text(5,15,"Point : "+ str(self.point),0)

            #Draw the Catcher
            self.catcher.draw()

        if self.game_mode == 2 :
            pyxel.text(82, 80, "GAME OVER", 0)
            pyxel.text(60, 90, "Press 'R' ro RESTART", 0)
            pyxel.rect(200-16,0,16,16,6)

            #pyxel.blt(62,90,1,0,96,77,24,6)      

Game()
