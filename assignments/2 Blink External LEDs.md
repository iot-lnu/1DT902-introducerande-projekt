# Blink External LED's

## Introduction
In this assignment we connect basic circuits with LED's on a breadbord and write python code that turns these on and off. 

 * Get LED-lights to blink.
 * Work with GPIO ports.
 * Python loops
 

## Rules

This task is going to be conducted in a group of two students. Both students must be active during all steps of the assignment.

During the assignment you may discuss the assignment with students outside the group. You may help other groups but you may NOT do all steps for them. Note that these rules change between assignments.

## Ingredients

### Hardware
 * Everything from task 1.
 * breadboard
 * 1 Red LED
 * 1 Yellow LED
 * 1 Green LED
 * 3 Resistors 560 Ohm (Green, Blue, Brown, Gold) or higher
 
### Software 
 * Everything from task 1.
 * Atom with pymakr plugin

### Knowledge components
 * Breadboards (kopplingsdäck) https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard/all
 * Basic LED circuit https://en.wikipedia.org/wiki/LED_circuit
  * Light Emitting Diode's (LED's) https://en.wikipedia.org/wiki/Light-emitting_diode
  * Resistors (motstånd) https://en.wikipedia.org/wiki/Resistor
 * Microcontroller GPIO https://en.wikipedia.org/wiki/General-purpose_input/output
  * LOPY4 Datasheet https://docs.pycom.io/gitbook/assets/specsheets/Pycom_002_Specsheets_LoPy4_v2.pdf 
  * Make a GPIO port an output https://docs.pycom.io/firmwareapi/pycom/machine/pin/
  * Turn GPIO output on and off. ```python pin.value([value]) ```
 * Make the thread sleep for a second  ```python  time.sleep(seconds) ```
 * Loops. ```python  while Condition: ``` and/or ```python  for element in array: ```

 
## Steps


### Step. Connect Three LED circuits
We are going to connect three LED circuits on the breadboard and power these from the GND(-) and 3V3(+) connections on the LoPy4 board. See breadboard tutorial if needed.
WARNING! When changing components on the breadboard, always have the USB disconnected!

 * Disconnect the USB cable. 
 * Connect the GND on LOPY4 to the black power rail(BPR) on the breadboard. Also connect 3V3 to the red power rail(RPR). 
 * Connect the three LED circuits as in this video https://www.youtube.com/watch?v=yQ2-yVXFMeE but use the power rails as + and - of the battery and use a 560 Ohm resistor. 
 * Make sure each LED lights up when you connect the USB-cable. 
 
#### Connections 
Summary of connections. "<-->" means a cable or connection
 * LOPY4 GND <--> Black Power Rail (BPR)
 * LOPY4 3V3 <--> Red Power Rail (RPR)
 * RPR(3V3) <--> [ Anode - LED - Cathode ] <--> [ 560 Ohm resistor ] <--> BPR(GND)
 
 ![LED Circuit, Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/LED_circuit.svg/1200px-LED_circuit.svg.png)


### Step. Driving LED with GPIO  
IMPORTANT: We are going to connect external LED's to the microcontroller. The LoPy4 microcontroller provides "General Purpose Input Output"-ports also called GPIO-ports that can be used to communicate with external components. The ports are a bit sensitive and should not be used to directly drive heavy loads (like a motor). The Datasheet for LOPY4 says "Absolute MAX per pin 12mA, recommended 6mA" which means we must reduce current by using resistors. If more current is needed, additional components (eg. transistors, or drivers) can be used. Thankfully this assignment does not require high current and we can reduce the current flow by having a 560 Ohm resistor in series with each LED we connect.

 * Disconnect the USB cable again
 * For each of the LED's, remove the wire going from the red power rail to the anode (but keep the GND cable and resistor).
 * Introduce new cables going from the P8-10 port on the LoPy4 to the LED anodes as in connections below.
 
 #### Connections 
 * LOPY4 GND <--> Black Power Rail (BPR)
 * LOPY4 P8 <--> [ Anode - Red LED - Cathode ] <--> [ 560 Ohm resistor ] <--> BPR(GND)
 * LOPY4 P9 <--> [ Anode - Yellow LED - Cathode ] <--> [ 560 Ohm resistor ] <--> BPR(GND)
 * LOPY4 P10 <--> [ Anode - Green LED - Cathode ] <--> [ 560 Ohm resistor ] <--> BPR(GND)
 
 When done, connect USB again and upload the following code in the main.py file.

```python
import time
from machine import Pin
redLED = Pin("P8", mode=Pin.OUT) #Make GPIO P8 an output
redLED.value(1) # Send a 1 to GPIO to turn the LED on
time.sleep(1) # Sleep for a second
redLED.value(0) # Send a 0 to the GPIO to turn the LED off
```

#### Expected output

The Red LED should light up after the LOPY4 has booted, should stay lit for one second, and turn off. The behaviour is repeated if the board is resetted by pressing the reset button on the LoPy4 board (next to the RGB-LED on the side of the microUSB.

### Driving multiple LED's with GPIO

Now adjust the code so that all three LED's blink like this:
 * RED lights up for 1 s. Other LEDs are unlit.
 * GREEN lights up for 1 s. Other LEDs are unlit.
 * YELLOW lights up for 1 s. Other LEDs are unlit.
 * Repeat forever with RED again

#### Expected output
[![](http://img.youtube.com/vi/Wtd8pp-DW3w/0.jpg)](http://www.youtube.com/watch?v=Wtd8pp-DW3w "")

## Examination
This task can be self-examined. When the LED's blink in the expected sequence you are done with the programming task.

Check yourself so that you know the answers to the following questions.
 * Which leg of the LED is longer, the cathode or the anode?
 * Why do we need a resistor?
 * How can we make the LED's blink faster?
 * Where can you find information about the different hardware limits in the LOPY4 board?
 * What are the components of a basic LED-circuit and how do we connect them in order for the LED to light up?


