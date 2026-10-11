# Bluetooth-Controlled and Obstacle-Avoiding Car

An embedded car project built around an STM32F103C8. The Arduino-style firmware supports Bluetooth manual control and a basic autonomous mode that reads an ultrasonic sensor and chooses a turn when an obstacle is nearby.

## Hardware indicated by the firmware

- STM32F103C8 development board
- Bluetooth serial module connected through `Serial1` at 9600 baud
- Ultrasonic distance sensor
- Servo used to point the sensor left, forward, and right
- Two DC motor control channels
- Indicator/stop LEDs and a buzzer

Pin assignments are declared near the top of `sketch_may9b/sketch_may9b.ino`; confirm them against the actual wiring before powering the circuit. The repository also includes a Proteus project and circuit image.

## Firmware behavior

- Manual mode responds to serial commands for forward, reverse, left, right, stop, speed changes, a turn, and buzzer.
- Autonomous mode checks forward distance; when an obstacle is close, it scans left and right and chooses a direction with more clearance.
- The logic is a simple obstacle-avoidance routine, not a general maze-solving or path-planning algorithm.

## Build and upload

The source is an Arduino sketch targeting an STM32F103 generic STM32F1 board. Open `sketch_may9b/sketch_may9b.ino` in an Arduino-compatible IDE, install/select a compatible STM32 board core, confirm the pin mapping and serial setup, then compile and upload using the appropriate board and port settings.

The checked-in `build/` outputs are generated artifacts and may not match your toolchain. Rebuild the sketch rather than relying on the checked-in `.bin` or `.elf`.

## Safety

Test with the wheels raised and a current-limited power supply where possible. Verify motor-driver wiring, voltage levels, servo range, and sensor connections before autonomous operation. The source uses blocking delays and has not been validated as a safety-critical controller.
