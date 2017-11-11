# step 3 - add a laser to the spacecraft

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
5. Create a new function called initailRockPositions, we are going to have a special function for the rock's initial position. Move most of this code from the initialPosition function.
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
7. Now we invoke the initialPositions function.
```
initialPositions()
```
8.  At the end of updateSpacecraft we want to fire the laser if spacecraft is pressed.
```
  if keyboard.space and laserCharged:
    laserCharged = False
    laserFiring = True
```