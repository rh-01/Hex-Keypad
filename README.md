+++ work in progress +++

# Hex-Keypad

This is a side project for Ben Eater's 8 bit computer. It adds an input module that enables using a simple hex keyboard for code input. It consists of three sub-modules:

## Input selector 
Selects the input type (address / msb / lsb) and consists of the following components:
- pushbutton
- double D flip flop [74HC74]
- quad NAND (74HC00) 
- 3 inverters (can be used from clock module above)
- 3 LEDs to indicate input mode (yellow for MAR and 2xred for RAM)

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
I used HC series chips for the whole project.

There might be a more elegant way to implement this. For example, I wanted to directly connect the input select with the 4-Or gate that registers key presses so that I don't have to manually switch between the three target registers. However, there was a problem in the signal quality so that the switch would not happen reliably. When I have a bit more time I might try to fix this.

The first module can be placed directly next to the MAR module, and if you keep the lowest two breadboards (right and left side) empty for Ben Eater's original design, you can fit the last two modules there (see image, I removed the Keypad to show the full board).

![alt text](IMG_3048.jpg)


The project can easily be extended to 8 bit addresses: simply add another 175 and one more indicator LED for the 8 bit address (one of the 244 routers still has an empty slot). 
