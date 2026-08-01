# THE DIMAH

An F450 quadcopter built from parts and flown from a phone. ESP32 for the flight controller, MPU-6050 for attitude, WiFi for the link. The control loop is adapted from Joop Brokking's YMFC-AL, ported to the ESP32 and documented from scratch.

## What is here

    THE_DIMAH.pdf     the build guide, 19 pages, meant to be read in order
    images/           wiring, motor layout and power tree schematics
    code/             three Arduino sketches, meant to be run in sequence

The sketches are staged deliberately, because the failure modes get worse as you go:

1. `dimah_01_test_capteurs` reads the MPU-6050 and measures battery voltage. USB only. Nothing spins, nothing can hurt you.
2. `dimah_02_calibration_esc` calibrates the electronic speed controllers and tests the motors. Props off. This is not negotiable.
3. `dimah_03_flight_controller` is the real thing: attitude loop, mixer and the WiFi remote. Needs the WebSockets library by Markus Sattler.

## Flying it

The drone brings up its own WiFi access point. Connect a phone to it and the control page is served at `http://192.168.4.1`. The network name and password are set at the top of the flight controller sketch. Change the password before you fly anywhere near other people.

## Order of operations

Read chapter 2 on safety and chapter 7 on wiring before touching anything. Set the LM2596 regulator to exactly 5.0 V before connecting it to the ESP32, because getting that wrong ends the project on the spot. Then follow the chapters in sequence. Each stage has a verification step, and skipping them is how you discover a wiring mistake at full throttle.

## Status

Built and documented. Bench tests pass. It has not flown yet.

## Credit

The control loop structure comes from Joop Brokking's YMFC-AL series, which is the clearest explanation of a hand written flight controller I have found. The ESP32 port, the WiFi remote, the power design and the documentation are mine.
