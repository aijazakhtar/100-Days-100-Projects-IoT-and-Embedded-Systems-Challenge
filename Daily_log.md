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

### Circuit Connections

- **Red LED**: Connect the anode (long leg) to digital pin 10 and cathode (short leg) to GND via a 220-ohm resistor.
- **Yellow LED**: Connect the anode to digital pin 9 and cathode to GND via a 220-ohm resistor.
- **Green LED**: Connect the anode to digital pin 8 and cathode to GND via a 220-ohm resistor.

## #Code

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
```

---
## Day 1: 8 LED Fun

### Objective
Create a circuit with eight LEDs to explore various lighting sequences and experiment with Arduino programming. This project introduces the use of `for` loops and arrays to manage multiple LED control with minimal code.

## Overview
In this experiment, we'll enhance the previous task by connecting eight LEDs. This circuit allows us to stretch the capabilities of the Arduino and experiment with different lighting animations. 

### Key Concepts
- **for() loops**: Useful for repeating a block of code multiple times.
- **arrays[]**: A collection of variables that can simplify the management of multiple items.

### Code Example
```cpp
/* 
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
    oneAfterAnotherNoLoop(); // Runs the LED animation function
    delay(1000);             // Wait for a second before the next sequence
    oneAfterAnotherLoop();   // Another LED animation
    delay(1000);             // Wait for a second before the next sequence
    oneOnAtATime();         // Turns on one LED at a time
    delay(1000);             // Wait for a second before the next sequence
    inAndOut();              // Runs in and out effect
    delay(1000);             // Wait for a second before restarting
}

// Function to light up LEDs one after another without looping
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

// Function to light up LEDs one after another using loops
void oneAfterAnotherLoop() {
    int delayTime = 100; // Time to pause between LEDs

    // Turn Each LED on one after another
    for (int i = 0; i <= 7; i++) {
        digitalWrite(ledPins[i], HIGH);  // Turns on LED #i
        delay(delayTime);                // Waits for delayTime milliseconds
    }

    // Turn Each LED off one after another
    for (int i = 7; i >= 0; i--) {
        digitalWrite(ledPins[i], LOW);   // Turns off LED #i
        delay(delayTime);                // Waits for delayTime milliseconds
    }
}

// Function to turn on one LED at a time
void oneOnAtATime() {
    int delayTime = 100; // Time to pause between LEDs

    for (int i = 0; i <= 7; i++) {
        int offLED = i - 1;  // Calculate which LED was turned on last time
        if (i == 0) {         // For i = 0, we turn off LED 7
            offLED = 7;
        }
        digitalWrite(ledPins[i], HIGH);     // Turn on LED #i
        digitalWrite(ledPins[offLED], LOW); // Turn off the last LED
        delay(delayTime);
    }
}

// Function to create an in-and-out effect with the LEDs
void inAndOut() {
    int delayTime = 100; // Time to pause between LEDs

    // Runs the LEDs out from the middle
    for (int i = 0; i <= 3; i++) {
        int offLED = i - 1; // Calculate which LED was turned on last time
        if (i == 0) {
            offLED = 3; // If i is 0, turn off LED 3
        }
        int onLED1 = 3 - i; // First LED to go on
        int onLED2 = 4 + i; // Second LED to go on
        int offLED1 = 3 - offLED; // Turn off the LED we turned on last time
        int offLED2 = 4 + offLED; // Turn off the LED we turned on last time

        digitalWrite(ledPins[onLED1], HIGH);
        digitalWrite(ledPins[onLED2], HIGH);
        digitalWrite(ledPins[offLED1], LOW);
        digitalWrite(ledPins[offLED2], LOW);
        delay(delayTime);
    }

    // Runs the LEDs into the middle
    for (int i = 3; i >= 0; i--) {
        int offLED = i + 1; // Calculate which LED was turned on last time
        if (i == 3) {
            offLED = 0; // If i is 3, turn off LED 0
        }
        int onLED1 = 3 - i; // First LED to go on
        int onLED2 = 4 + i; // Second LED to go on
        int offLED1 = 3 - offLED; // Turn off the LED we turned on last time
        int offLED2 = 4 + offLED; // Turn off the LED we turned on last time

        digitalWrite(ledPins[onLED1], HIGH);
        digitalWrite(ledPins[onLED2], HIGH);
        digitalWrite(ledPins[offLED1], LOW);
        digitalWrite(offLED2, LOW);
        delay(delayTime);
    }
}

```
---
## Day 2: Using Digital Input with Arduino UNO

### Project Overview

In today's project, we explore how to read a digital input signal using an Arduino UNO and report the signal state via the Serial Monitor. This project covers wiring a tact switch and a pull-up resistor to detect button presses.

### Components Needed

- **Arduino UNO**
- **Breadboard**
- **Tact Switch**
- **10k ohm Resistor**
- **Jumper Cables**

## Background Information

The digital pins on the Arduino UNO operate at a 5V rating. In this setup:
- **Logic-1 (HIGH)**: Connected to a 5V power supply through a 10k ohm pull-up resistor.
- **Logic-0 (LOW)**: Achieved by pressing the tact switch, which shorts the input pin to ground.

By default, when the tact switch is open, the input pin reads **5V**. When pressed, it grounds the pin to **0V**. The 10k ohm resistor limits the current when the switch is pressed, preventing damage to the Arduino.

## Schematic Diagram


## Breadboard Wiring Instructions

1. **Connect the 10k ohm Resistor** between the digital pin 12 and the 5V supply.
2. **Attach the tact switch** so that it connects digital pin 12 to ground when pressed.
3. **Ensure correct orientation** of the tact switch; otherwise, the signal will always remain grounded.

## Code

```cpp
/*
– Digital Input
*/

const int buttonPin = 12;     // Use digital pin 12 for the button pin
int buttonState = 0;          // variable for storing the button status

void setup() {
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT);  
  // initialize the serial port;
  Serial.begin(9600);  // start serial for output 
}

void loop(){
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);
  
  // Output button state
  Serial.print("The button state is ");
  Serial.println(buttonState);
  
  // Delay 1000ms
  delay(1000);
} 
```
### Expected Output
-**Default State**: The Serial Monitor should show a buttonState of 1.
-**Button Pressed**: When the button is pressed, buttonState changes to 0.
### Key Concepts Covered
- Using a digital input pin with Arduino
- Reading and printing digital pin states on the Serial Monitor
### Notes
- The 10k ohm resistor ensures only a small current flows from the 5V source when the button is pressed, protecting the circuit components. Adjust the button pin or delay time as desired to customize your setup.
---
## Day 2: LED Game with Arduino UNO

### Project Overview

Today, we created a simple game using the Arduino UNO that combines digital input and output pins to control LEDs in sequence. The objective is to stop the LED sequence precisely when the green LED is lit by pressing a button. Each successful attempt increases the game’s speed, enhancing the difficulty level.

### Components Needed

- **Arduino UNO**
- **Breadboard**
- **4 LEDs** (White, Yellow, Green, Red)
- **Resistors**
  - (appropriate for LEDs or 220 / 330 ohm)
  - 10K ohm
- **Jumper Cables**
- **Tact Switch**

### Schematic Diagram

### Breadboard Wiring Instructions

1. **Digital Input Pin**: Connect the tact switch to digital pin 12 and GND, connect 10K ohm resister between 5V and digital pin 12.
2. **Digital Output Pins**:
   - Connect the anode (long leg) of White LED to pin 2 and cathode (short leg) to GND via a 220-ohm resistor.
   - Connect the anode (long leg) of Yellow LED to pin 3 and cathode (short leg) to GND via a 220-ohm resistor.
   - Connect the anode (long leg) of Green LED to pin 4 and cathode (short leg) to GND via a 220-ohm resistor.
   - Connect the anode (long leg) of Red LED to pin 5 and cathode (short leg) to GND via a 220-ohm resistor.

### Code
```cpp
/*
  – Digital Input and Output Game
  In this game, the LED will loop from white, yellow, green, red
  then back to white. The goal is to press the push button at the exact
  moment when the green LED is ON. Each time you get it right, the LED
  will speed up and the difficulty will increase.
*/

int currentLED = 2;
int delayValue = 200;

void setup() {
  // Initialize digital pin 12 as input for the button
  pinMode(12, INPUT);
  
  // Initialize digital pins 2 to 5 as outputs for LEDs
  pinMode(2, OUTPUT);   // White LED
  pinMode(3, OUTPUT);   // Yellow LED
  pinMode(4, OUTPUT);   // Green LED
  pinMode(5, OUTPUT);   // Red LED
}

int checkInput() { 
  return (digitalRead(12) == 0) ? 1 : 0;
}

void loop() {
  // Check if the button is pressed at the right moment
  if (digitalRead(12) == 0) {
    if (currentLED == 4) {
      // Blink the correct (green) LED to indicate success
      for (int i = 0; i < 2; i++) {
        digitalWrite(4, HIGH);
        delay(200);
        digitalWrite(4, LOW);
        delay(200);
      }
      // Speed up the game
      delayValue -= 20;
    } else {
      // Blink the incorrect LED to indicate failure
      for (int i = 0; i < 2; i++) {
        digitalWrite(currentLED, HIGH);
        delay(200);
        digitalWrite(currentLED, LOW);
        delay(200);
      }
    }
  }

  // Cycle through the LEDs (white -> yellow -> green -> red)
  digitalWrite(currentLED, HIGH);
  delay(delayValue);
  digitalWrite(currentLED, LOW);
  delay(delayValue);
  currentLED++;
  if (currentLED > 5) {
    currentLED = 2;
  }
}
```
### Code Explanation
- **Setup**: Sets pin 12 as input (for button) and pins 2 to 5 as outputs (for LEDs).
- **Loop**:
  - Checks if the button is pressed when the green LED is lit.
  - Correct guess triggers a success blink on the green LED and increases game speed.
  - Incorrect guess blinks the current LED without speeding up the game.
  - Loops through LEDs in the sequence: white -> yellow -> green -> red.
### How to Play
- **Objective**: Press the button exactly when the green LED is on.
- **Scoring**: Each successful press increases the speed, making it more challenging.
- **Reset**: Press the reset button on the UNO R3 to start over.
### Key Concepts Covered
- Using digital input and output pins together.
- Implementing a game loop and changing speed based on input.
### Notes
- This game demonstrates how to use digital I/O in combination to create interactive projects. Experiment with different LED sequences or increase/decrease the difficulty by adjusting delayValue.
---
## Day 2: Building a Voltage Meter with Arduino UNO

### Project Overview

Today, we built a basic voltage meter using the analog input on the Arduino UNO. The voltage meter reads the voltage from a voltage divider circuit made with a resistor and a potentiometer, then displays the voltage on the serial monitor.

### Components Needed

- **Arduino UNO**
- **Breadboard**
- **1kΩ Potentiometer**
- **1kΩ Resistor**
- **Jumper Cables**

### Background Information

The analog input on the UNO reads a voltage range from 0V to 5V and converts it to a digital value between 0 and 1023 using a 10-bit ADC. This gives a resolution of about 4.89mV per unit. Using a 1kΩ resistor and a 1kΩ potentiometer, we created a voltage divider that allows us to feed an adjustable voltage between 0V and 2.5V to the analog input pin A0.

### Voltage Calculation

The voltage at the sensor input can be calculated using the formula:

    V_sensor_input = 5V * (R1 / (R1 + 1kΩ))

where R1 is the resistance set by the potentiometer.


### Schematic Diagram

### Breadboard Wiring Instructions

1. **Analog Input**: Connect the middle pin of the potentiometer to analog pin A0 on the UNO.
2. **Voltage Divider Circuit**:
   - One side of the potentiometer to ground.
   - The other side of the potentiometer to 5V through a 1kΩ resistor.

### Code

```cpp
/*
  Volt Meter
*/
int sensorPin = A0;       // select the analog input pin
int sensorValue = 0;      // variable to store the value coming from the sensor
float sensorVoltage = 0;  // variable to store the voltage

void setup() {
  Serial.begin(9600);     // start serial communication
}

void loop() {
  // Read the value from the analog input pin
  int sensorValue = analogRead(sensorPin);   
  
  // Convert sensor value to voltage
  float sensorVoltage = sensorValue * (5.0 / 1023.0);
  
  // Print the voltage
  Serial.print("The voltage is ");
  Serial.println(sensorVoltage);
  
  // Delay by 1000 milliseconds
  delay(1000);                 
}
```
### Code Explanation
- **Setup**: Starts serial communication at 9600 baud for displaying voltage readings.
- **Loop**:
  - Reads the analog value from pin A0.
  - Converts this analog value to voltage.
  - Prints the voltage reading to the serial monitor.
  - Delays for 1 second to create a readable update frequency.
### How to Use
  - Adjust the potentiometer to vary the voltage at the input.
  - Observe the voltage change in real-time on the serial monitor.
### Key Concepts Covered
  - Using the analog sensor on the Arduino UNO R3.
  - Building and using a voltage divider circuit with a potentiometer.
### Notes
  - This project introduced the basics of analog voltage reading and real-time monitoring using a serial interface. Adjusting the potentiometer allows you to simulate voltage changes, a foundational concept for analog sensor applications.
---
## Day 2 Log: Arduino LED Dice Game 🎲

### Project Overview
Today’s project was to build an LED dice simulator using the Arduino UNO. By pressing a button, this setup simulates a dice roll, randomly lighting up a number of LEDs (from 1 to 6) to represent the dice number.

### Components Needed
- **1 x Arduino UNO**
- **6 x LEDs** (for each dice face)
- **6 x 220Ω resistors** (for each LED)
- **1 x Button switch**
- **1 x 10KΩ resistor** (for button switch)
- **Jumper cables**
- **Breadboard**

### Circuit Diagram
- **LEDs**: Connected to digital pins 2 through 7, each with a 220Ω resistor.
- **Button**: Connected to digital pin 12 to act as the dice roll trigger and pullup resister between 5V and digital pin 12.

### Code Walkthrough

#### 1. Pin Setup
```cpp
int first = 2;
int second = 3;
int third = 4;
int fourth = 5;
int fifth = 6;
int sixth = 7;
int button = 12;
int pressed = 0;

void setup() {
  // Initialize LED pins
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);

  // Initialize button pin
  pinMode(button, INPUT);

  // Set up a random seed from an unconnected analog pin
  randomSeed(analogRead(0));
  Serial.begin(9600);
}
```
#### Simulating Tension
  - To build suspense, the LEDs light up sequentially from left to right and then back.
```cpp
void buildUpTension() {
  for (int i=first; i<=sixth; i++) {
    if (i!=first) digitalWrite(i-1, LOW);
    digitalWrite(i, HIGH);
    delay(100);
  }
  for (int i=sixth; i>=first; i--) {
    if (i!=seventh) digitalWrite(i+1, LOW);
    digitalWrite(i, HIGH);
    delay(100);
  }
}
```
#### Displaying the Dice Roll
  - A random number between 1 and 6 lights up the corresponding number of LEDs to display the dice result.

```cpp
void showNumber(int number) {
  digitalWrite(first, HIGH);
  if (number >= 2) digitalWrite(second, HIGH);
  if (number >= 3) digitalWrite(third, HIGH);
  if (number >= 4) digitalWrite(fourth, HIGH);
  if (number >= 5) digitalWrite(fifth, HIGH);
  if (number == 6) digitalWrite(sixth, HIGH);
}
```
#### Dice Roll Logic
  - If the button is pressed, the dice roll is initiated, building suspense and then displaying a random result.

```cpp
void loop() {
  pressed = digitalRead(button);
  if (pressed == HIGH) {
    setAllLEDs(LOW);
    buildUpTension();
    int thrownNumber = throwDice();
    showNumber(thrownNumber);
  }
}
```
### What I Learned
  - Using digital input/output pins together.
  - Implementing randomization for simulating a dice throw.
  - Creating a suspense effect by sequencing LED lights.
### Next Steps
  - Try customizing the code by changing LED blink speed or adding different suspense effects before the dice roll.
---
## Day 2 Log: 10-LED Bar Graph Meter

### Project Overview
Today’s project involved building a 10-LED bar graph meter using a potentiometer and Arduino UNO. The brightness level of each LED indicates the potentiometer's analog input value, effectively visualizing sensor readings.

### Components Needed
- **1 x Arduino UNO**
- **10 x LEDs** (for bar graph display)
- **10 x 220Ω resistors** (for each LED)
- **1 x Potentiometer** (for input control)
- **Breadboard** and **Jumper cables**

### Circuit Diagram
- **LEDs**: Connected to digital pins 2 through 11, each with a 220Ω resistor.
- **Potentiometer**: Connected to analog pin A0.and other two pins of potentiometer to 5V and GND.

### Code Walkthrough

#### 1. Pin and Array Setup
```cpp
const int analogPin = A0;   // potentiometer connected here
const int ledCount = 10;    // number of LEDs in the bar graph

int ledPins[] = {2, 3, 4, 5, 6, 7, 8, 9, 10, 11}; // LED pins
void setup() {
  for (int thisLed = 0; thisLed < ledCount; thisLed++) {
    pinMode(ledPins[thisLed], OUTPUT);
  }
}
```
#### Potentiometer Input to LED Level Mapping
  - This section reads the potentiometer value and maps it to the LED levels.
```cpp
void loop() {
  int sensorReading = analogRead(analogPin);
  int ledLevel = map(sensorReading, 0, 1023, 0, ledCount);

  for (int thisLed = 0; thisLed < ledCount; thisLed++) {
    if (thisLed < ledLevel) {
      digitalWrite(ledPins[thisLed], HIGH);  // turn on LEDs up to the level
    } else {
      digitalWrite(ledPins[thisLed], LOW);   // turn off LEDs beyond the level
    }
  }
}
```
### What I Learned
  - Using an analog input (potentiometer) to control multiple digital outputs (LEDs).
  - Mapping sensor values to a specific range for bar graph visualization.
  - Implementing array-based looping for efficient control of multiple LEDs.
### Next Steps
  - Explore using different sensors (e.g., a light sensor) in place of the potentiometer for various types of bar graph visualizations.
---
## Day 2 Log: Roulette Game with Arduino

### Project Overview
Today's project involved creating a **Roulette game** using an Arduino and an array of LEDs. This game allows players to set difficulty levels, spin a light "roulette," and try to stop it at the winning LED. A button is used to select difficulty and play the game, with lights indicating game progress and outcomes.

### Components Needed
- **1 x Arduino UNO**
- **9 x LEDs** (to form the "roulette" circle)
- **9 x 220Ω resistors** (one for each LED)
- **1 x Button** (to control the game)
- **Breadboard** and **Jumper cables**

### How to Play
#### Basics of the Game
The game is inspired by roulette and combines elements of chance and timing. Players set a difficulty level, which controls the speed of the LEDs. Then, they "spin" the LEDs and attempt to stop the movement at the "winning" LED to win the game.

#### Rules to Play
1. **Choose Difficulty**: Press the button to cycle through difficulty levels, represented by LEDs lighting up one by one.
   - Each click increases the difficulty (and speed). When the final LED lights up, it resets to the first position.
2. **Start the Game**: Double-click the button to confirm your difficulty level. The game starts immediately after.
3. **Spin the LEDs**: The LEDs light up sequentially in a "roulette" motion, moving faster as difficulty increases.
4. **Stop the Roulette**: Press the button again to try to land on the "winning" LED (the middle LED in the sequence).
5. **Win or Lose**: 
   - If the lit LED stops on the middle LED, you win!
   - If it stops elsewhere, the game ends, and you can try again.

### Code Walkthrough

#### 1. Pin Setup and Variables
This section initializes the pins for LEDs and the button and sets flags for the game.
```cpp
#include <TTBOUNCE.h>   // Button debouncing library

int delay_time = 0;
const int led_array[9] = {4, 3, 5, 6, 7, 8, 9, 10, 11};
const int button = 2;
int difficulty = 0;
int current_led = 0;
bool dir_flag = true;   // true goes right, false goes left
bool game_ended = false;
bool is_win = false;
bool is_finished_selecting = false;

TTBOUNCE b = TTBOUNCE(button); // Initialize the button with debounce
```
#### 2. Button Clicks for Setting Difficulty and Starting Game
  - **Single click**: Increases difficulty level (indicated by the LED position).
  - **Double click**: Starts the game with the chosen difficulty.
```cpp
void click(){
  Serial.print("Click | ");
  digitalWrite(led_array[difficulty], LOW);
  difficulty++;
  if (difficulty > 8) difficulty = 0;
  digitalWrite(led_array[difficulty], HIGH);
  Serial.println("Difficulty is: " + String(difficulty));
  delay(100);
}

void doubleClick(){
  Serial.println("Double click");
  is_finished_selecting = true;
  delay_time = floor(500 / (difficulty + 1));
  Serial.println("Difficulty: " + String(delay_time));
  sweep();
}
```
#### 3. Game Setup and LED Initialization
  - Sets LED pins to OUTPUT and starts the game with difficulty selection.

```cpp
void setup() {
  Serial.begin(9600);
  b.attachDoubleClick(doubleClick);
  b.attachClick(click);
  b.setActiveLow();
  b.enablePullup();

  for (int i = 0; i < 9; i++) pinMode(led_array[i], OUTPUT);

  sweep();
  pulse();

  difficulty = 0;
  digitalWrite(led_array[difficulty], HIGH);
  while (!is_finished_selecting) b.update();
  
  b.update();
  pinMode(button, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(button), button_pressed, FALLING);
  delay(1000);
}
```
#### 4. Main Game Loop
  - Moves the lit LED back and forth to simulate a roulette motion. When the button is pressed, it checks if the game has ended and if the player has won.

```cpp
void loop() {
  if (!game_ended) {
    move_led();
    delay(delay_time);
  } else if (game_ended) {
    Serial.println("Game over");
    if (is_win) {
      Serial.println("You won!");
      for (int i = 0; i < 5; i++) {
        pulse();
        delay(100);
      }
    }
    sweep();
    game_ended = false;
    is_win = false;
    delay(2000);
  }
}
```
#### 5. LED Motion, Sweeping, and Pulse Effects
  - **move_led**: Controls the movement of the lit LED based on direction.
  - **sweep and pulse:** Create visual effects on the LEDs for game feedback.
```cpp
void move_led() { /* Moves the LED based on direction flags */
  digitalWrite(led_array[current_led], LOW);
	if(current_led == 8){
		dir_flag = false;
		current_led -= 1;
	}
	
	else if(current_led == 0){
		dir_flag = true;
		current_led += 1;
	}
	
	else if(dir_flag){
		current_led += 1;
	}
	
	else if(!dir_flag){
		current_led -= 1;
	}
	digitalWrite(led_array[current_led], HIGH);
 }
void pulse() {
 /* Pulses all LEDs simultaneously */
for(int i=0; i<9;i++){
		digitalWrite(led_array[i], HIGH);
	}
	
	delay(100);
	
	for(int i=0; i<9;i++){
		digitalWrite(led_array[i], LOW);
}
void sweep() {
 /* Sweeps the LEDs back and forth */
for(int i=0; i<9;i++){
		digitalWrite(led_array[i], HIGH);
		delay(50);
		digitalWrite(led_array[i], LOW);
	}
	
	for(int i=8; i>=0;i--){
		digitalWrite(led_array[i], HIGH);
		delay(50);
		digitalWrite(led_array[i], LOW);
	}
 }
void button_pressed(){
  Serial.println("Button pressed on LED: "+String(current_led));
	game_ended = true;
	if(current_led==4){
		is_win = true;
	}
	else if(current_led != 4){
		is_win = false;
	}
 current_led = 0;
 delay(500);
}

```
### What I Learned
  - Using button debouncing with the TTBOUNCE library for smooth button interactions.
  - Controlling multiple LEDs with direction flags and sequential lighting.
  - Programming a simple game loop that adjusts based on user input and game states.
### Next Steps
  - Explore adding sound effects or creating a digital display to show the score. Experiment with different LED patterns to enhance the gameplay experience.

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

