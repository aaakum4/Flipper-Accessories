# Flipper-Accessories
Now that I have made a custom Flipper, I use create some accessories for it to go with.

A custom expansion board for the Flipper Zero that adds WiFi capability and a high-power IR blaster, designed with safety, flexibility, and future expansion in mind.

This project was designed specifically for my custom Flipper Zero build, which can be found here:
https://github.com/aaakum4/Sorta-Flipper-Zero

While the designs and files are shared openly, they should not be blindly copied or connected to a stock Flipper Zero without understanding the electrical implications. Component choices, power rails, and protection methods were selected with my particular setup and use case in mind.
If you choose to reuse or adapt any part of this project, please make sure it will work with whatever device you are using.

## Overview
This project combines two main subsystems:
- A WiFi board built around the ESP32-S2-WROVER-N4R2 for networking and future firmware experiments
- A 960 nm IR blaster designed for high-power pulsed output while keeping the Flipper electrically isolated

The goal wasn’t just to make something that works, but to make something that’s understandable, modifiable, and safe to plug into a Flipper.

## The WiFi Board
The WiFi side uses the ESP32-S2-WROVER-N4R2, which offered more than enough performance without being unnecessarily complex. Since this board is meant to be reused and extended, several design choices were made with development and debugging in mind:
- Spare GPIO pins left uncommitted for future features
- JTAG and UART exposed for debugging and flashing
- Dedicated BOOT and RESET buttons to avoid relying on awkward software-only recovery

Rather than pushing for maximum performance, the focus here was reliability, ease of development, and not boxing the design into a single use case.

## IR Blaster
The IR blaster uses seven 960 nm IR LEDs, arranged as three series pairs plus one standalone LED, which allowed higher optical output while still working comfortably from a 5 V rail.

A logic-level MOSFET is used for switching instead of a transistor, keeping all high current paths away from the Flipper’s GPIO pins and allowing clean, efficient pulsed operation. The circuit is intended for modulated IR (rather than continuous drive), which makes higher peak currents practical without excessive heat.

This part of the design involved a lot of trade-offs around current, voltage, and safety, and ended up being more conceptually challenging than the WiFi board despite using fewer components.

## Safety & Protection
A core design requirement was ensuring that the Flipper Zero is not put at risk, even in the event of a fault or design mistake. To that end:
- GPIO pins are only ever used as logic-level control signals
- High-current loads are fully isolated using switching components
- Current is limited where appropriate
- No direct power paths exist that could back-feed into the Flipper

The aim was to make the board something you can plug in without constantly worrying about damaging the host device.

## Making the PCB
Here is the final Wifi PCB:
<img width="1308" height="684" alt="image" src="https://github.com/user-attachments/assets/5ea5646b-a5a6-4113-880f-4478cdf6ca4e" />

<img width="1944" height="1160" alt="image" src="https://github.com/user-attachments/assets/788b7fd7-695b-4556-8315-ed992370c3c5" />


Here is the final IR Blaster PCB:
<img width="1378" height="420" alt="image" src="https://github.com/user-attachments/assets/60415aa1-cf97-4ff2-ada6-129e91e6e853" />

<img width="1990" height="872" alt="image" src="https://github.com/user-attachments/assets/d4a6bce3-a25b-46a9-9a48-5e71a3b4f939" />
