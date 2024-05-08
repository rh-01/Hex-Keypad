# Hex Keypad Input Module

This is a side project for Ben Eater's 8 bit computer. It adds an input module that give you the option to use a simple hex keypad for code input, and consists of three sub-modules. I added some basic schematics for them, but this whole description still needs to be cleaned up a bit when I have more time...

Operation is straightforward: select destination, enter hex code, finally (after all three hex codes have been entered) confirm input with Ben's original Enter button.

Note: I used HC series ICs for the whole project, and I also needed a few 4.7k push-down resistors and 100nF decoupling capacitors.

## 1 - Input selector 
Selects the input destination (address / msb / lsb) and consists of the following components:
- push button to select the input destination 
- double D flip flop [74HC74]
- quad NAND (74HC00) 
- 3 inverters (can be used from clock module above) for indicator LEDs
- 3 LEDs to indicate input mode (yellow for MAR and 2 x red for RAM)

## 2 - Key encoder
Converts the button presses of the hex keypad (which is simply 16 buttons connected with 4 wires each for rows and columns) into a 4 bit code. It consists of the following components:
- hex keypad (or simply 16 push buttons)
- existing counter from output module (needs to be inverted with an additional 74HC04) to scan columns
- quad OR (74HC32) for encoding rows and columns
- 2x 4-OR gates (4072 + additional 74HC32 OR gate for '0' button which otherwise is not captured) for two triggers: one for the 3- state buffer of the key encoder, one for the signal switch  
- 4-bit 3-state buffer (with Schmitt trigger) [74HC126]

## 3 - Signal router
Routes the input signal to MAR or RAM according to the input selected (MAR, RAM msb/lsb), and consists of the following components: 
- 2x double 4-bit buffers (74HC244) for routing
- 3x quad buffers (74HC175) as input buffers
- 3-state buffer (74HC125) as read enable switch (triggered by input selector)


## Notes

The first module can be placed in the empty space of the MAR module (the LEDs are placed on the clock module above), and if you keep the lowest two breadboards (right and left side) empty for Ben Eater's original design, you can fit the last two modules there (see image, I removed the keypad to show the full board).

Hex keypads are really cheap, but they typically have key layouts like on a phone or pocket calculator. I simply fixed a piece of (handwritten) paper on top of it with a layout that is more convenient for the given purpose. I added some long pins to the connector (mine had female connectors) so that I can easily stick it into to breadboard.  

![alt text](IMG_3048.jpg)


There might be a more elegant way to implement all this. For example, I wanted to directly connect the input select with the 4-OR gate that registers key presses so that I don't have to manually switch between the three target registers. However, there was a problem in the signal quality from the 4-OR (the switch would not happen reliably). When I have a bit more time I might try to fix this.

If you have implemented a 8-bit address version of Ben Eater's computer, the project can easily be extended to 8-bit addresses: simply add another 175 buffer and one more indicator LED for the 8 bit address (one of the 244 routers still has an empty slot). In my setup, I was unfortunately running out of physical space. 
