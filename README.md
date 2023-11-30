# Pinball Machine

## Table Of Contents
* [Planning](#Planning)
* [Rollover Buttons](#Rollover Buttons)



## Planning

Gaby and I first came up with the idea to make a Pinball Machine last year at the end of Engineering 4 when we had completed our rocket and were looking for an exciting Capstone project. To begin planning, we made a slideshow with all our essential and nonessential requirements for our project and laid out our plans for how the machine should work and all the necessary steps beforehand. [Here's a link to the Pinball Slideshow](https://docs.google.com/presentation/d/1-0p-8omO62feyVH7SRMGAjvP5zyLEiNpoB7CkiigmQg/edit?usp=sharing). 

## Rollover Buttons

### Code

``` python
import time #imports
import board
import digitalio

led1 = digitalio.DigitalInOut(board.GP15) #pins 
led1.direction = digitalio.Direction.OUTPUT
led2 = digitalio.DigitalInOut(board.GP17)
led2.direction = digitalio.Direction.OUTPUT
button = digitalio.DigitalInOut(board.GP16) #adds in the button
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.UP #incorperates the button into the circuit

score = 0   #base value starts score at 0
oldbutton_state = 0


while True: #if the button is pressed this will happen
     if button.value == False: #if pressed
          if oldbutton_state == 0:
               score = score + 350 #each time the button is pushed the score increases by 350
               print(score)
               oldbutton_state = 1 #button was pressed
     else:
          oldbutton_state = 0   #only changes when the button is pressed
```

Every time the pinball rolls over the button, the score will increase by 350 points. I'm working on coding an LCD so that this score will be visible and updated on an LCD screen so people can see their points increase while playing. That's going to be kind of complicated because there are going to be several mechanisms that will need to add to the score as well. 

 


