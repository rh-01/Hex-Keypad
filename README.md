+++ work in progress +++

# Hex-Keypad

This is a side project for Ben Eater's 8 bit computer. It adds an input module that enables using a simple hex keyboard for code input. It consists of three sub-modules (I used HC series ICs for the whole project):

## Input selector 
Selects the input type (address / msb / lsb) and consists of the following components:
- pushbutton
- double D flip flop [74HC74]
- quad NAND (74HC00) 
- 3 inverters (can be used from clock module above) for indicator LEDs
- 3 LEDs to indicate input mode (yellow for MAR and 2 x red for RAM)

## Key encoder
Converts the button presses of the hex keyboard into a 4 bit code and consists of the following components:
- hex keypad (or simply 16 push buttons)
- existing counter from output module (needs to be inverted with an additional 74HC04) to scan columns
- quad OR (74HC32) for encoding rows and columns
- 2 triggers - one for key encoder (4-OR gate, 4072), one for signal switch (4-OR gate + additional OR for 0) 
- 4-bit 3-state Buffer (with Schmitt trigger) [74HC126]

## Signal router
Routes the input signal to MAR or RAM according to the input selected (MAR, RAM msb/lsb). It and consists of the following components: 
- 2x double 4 bit buffer (74HC244) for routing
- 3x quad buffers (74HC175) as input buffers
- 3-state Buffer (74HC125) as trigger (from input selector)


## Notes

There might be a more elegant way to implement this. For example, I wanted to directly connect the input select with the 4-OR gate that registers key presses so that I don't have to manually switch between the three target registers. However, there was a problem in the signal quality from the 4-OR (the switch would not happen reliably). When I have a bit more time I might try to fix this.

The first module can be placed in the empty space of the MAR module (the LEDs are placed on the clock module above), and if you keep the lowest two breadboards (right and left side) empty for Ben Eater's original design, you can fit the last two modules there (see image, I removed the keypad to show the full board).

![alt text](IMG_3048.jpg)


PS: The project can easily be extended to 8 bit addresses, if you have implemented a 8-bit address version of the computer: simply add another 175 and one more indicator LED for the 8 bit address (one of the 244 routers still has an empty slot). In my setup, I was unfortunately running out of space. 
