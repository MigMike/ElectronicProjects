---
title: Project 008.md

---

# Title: Building a Transistor-Based Combination Lock

## Introduction
Combination locks are foundational elements in electronic security systems, used in everything from door locks to safe boxes. While digital systems like microcontrollers and keypads dominate modern designs, building a transistor-based combination lock offers an excellent opportunity for electronics enthusiasts and students to understand the basics of logic circuits using discrete components.

This article walks you through the design and construction of a simple combination lock using NPN transistors, pushbuttons, resistors, and a few other passive components. With a focus on educational clarity and hands-on understanding, the guide below will help you build and test the lock on a breadboard using just four transistors and basic components.

## Learning Objectives
* By the end of this article, you will:
* Understand how to build a multi-stage logic system using NPN transistors.
* Learn how to use transistors as switches in a sequential unlocking mechanism.
* Grasp basic concepts of input debouncing, logic path isolation, and signal conditioning.
* Gain practical experience in circuit prototyping on a breadboard.

## Components Required

| Component                         | Quantity  | Notes                                      |
| --------------------------------- | --------- | ------------------------------------------ |
| NPN Transistor (e.g. S8050)       | 4         | Number of combination stages               |
| Resistors (10kΩ, 1kΩ)             | As needed | 10kΩ for pull-downs, 1kΩ for base limiting  |
| Pushbutton Switches               | 4+        | 4 correct buttons, optional decoy ones     |
| LEDs                              | 1         | Indicates successful combination           |
| 1N4148 Diodes                     | Optional  | For logic isolation (if needed)            |
| Breadboard + Wires                | 1         | For circuit assembly                       |
| 9V Battery / DC Power Supply      | 1         | System power source                        |

## Circuit Concept Overview
This lock works on the principle of transistor-based sequential logic. Each transistor represents one stage in the combination. Only when the correct button is pressed in the correct order, the corresponding transistor conducts, passing voltage to the base of the next transistor in the chain. The final transistor activates an LED, indicating that the correct combination has been entered.

### Circuit Block Diagram

Pushbutton1 → Transistor1 → Pushbutton2 → Transistor2 → Pushbutton3 → Transistor3 → Pushbutton4 → Transistor4 → LED

Each stage acts as a switch that only passes the signal forward if:
a). The correct pushbutton is pressed.
b). The previous stage is correctly activated.

## Step-by-Step Circuit Construction
1. Prepare the Power Supply
 Connect the positive terminal of the 9V battery (or DC supply) to the Vcc rail of the breadboard.
 Connect the negative terminal to the GND rail.

2. Insert the NPN Transistors
Place four S8050 NPN transistors on the breadboard, spaced adequately.
Label them Q1 to Q4 for clarity.

3. Connect the First Pushbutton Stage
* Connect one terminal of the first pushbutton to Vcc.
* Connect the other terminal to a 1kΩ resistor, then to the base of Q1.
* Add a 10kΩ pull-down resistor from the transistor base to GND to prevent false triggering.
* Connect the emitter of Q1 to GND.
* Connect a collector resistor (1kΩ) from Vcc to Q1’s collector.

4. Stage Linking (Q1 to Q2, Q2 to Q3, etc.)
* From the collector of Q1, connect to one terminal of the second pushbutton.
* Connect the other terminal of this pushbutton to the base of Q2 via a 1kΩ resistor.
* Again, place a 10kΩ pull-down on Q2’s base to GND.

*Repeat the same for Q3 and Q4, linking the collector of each stage to the next pushbutton and then to the next transistor's base.*

5. Final Output Indicator (LED)
* Connect the collector of Q4 to the anode of an LED through a 330Ω resistor.
* Connect the cathode of the LED to GND.
* The emitter of Q4 goes to GND as well.

6. Optional: Add Decoy Buttons
* You can place additional pushbuttons (connected to nothing or to dummy resistors) to mislead users.

****These do not affect the logic unless modified deliberately.***

### Circuit Diagram

![Figure 1](<images/images S2/T Combination.png>)
## Working Principle
Initially, all transistor bases are at GND due to the pull-down resistors, so all transistors are off.
When the first correct button is pressed:
* Current flows into the base of Q1, turning it on.
-This allows current to flow from Vcc to the collector of Q1, enabling the second button to function.

**This process repeats through Q2 and Q3.*

When the fourth correct button is pressed and Q4 turns on, the LED lights up, indicating a successful combination entry.

**Note:** If any button is pressed out of sequence, the current path is broken and the LED will not light up.

## Educational Analysis
***Transistors as Logic Gates:*** Each transistor acts like an AND gate where one input is the previous stage and the other is the correct button press.

***Sequential Dependency:*** The design ensures the order of inputs matters—if you press the right buttons in the wrong order, the lock won't open.

***No Microcontroller Needed:*** This design achieves digital logic behavior with purely analog components.

### Tips for Prototyping
* Test each transistor stage independently before linking.
* Use color-coded wires to distinguish between input, output, and power lines.
* If you experience bouncing or false triggering, consider adding 100nF capacitors across pushbutton terminals for debouncing.

For a more robust version, consider implementing diode isolation using 1N4148 diodes between the collector outputs and transistor bases.

## Conclusion
This transistor-based combination lock demonstrates how fundamental logic circuits can be constructed from basic electronic components. It’s a powerful educational project for understanding:

* Transistor switching,
* Sequential logic,
* Input conditioning, and
* DIY prototyping techniques.

Though limited in security and complexity, it serves as a foundation for building more sophisticated systems using logic gates or microcontrollers.

## Additional Resources

### Books

- ["The Art of Electronics" by Paul Horowitz and Winfield Hill](https://www.artofelectronics.net/)
- ["Practical Electronics for Inventors" by Paul Scherz](https://www.amazon.com/Practical-Electronics-Inventors-Fourth-Scherz/dp/1259587541)

### Simulation Tools

- [NI Multisim](https://www.multisim.com/)
- [Falstad Circuit Simulator](https://falstad.com/circuit/)
- [LTspice (Analog Devices)](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)

### Video Tutorials

- [Afrotechmods – Transistors Explained](https://www.youtube.com/watch?v=7ukDKVHnac4)
- [All About Circuits – YouTube Channel](https://www.youtube.com/user/AllAboutCircuits)

### Communities & Forums

- [Electronics Stack Exchange](https://electronics.stackexchange.com/)
- [EEVblog Forum](https://www.eevblog.com/forum/)
- [Reddit – r/AskElectronics](https://www.reddit.com/r/AskElectronics/)

If you're interested in expanding this lock to support more digits, memory, or digital displays, consider integrating flip-flops or transitioning to a microcontroller-based system using the same logic principles you've now mastered.
 
 
 






