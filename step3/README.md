# Step 3: add a laser to the spacecraft

1. Let's create a laser rectangle, positioned off the screen initially. Add this to below our declaration of the spacecraft and rock objects.
```
laser = Rect((0,-HEIGHT*4), (2, 1000))  
```
2. Declare two new variables to detect the status of the laser. Put the code near the initial gameOver declaration.
```
laserCharged = True
laserFiring = False
```
3. We are also going to keep a track of the score, so put the variables underneath the above.
```
score = 0
topScore = 0
```
4. When hit, the rock is going to disappear, so we need a variable to control this, add the following  
```
rmRock = False
```
5. Create a new function called initailRockPositions, we are going to have a special function for the rock's initial position. Move most of this code is from from the initialPosition function from step 2.
```
def initialRockPosition():
  global rock
  global rock_vx
  global rock_vy
  global rmRock
  rock.image = 'rock' # In case it has been destroyed
  rock.pos = 0, HEIGHT*2 # Off the screen
  rock_vx = 0 # Set the x component of the rock velocity to be zero
  rock_vy = 0 # Set the y component of the rock velocity to be zero
  (rock.x, rock.y) = startingPosition() 
  (rock_vx, rock_vy) = startingVelocity() 
  rock.image = 'rock'
  rmRock = False
```
6. The initialPosition function is now just for the Spacecraft. It should now look like this:  
```
def initialPositions():
  global spacecraft
  global score
  spacecraft.image = 'spacecraft' 
  spacecraft.pos = centre_x, centre_y 
  initialRockPosition()
  score = 0 
```
7. Now we invoke the initialPositions function. This isn't part of a function, so should not be indented.
```
initialPositions()
```
8.  At the end of updateSpacecraft we want to fire the laser if spacecraft is pressed.
The laser will fire for 3/10 of a second, so we want to user a time event to control this. This will call a function after 0.3 seconds.
```
if keyboard.space and laserCharged:
    laserCharged = False
    laserFiring = True
    clock.schedule(laserFiringComplete, 0.3)
```
10. Let's create a new function laserFiringComplete. This will change a flag so we know the firing is complete. We will also prevent the player firing the laser straight away - so we will 'charge' the laser for 1 second. After 1 second we will call another function.
```
def laserFiringComplete():
  global laserFiring
  laserFiring = False 
  clock.schedule(laserChargingComplete, 1.0)
```
11. Let's create the function for when charging is complete.
```
def laserChargingComplete():
  global laserCharged
  laserCharged = True
```
12. Back in updateSpacecraft; If the laser is firing, we want to move the rectangle (representing the laser) to where the spacecraft is. It will requires two sets of co-ordinates to draw the rectangle; x and width, y and heigth. At the end of the function, place this code:
```
if laserFiring:
    laser = Rect((spacecraft.x-2,0),(4,spacecraft.top))
```
13. Now we need to modify the update function. Let's add global score variables at the top.
```
  global score
  global topScore
```
14. We need to check if the laser has hit the rock, if it has and has not already been hit, then increase the score - keeping a track of the top score. The rock will be removed after 0.2 seconds.
```
rockLaser = rock.colliderect(laser)

if rockLaser and laserFiring and rock.image != 'rock_destroyed':
    rock.image = 'rock_destroyed'
    score = score + 1
    
    if score > topScore:
      topScore = score

    clock.schedule(removeRock, 0.2)
```
15. Now create a function that will remove the rock.
```
def removeRock():
  global rmRock
  rmRock = True
```
16. Modify the draw function to show the score information at the bottom of the screen. This should be place at the top of draw, just below the rock.draw call.
```
  screen.draw.text("Score : "+str(score), center=(centre_x-100, HEIGHT-10.))
  screen.draw.text("Top Score : "+str(topScore), center=(centre_x+100, HEIGHT-10.))
```
17. Modify the draw function to actually display the laser rectangle. Place just after the above code.
```
if laserFiring:
    screen.draw.filled_rect(laser,(0,255,0))
```
 
  [Go back to step 2](../step2)

  [Go back to step 1](../step1)
