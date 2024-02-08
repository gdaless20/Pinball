# Pinball Machine

## Table Of Contents
* [Planning](#Planning)
* [Rollover Buttons](#Rollover_Buttons)
* [LCD](#LCD)



## Planning

Gaby and I first came up with the idea to make a Pinball Machine last year at the end of Engineering 4 when we had completed our rocket and were looking for an exciting Capstone project. To begin planning, we made a slideshow with all our essential and nonessential requirements for our project and laid out our plans for how the machine should work and all the necessary steps beforehand. [Here's a link to the Pinball Slideshow](https://docs.google.com/presentation/d/1-0p-8omO62feyVH7SRMGAjvP5zyLEiNpoB7CkiigmQg/edit?usp=sharing). 

## Rollover_Buttons

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

Every time the pinball rolls over the button, the score will increase by 350 points. I'm working on coding an LCD so that this score will be visible and updated on an LCD screen so people can see their points increase while playing. Buttons in general are pretty simple for code, this button is specifically functioning as the point route notches. Each time the pinball runs over them, pressing them down, the lcd screen will update your score by adding 350 points. 

## LCD
 
``` python
import time  
import board 
import busio  
import digitalio
import displayio
 
from lcd.lcd import LCD, CursorMode
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface

button = digitalio.DigitalInOut(board.GP16) #adds in the button
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.UP #incorperates the button into the circuit


# Pin definitions

# I2C used for LCD Display
i2c_scl = board.GP11
i2c_sda = board.GP10
i2c_address = 0x27 # 39 decimal

# LCD display info
cols = 16
rows = 2

score = 0   #base value starts score at 0
oldbutton_state = 0

# Setup LCD display

i2c = busio.I2C(scl=i2c_scl, sda=i2c_sda)
interface = I2CPCF8574Interface(i2c, i2c_address)  #sets up lcd screen
lcd = LCD(interface, num_rows=rows, num_cols=cols)
lcd.set_cursor_mode(CursorMode.HIDE)

while True: #if the button is pressed this will happen
     if button.value == False: #if pressed
          if oldbutton_state == 0:
               score = score + 350 #each time the button is pushed the score increases by 350
               lcd.set_cursor_pos(0, 0)
               lcd.print(str(score)) #lcd shows new score
               oldbutton_state = 1 #button was pressed
     else:
          oldbutton_state = 0   #only changes when the button is pressedlcd.print ("word")

#sources
##https://www.penguintutor.com/electronics/pico-lcd
##https://learn.adafruit.com/character-lcds/python-circuitpython 
##https://learn.adafruit.com/i2c-spi-lcd-backpack/python-circuitpython 
##https://github.com/T-622/RPI-PICO-I2C-LCD 
```

LCD code was not the highlight of this project for me. This felt really complicated but to be honest starting out what took me the most time to get the LCD code going was simply finding the right libraries to download. I had never used an LCD code before and had no idea where to start out but I used several different websites online (linked in code) to get a feel for how the code needed to be organized and what each aspect did. I used an LCD backpack so the wiring was almost non-existent which was really nice for time, energy, and organization. Using the links I setup the libraries to the LCD and addressed everything so each part would be recognized and run smoothly between the code and LCD itself. Then I added in my code from the button because I need the points scored to show up on the display. To incorporate the points being added to the score on display, I made score a variable and set it to 0 when you start, I was able to then use an equation to make it so that each time the button was pressed, 350 points would be added to the score and stay there until added to again. 












