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
3. We are also going to keep a track of the score, so put the variables underneathe the above.
```
score = 0
topScore = 0
```
4. When hit, the rock is going to disappear, so we need a variable to control this, add the following below 
```
rmRock = False
```
5.