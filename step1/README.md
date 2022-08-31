# Create a rocket, can move in 4 directions from keyboard

1. Let's create the size of the screen
```
WIDTH = 600
HEIGHT = 500
```
2. Now create the Actor - which is the spacecraft. Set its position to be in the centre of the screen.
```
spacecraft = Actor('spacecraft')   
spacecraft.pos = WIDTH/2, HEIGHT/2  
```
3. Create a new function, draw. Pygame Zero will invoke this function when the game is started. In this we clear the screen and draw the spacecraft.
```
def draw():
  screen.clear()
  spacecraft.draw()

```
4. Now we want to move the spacecraft with the keyboard. Create a new function call update, this will be regularily invoked by Pygame Zero.   
If the left button is pressed and we're not at the edge of the screen, then modify the x position of the spacecraft. Likewise for the right button.   
If up or down is pressed, modify the y postion of the spacecraft.  
```
def update():
  if keyboard.left and spacecraft.left > 2:
    spacecraft.x -= 2
  if keyboard.right and spacecraft.right < WIDTH+2:
    spacecraft.x += 2
  if keyboard.down and spacecraft.bottom < HEIGHT+2:
    spacecraft.y += 2
  if keyboard.up and spacecraft.top > 2:
    spacecraft.y -= 2
```
5. Now test your code. 

[Go to step 2](../Step2)
