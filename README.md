# Debouncing Circuits and Edge Detection using FSMs

This project involves the design and implementation of FSM-based modules for debouncing a switch and detecting edges. The modules are implemented in Verilog and synthesized for FPGA programming. The FPGA used is Nexys Artix-7 100T with CSG324 chip.
![350768424-00b7968c-1de6-4379-9cda-a7d86f0c6599](https://github.com/user-attachments/assets/7b1d3acb-16c9-45dc-85f8-34dbab1424d1)


## Overview

Switches are often prone to noise, which can cause multiple transitions (bounces) when pressed or released. This project aims to address this issue by creating a debouncing circuit. Additionally, an edge detector is implemented to detect rising and falling edges of the switch signal.

## Features

- **FSM Design**: Created finite state machine (FSM) modules for debouncing and edge detection.
- **Verilog Coding**: Implemented the FSMs using Verilog hardware description language.
- **Design Synthesis**: Synthesized the design for FPGA implementation.
- **Bitstream Generation**: Generated bitstreams for programming the FPGA.
- **FPGA Programming**: Programmed the FPGA to implement the practical button using the developed modules.
- **Checking and Verification**: Verified the functionality of the modules on the FPGA.

## Description

The project is focused on implementing a reliable edge detection mechanism when a button is pressed, ensuring accurate edge counting by eliminating false edges through debouncing. In many digital systems, mechanical buttons often produce spurious signals known as "bounces" when pressed or released, which can lead to multiple unwanted edge detections. To address this, the design incorporates a debouncing unit that filters out these false signals, ensuring that only legitimate button presses are recognized and counted.

### Design Overview:

1. **Debouncing Mechanism:**
   - The debouncing logic is implemented using a Finite State Machine (FSM) that is specifically designed to ignore any spurious edges resulting from button bounce. The FSM only acknowledges an edge if it persists for a duration longer than a predefined time threshold, set to 20 milliseconds in this case. This ensures that only intentional and sustained button presses are counted.
   - The FSM transitions through states that monitor the button's input signal. If the signal remains stable for the required duration, it is considered a valid edge, and the FSM proceeds to register it as a legitimate press. If the signal fluctuates within the debounce period, the FSM resets, effectively ignoring the false edge.

2. **Synchronization to Prevent Metastability:**
   - To handle the asynchronous nature of the button press with respect to the system clock, a 2-stage synchronizer is employed. This is crucial for avoiding metastability, a state where the system could behave unpredictably due to the asynchronous input. The synchronizer ensures that the button press signal is properly aligned with the system clock, providing a stable input for the FSM.

3. **Verification Through Counter Increment:**
   - The effectiveness of the debouncing mechanism is verified by incrementing a counter each time the button is pressed. Two counters are used in the system: one that increments based on raw, unfiltered button presses and another that increments only after the debouncing logic has verified the press. This allows for a direct comparison between the two counts, demonstrating the impact of debouncing on eliminating false edges.

4. **Seven-Segment Display Integration:**
   - The output from both counters (with and without debouncing) is displayed on a seven-segment display connected to an FPGA board. To achieve this, the system includes carefully designed combinational logic and multiplexing to manage the display of multiple digits. 
   - A custom timer and counter-based refresh rate mechanism is employed to ensure that the display is updated consistently and smoothly. The display logic ensures that each digit is refreshed at a rate that prevents flickering, while still being fast enough to appear continuous to the human eye.

### Conclusion:

This project successfully implements a robust edge detection system that is capable of filtering out noise from button presses using an FSM-based debouncing technique. The inclusion of synchronization stages prevents metastability, and the entire system is verified through comparison of counters, with results clearly displayed on an FPGA board's seven-segment display. The design demonstrates careful consideration of timing, signal integrity, and user interaction in digital systems.

## Simulation and Verification

The noisy push button was simulated first on a testbench and results were verified on Xilinx Vivado. Further, it was tested on a FPGA to confirm the debouncing action of the mechanical push buttons of the FPGA.

### Xilinx Vivado Simulation

<img width="959" alt="339135616-dcd7ff33-eb96-4257-942d-ea7cb6508bd4" src="https://github.com/user-attachments/assets/d7739aa0-3a91-4e25-8a30-fed84187066a">


### Schematic
<img width="938" alt="339137157-a0f6087d-cdfa-45c6-828a-5e352a630c1e" src="https://github.com/user-attachments/assets/727cd59a-3002-41c1-a211-9486422f4cbb">

