#  Interactive LED Stage Lighting Controller

##  Project Overview
This project is a custom-built, interactive LED lighting system designed to provide dynamic ambient and stage lighting for University of Louisville cultural showcases (such as Jalsa and Derby City Dhoom). 

The system bridges hardware engineering and software design. It utilizes an Arduino microcontroller running C++ (via the FastLED library) to drive multiple WS2812B addressable LED strips simultaneously. A core feature of the system is a custom-soldered hardware button interface that allows organizers to seamlessly toggle lighting states live during a performance.

##  Hardware Engineering & Assembly
Building this system required physical fabrication and circuit design to ensure reliability during a live event.
* **Microcontroller:** Arduino Uno/Nano.
* **LED Hardware:** 5 separate WS2812B addressable LED strips (5V).
* **Fabrication (Soldering):** All data lines, power distribution rails, and ground wires were manually soldered to ensure stable connections that could withstand movement and setup stress.
* **Physical Control Interface:** Integrated a physical push-button wired to a digital interrupt pin (Pin 2). The circuit utilizes the Arduino's internal pull-up resistor (`INPUT_PULLUP`), meaning the button safely grounds the circuit when pressed to trigger a state change without requiring external resistors.

##  Software & Logic Design
The codebase manages concurrent data streams to multiple digital pins while listening for hardware interrupts.

### The Core Controller (`FiveStrips_ButtonToggle`)
* **Concurrent Arrays:** Manages 5 separate `CRGB` arrays, allowing simultaneous, synchronized animations across all strips without severe frame-rate drops.
* **Debounce Logic:** Implements a software debounce delay (`delay(50)`) to prevent the hardware button from registering false double-clicks due to physical mechanical vibration.
* **State Toggling:** Uses a boolean tracker (`ledsOn`) to flip between a deactivated state and a cascading warm-white visual effect, giving the stage crew instant control.

###  Visual Effects Library
In addition to the main stage controller, several modular visual effects were programmed for different event moods:
* **`Fire_effect`**: Utilizes randomization math to mimic the volatile flickering of a real flame, shifting between bright reds, oranges, and dim embers.
* **`Rainbow_effect`**: Leverages HSV (Hue, Saturation, Value) color space to smoothly iterate a rainbow across the strip.
* **`Running_dot_effect`**: Uses FastLED's `beatsin16` and `fadeToBlackBy` functions to create a smooth, pulsing "comet" trail that runs back and forth.
* **`Sparkle_effect`**: Randomly injects bright flashes onto a fading background to create a starry, glittering visual.

##  Setup & Dependencies
* **Language:** C++ (Arduino framework)
* **Library:** [FastLED](https://github.com/FastLED/FastLED)
* **Wiring Warning:** When recreating this setup, ensure the LED power supply shares a common ground with the Arduino to prevent erratic data signal behavior.



**Screenshots** 
![IMG_2790](https://github.com/user-attachments/assets/0d68d422-1d64-4d18-8756-3de35d27c3b9)


![IMG_2791](https://github.com/user-attachments/assets/43099324-bead-4c56-b328-e54270e0bf08)

---
*Developed by: Salok Samant*
