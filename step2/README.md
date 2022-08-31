# Step 2: add a rock

1. The rock will be moving randomly across the screen, so we need to include the Random library to provide this functionality. Add the top of your code, add the following, as the first line:
```
import random
```
2. We now need to create the rock object as an Actor, it will use an image of the same name. Underneath the spacecraft declaration add :  
```
rock = Actor('rock') 
```
3. Some improvements are needed to our step 1 code, let's store the co-ordinates of the centre of the screen, so we don't have to repeat calculating it. Add this underneath the rock declarations :  
```
centre_x = WIDTH/2
centre_y = HEIGHT/2
```
4. Let's create a function that declares the initial setting of both the spacecraft and the rock. We are going to declare several global variables, remember if a variable is global it can be used throughtout the program not just in a single function.
```
def initialPositions():
  global spacecraft
  global rock
  global rock_vx
  global rock_vy
```
We need to set the  spacecraft image, as it could have changed (it may have been hit!).
Add this to the initialPositions function: 
```
  spacecraft.image = 'spacecraft' 
```
Let's set the spaceship to be in the centre of the screen (in the same initialPositions function)
```
  spacecraft.pos = centre_x, centre_y 
```
Set the rock's initial position to be off the screen
```
  rock.pos = 0, HEIGHT*2 
```
Set the x and y velocity of the rock to zero (how it's moving)
```
  rock_vx = 0 
  rock_vy = 0 
```
5. Now create a new function to set the starting postion of the rock. This uses a return statement. So when the function is called, the returned data is available to use. In this case we return a Tuple, which is a pair of numbers, the first being a randon integer between 0 and the width of the screen and the second number is 0. This will be co-ordinates for a random location at the top of the screen.
```
def startingPosition():
  return (random.randint(0, WIDTH), 0)

```
6. Now we need to do something similar for the starting velocity. What directon should the rock start going? A random velocity, going downwards away from the top of the screen.
```
def startingVelocity():
  return (random.randint(-5, 5), random.randint(1, 5))
```
7. Let's modify our draw function and draw the rock. After spacecraft.draw() add :
```
rock.draw()
```
8. We now need some functionality to update the rock position. Let's create a new function call updateRock. If the rock has gone off the screen, i.e left, right or top - we need to reset the position and velocity. Aslo reset the image, just in case it was destroyed.  
Change the X and Y co-ordinates of the rock by the velocity amount.
```
def updateRock():
  global rock
  global rock_vx
  global rock_vy
 
  if rock.right < 0 or rock.left > WIDTH or rock.top > HEIGHT:
    (rock.x, rock.y) = startingPosition()
    (rock_vx, rock_vy) = startingVelocity()
    rock.image = 'rock'  

  rock.x += rock_vx

  rock.y += rock_vy 
```
9. Create a new function call UpdateSpacecraft, this is where the code for moving the spacecraft that we previosuly wrote in the update function is to be placed. So move all of the existing keyboard detection code into a new function, as below:
```
def updateSpacecraft():
  if keyboard.left and spacecraft.left > 2:
    spacecraft.x -= 2
  if keyboard.right and spacecraft.right < WIDTH+2:
    spacecraft.x += 2
  if keyboard.down and spacecraft.bottom < HEIGHT+2:
    spacecraft.y += 2
  if keyboard.up and spacecraft.top > 2:
    spacecraft.y -= 2
```
10. The update function will now be empty, this is where we now want to put code that invokes the updateRock and updateSpacecraft functions. Remember the update function is called by PyGame framework multiple times a second. Your update function should now look like this :
```
def update(): 
    updateSpacecraft()
    updateRock()
```
11. As the very last code in your program, call the function that sets the initial positions of the rock and spacecraft. This is not part of any function so make sure it is not indented.
```
initialPositions() 
```
12. Now save and test your code - if everything works ok then proceed to the next step.
13. At the moment if the rock hits the spacecraft nothing happens, let's change that. We will use the the colliderect function available on the Actor objects, this function will return true if the specific object is colliding with another Actor object that we pass as a parameter. So add this line of code into the update function: 
```
collision = spacecraft.colliderect(rock)
```
The collision variable will be set to true if the spacecraft has hit the rock.   
If it is true, we want to change the images of both the rock and the space craft. Place this code immediately after the collision check.
```
if collision:
    rock.image = 'rock_destroyed'
    spacecraft.image = 'spacecraft_destroyed'
```
14. Now save and test your code - if everything works ok then proceed to the next step. 
15. If the rock and spacecraft do actually collide we need to display a message and end the game. At the start of the update function, add a new global variable called gameOver.
```
 global gameOver
 ```
 In the section of code where we haev detected that there has been a collision, set the gameOver variable to True.
 ```
 gameOver = True
 ```
 16. At the end of your code, just before calling initailPositions, set the gameOver to False. This is the first code executed when the program starts.
 ```
 gameOver = False
 ```
 17. Now let's display the message. At then end of the draw function, if we find that gameOver is set to True then draw a series of coloured rectangles of slighly different red to , followed by two lines of text.
 ```
  if gameOver:
    for i in range(20,-5,-5):
      screen.draw.filled_rect(Rect((centre_x-(100+i), centre_y-(30+i)), (200+(i*2), 80+(i*2))), (200-(i*8), 0, 0))
    screen.draw.text("GAME OVER!", center=(centre_x, centre_y))
    screen.draw.text("(spacebar to restart)", center=(centre_x, centre_y+20))
 ```
 18. Now we need to detected if the spacebar was pressed in response to this message. In the update function, just after our declaration of the gameOver variable, we need to check whether it's set to True. If it is not then we move our existing code to  updateSpacecraft and updateRock (we only want to move these if the game is still running), if the game is over  we need to then check if the spacebar was pressed (the user want's to continue) - if so, set the rock and spacecraft back to the initial postions and reset gameOver.
 ```
  if not gameOver:
    updateSpacecraft()
    updateRock()
  else:
    if keyboard.space:
      initialPositions()
      gameOver = False
 ```
 19. Now save and test your code - if everything works ok then proceed to the step 3. 
 
 [Go to step 3](../step3)
 
 [Go back to step 1](../step1)
