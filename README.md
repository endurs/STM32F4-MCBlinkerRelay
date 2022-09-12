# STM32F4-MCBlinkerRelay

Small personal project to replace the (broken) blinker relay on my Honda XL500s motorcycle without changing anything other than the relay unit.

Planned solution/features:
- STM32F411 blackpill for controlling everything
- Mechanical relay with satisfying click for blinking the blinkers
- Optoisolatoion for powering the relay
- Current sensing OPamp for measuring when the blinkers are turned on.
- Custom PCB and 3d printed housing to keep everything pretty compact and protected from the elements.

Some notes:
Very overkill solution for such a simple problem as this. Large part of the goal is to get some experience with different types of circuitry, and also allow for some sort of future expansion. 
Some ideas for future expansion are: enigne RPM sensing, display for engine RPM, temp/baro/humidity sensor for weather display, LTE + gps for tracking bike location on phone.

13/09/2022
