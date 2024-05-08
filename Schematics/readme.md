# Notes
- In the **Key Encoder** schematic the second 4-OR gate is shown as a 5-OR gate (which in reality is a 4-OR gate combined with a 2-OR gate). "4-Scanner" is the scanner from Ben's Output module, "S1" is the Input Selector, and "TM2" stands for the Signal Router.
- The fourth NAND gate in the **Input Selector** could be used to replace Ben's Enter button (for RAM), but then you can not switch through the selector anymore without the risk of accidentially entering whatever value currently is in the buffers.
- The 74HC125 consists of four 3-state buffers (three of which are used), but in the **Signal Router** schematic I only placed a symbol next to the middle one. The upper two ICs are the 244s, and the lower three are the 175s.

