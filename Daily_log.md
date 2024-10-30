# 📅 100 Days, 100 Projects: Daily Log

This file serves as a daily record of progress, discoveries, and challenges for each project day. This log will track growth and document all learning milestones.

---

## Day 1:  Arduino IDE Installation and First LED Blink

**Date**: 10/30/2024

**Objectives**:
  - Install Arduino IDE 2.3.3, set up the Arduino Uno, and run a basic LED blink to confirm the setup.
  - Controlling Digital Outputs

### Steps

1. **Download and Install Arduino IDE 2.3.3**:
   - Go to the [Arduino IDE Download page](https://www.arduino.cc/en/software).
   - Select **Arduino IDE 2.3.3** for your operating system (Windows, macOS, or Linux).
   - Follow the installation instructions for your system:
     - **Windows**: Run the downloaded `.exe` file and follow the setup wizard.
     
2. **Connect the Arduino Uno**:
   - Use a USB cable to connect the Arduino Uno to your computer.
   - Open the Arduino IDE.
   - Go to **Tools > Port** and select the port where the Arduino Uno is connected.
   - Under **Tools > Board**, select **Arduino Uno**.

3. **Test the Arduino with the Built-in Blink Example**:
   - Open the **Blink example** in the IDE:
     - Go to **File > Examples > 01.Basics > Blink**.
   - Review the code (it should be a simple `digitalWrite()` function turning the onboard LED on and off).
   - Click the **Upload** button (right arrow) to upload the code to the Arduino.

4. **Observe the Onboard LED**:
   - Once the code uploads, the onboard LED (usually on pin 13) should start blinking on and off in 1-second intervals.
   - experiment with the sketch and see how it alters the behavior of the LED.  For instance, try changing the delay(1000) to delay (2000) or changing delay(1000) to delay(500).
### Observations & Results
- **What Worked**: Successfully installed the IDE, connected the board, and ran the blink example.
- **What Didn’t Work**: N/A

### Notes
- **Challenges**: None encountered; the board worked perfectly.
- **Useful Note**: A typical Arduino sketch consists of two main procedures, a “setup” functions and a “loop” procedure.   The “setup” function gets executed one time only every time the board is power cycle or reset, and it is mainly use for defining the default or initial behavior.  The “loop” function gets executed continuously.
- **Learning**: This exercise clarified the basics of uploading code to the board and using the `digitalWrite()` function.

## Day 1: LED Circuit Setup on Breadboard with Resistor Calculation

## Objective
Assemble an LED circuit on a breadboard using the Arduino UNO board, size a suitable resistor for safe LED operation, and program digital pins to control each LED.

---

## Steps

### Components & Setup
- **Gathered Components**: Arduino UNO, USB cable, breadboard, LEDs, 330-ohm resistors, and jumper cables.
- **Digital Pins Overview**: Arduino UNO outputs 5V at logic-1, which is compatible with a 330-ohm resistor for typical LEDs.

### Resistor Calculation
Using Ohm’s law to find the minimum resistor value for a 5V source and LED with a 2V forward voltage (Vf) and 20mA current (If):
- **Formula**: R = V / I
- **Calculation**: R = (5V - 2V) / 0.02A = 150Ω
- **Resistor Used**: 330-ohm resistor chosen to keep the current below 20mA, protecting the LED. ( We can use resister from 150Ω to 470Ω)

### Circuit Assembly
1. Connected 330-ohm resistors in series with each LED on the breadboard.
2. Wired digital pins 2, 3, 4, and 5 on the Arduino UNO to the LEDs.
   - Positive lead of each LED connects to the resistor, and the negative lead goes to the ground rail.

### Writing the Code
Created a new project in Arduino IDE and used the following code to set up digital pins 2-5 as outputs, toggling each LED sequentially.

```cpp
void setup() {
    pinMode(2, OUTPUT);
    pinMode(3, OUTPUT);
    pinMode(4, OUTPUT);
    pinMode(5, OUTPUT);
}

void loop() {
    digitalWrite(2, HIGH);
    delay(500);
    digitalWrite(2, LOW);
    digitalWrite(3, HIGH);
    delay(500);
    digitalWrite(3, LOW);
    digitalWrite(4, HIGH);
    delay(500);
    digitalWrite(4, LOW);
    digitalWrite(5, HIGH);
    delay(500);
    digitalWrite(5, LOW);
}
```
### Testing
- Uploaded the code to the Arduino UNO board.
- Verified LEDs blinked in sequence as programmed, confirming proper wiring and resistor sizing.

### Observations & Results
- **What Worked**: LEDs blinked in sequence as programmed, confirming correct wiring and resistor choice.
- **What Didn’t Work**: No issues encountered.

### Notes
- **Challenges**: Ensured correct LED orientation and resistor placement to prevent circuit errors.
- **Learning**: Understood resistor sizing for LEDs and gained confidence in basic circuit setup and Arduino programming.
---
## Traffic Light Project

### Project Overview

This project simulates a traffic light system using three LEDs (Red, Yellow, Green) controlled by an Arduino. The LEDs will light up in a sequence that mimics real traffic lights, providing a practical example of basic electronics and programming.

### Components Needed
- **Arduino Board** (Arduino UNO)
- **3 LEDs** (Red, Yellow, Green)
- **3 Resistors** (220 ohms or 330 ohms)
- **Breadboard and Jumper Wires**

## Circuit Connections

- **Red LED**: Connect the anode (long leg) to digital pin 10 and cathode (short leg) to GND via a 220-ohm resistor.
- **Yellow LED**: Connect the anode to digital pin 9 and cathode to GND via a 220-ohm resistor.
- **Green LED**: Connect the anode to digital pin 8 and cathode to GND via a 220-ohm resistor.

## Code

```cpp
// Traffic Light Simulation with LEDs

// Define LED pin numbers
const int redLED = 10;
const int yellowLED = 9;
const int greenLED = 8;

void setup() {
    // Set LED pins as outputs
    pinMode(redLED, OUTPUT);
    pinMode(yellowLED, OUTPUT);
    pinMode(greenLED, OUTPUT);
}

void loop() {
    // Red Light
    digitalWrite(redLED, HIGH);
    delay(5000); // Wait for 5 seconds
    digitalWrite(redLED, LOW);

    // Yellow Light
    digitalWrite(yellowLED, HIGH);
    delay(2000); // Wait for 2 seconds
    digitalWrite(yellowLED, LOW);

    // Green Light
    digitalWrite(greenLED, HIGH);
    delay(5000); // Wait for 5 seconds
    digitalWrite(greenLED, LOW);

    // Yellow Light again before switching to red
    digitalWrite(yellowLED, HIGH);
    delay(2000); // Wait for 2 seconds
    digitalWrite(yellowLED, LOW);
}
'''

---
## Day 1: 8 LED Fun

### Objective
Create a circuit with eight LEDs to explore various lighting sequences and experiment with Arduino programming. This project introduces the use of `for` loops and arrays to manage multiple LED control with minimal code.

## Overview
In this experiment, we'll enhance the previous task by connecting eight LEDs. This circuit allows us to stretch the capabilities of the Arduino and experiment with different lighting animations. 

### Key Concepts
- **for() loops**: Useful for repeating a block of code multiple times.
- **arrays[]**: A collection of variables that can simplify the management of multiple items.

## Code Example
```cpp
/*     ---------------------------------------------------------
 *  A few Simple LED animations
 */

// LED Pin Variables
int ledPins[] = {2, 3, 4, 5, 6, 7, 8, 9}; // Array to hold pin numbers

void setup() {
    // Set each pin connected to an LED to output mode
    for (int i = 0; i < 8; i++) {
        pinMode(ledPins[i], OUTPUT);
    }
}

void loop() {
    oneAfterAnotherNoLoop(); // Run the LED animation function
}

// Function to light up LEDs one after another
void oneAfterAnotherNoLoop() {
    int delayTime = 100; // Time to pause between LEDs
    for (int i = 0; i < 8; i++) {
        digitalWrite(ledPins[i], HIGH);
        delay(delayTime);
    }
    for (int i = 7; i >= 0; i--) {
        digitalWrite(ledPins[i], LOW);
        delay(delayTime);
    }
}

// Additional functions for various animations can be added below
---
## Day 2: _[Project Title Here]_

**Date**: _[Enter Date Here]_

**Objective**: _[Briefly Describe Today’s Goal or Project]_

### Steps

1. _[List step-by-step actions taken]_

### Observations & Results
- **What Worked**: _[Summarize successful actions/results]_
- **What Didn’t Work**: _[Describe issues or challenges faced]_

### Notes
- **Challenges**: _[Record any obstacles and solutions]_
- **Learning**: _[Document new insights or skills learned]_

---

## Template for Following Days

For each day, copy the following structure and fill it out:

**Date**: 10/30/202

**Objective**: _[Briefly Describe Today’s Goal or Project]_

### Steps
1. _[List step-by-step actions taken]_

### Observations & Results
- **What Worked**: _[Summarize successful actions/results]_
- **What Didn’t Work**: _[Describe issues or challenges faced]_

### Notes
- **Challenges**: _[Record any obstacles and solutions]_
- **Learning**: _[Document new insights or skills learned]_

---

This format will be updated daily to document each project, troubleshoot challenges, and keep track of learning outcomes across the 100-day challenge.

