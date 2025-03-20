# Proteus Simulation: Arduino Stepper Control

## Why Proteus
- An easy to use interface with real-time microcontroller simulation.
- Supports  both analog and dialog components as it enable firmware testing on microcontrollers (Arduino or PIC)

## Installation of proteus
Step 1: Download Proteus zip. file
- Visit the official website (Labcenter Electronics)
- Click on Download.
- Choose the free proteus Demonstration Version or the Paid version if have License.

Step 2: Installing 
- Open the downloaded setup file (.exe).
- Follow the installation wizard:
    - Click Next.
    - Accept the license agreement.
    - Choose the installation directory.
    - Select components to install (Proteus, libraries, etc.).
    - Click Install.

Step 3:  Activate Proteus 
- Licensed version, enter your activation key during installation.
- Trial/demo, you can skip this step.
- 
Step 4: Run Proteus
- Once installed, launch Proteus version that you have from the Start Menu.
- 
Step 5: Install Additional Libraries (Optional)
- To use extra microcontrollers (e.g., Arduino) download the  additional library (Arduino library) and copy it into proteus folder location:
  **Example**
 ## Friendly Guide on How to Add Arduino Library to Proteus:
Step 1: Download the Arduino Library for Proteus

- Download the Arduino Proteus Library from a trusted source. You can search for "Arduino Proteus Library zip" online.
- The file will usually be in a .zip format. Extract it to get the .IDX, .LIB, and .HEX files.
 
Step 2: Copy Library Files to Proteus
- Navigate to your Proteus installation folder .
- Copy the .LIB and .IDX files into the LIBRARY folder.
 
Step 3: Load the Arduino HEX File (For Simulation)
- Open your proteus software and create a new project.
- Click on the "P" (Pick Devices) button.
- Search for "Arduino" in the search bar.
- Select the desired Arduino board (e.g., Arduino Uno, Mega, Nano) and place it on the schematic.
- Double-click the Arduino component and locate the "Program File" section.
- Click on the folder icon and browse to your Arduino HEX file.
- The HEX file is generated from the Arduino IDE after compiling a sketch.
- You can find it in the Arduino build directory.
- 
Step 4: Test the Library
- Connect components (LEDs, sensors, etc.).Click and hold as you drag your cursor to connect the terminals.
- Run the simulation to verify functionality.

## Troubleshooting
- If you face issues, run the setup as Administrator.

## Requirements/project. 
- In this Arduino Stepper Control Project, requuirements are :
- Categories :- 
         **Hardware**
         a) Microcontroller 
           - Arduino Uno (fits according to Io pins requirements and stepper motor).
         b) Stepper motor 
           - Bipolar [4leaded]
         c) Motor driver
           - L293D
         d) Power supply 
           - 5V for stepper motor
           - 5-24V for L293D driver

        **Software**
        a) Arduino IDE
        - Download from Arduino Official Website.
        b) Required Libraries
        - Stepper.h (For basic stepper control)
        - AccelStepper.h (For advanced motion control like acceleration and deceleration)
        - Install via Arduino Library Manager (Sketch → Include Library → Manage Libraries).


        c) Arduino Code:
- Write the code to match the project needs [speed, direction and step precision]

```cpp
#include <Stepper.h>

#define STEPS 2048 // Steps per revolution for 28BYJ-48 motor

Stepper stepper(STEPS, 8, 10, 9, 11); // Define stepper motor control pins

void setup() {
    stepper.setSpeed(10); // Set speed in RPM
    Serial.begin(9600);
}

void loop() {
    Serial.println("Rotating Forward");
    stepper.step(STEPS); // Rotate one full revolution forward
    delay(1000);
    
    Serial.println("Rotating Backward");
    stepper.step(-STEPS); // Rotate one full revolution backward
    delay(1000);
}
```


## What's missing? 
 - LN2003 driver component is missing .
 - yo 


## Adding components to protues project

## Wiring Components - project 

## Arduino program/sketch


## Uploading sketch binary to simulation

-- configurations - clcok speed and effect 
-- eeprom configuration - whats eeprom in the first place. how to use it in this setup?  

- how about serial monitoring


## Conclusion

- It is an effective way of doing this at the end of the day.


### Resources 

1. Installation:https://www.labcenter.com 


** TODO **
- A component is missing on proteus - what next ?  