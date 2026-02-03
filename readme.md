Zebra WT6000 USB / Dock Connector Pinout and Charging Behavior

This repository documents the USB, docking, and charging pinout behavior of the Zebra WT6000 wearable computer, based on hands-on reverse engineering and empirical testing.

The primary objective of this work was to:

    * Understand how the WT6000 detects docks and accessories
	 
    * Enable USB data access without the official dock
	
    * Build a single custom cable that supports both USB data and charging

Zebra’s official documentation is incomplete for this connector, and official accessories are costly. This README aims to provide clear, accurate technical information for repair, development, and reuse.
Overview

Key findings:

    The WT6000 uses separate pins for USB VBUS and charging power
    Charging functions in all modes
    USB data requires dock mode
    Dock mode is selected by grounding a single pin
    No resistor is required for USB or dock operation
    Charger and USB power inputs can be safely bridged

Connector Orientation

    Device screen facing upward
    Pin numbering follows Zebra’s internal numbering scheme
    The same connector and pinout are used by:

        WT6000 device-side port

        RS5000 / RS4000 scanner cables

Refer to images in this repository for exact pin numbering and orientation.
Pinout Summary
Pin	Function
1	Ground
2	Dock Mode Detect
3	Not connected
4	Not connected
5	USB VBUS (+5 V)
6	USB ID (unused for WT6000 USB)
7	Charger +5 V
8	Charger +5 V
9	Not connected
10	USB D+
11	USB D−
12	Ground
Dock Mode Detection (Pin 2)

Pin 2 determines how the WT6000 interprets the connected accessory.
Pin 2 Connection	WT6000 Behavior
Direct to Ground	Dock / USB mode
Resistor to GND	Scanner accessory identified
Floating	No accessory
Important Notes

    * USB and dock cables use a direct connection to ground

    * No resistor is used or required for USB

    * Resistor coding is used only for scanner accessories (e.g., RS4000, RS5000)

Charging Behavior
Charger Pins (Pins 7 and 8)

    * Accept +5 V at all times

    * Function regardless of dock or accessory mode

    * Charging does not depend on USB enumeration

These pins are the most reliable method for powering or charging the WT6000.
USB VBUS (Pin 5)

    * Required for USB data enumeration

    * Indicates the presence of a USB host

    * May not reliably charge the device when used alone

USB Data Lines

    USB D+ and D− operate as standard USB 2.0 signals

    Data becomes active when:

        USB VBUS is present, and

        The device is in dock mode (Pin 2 grounded)

Combined USB + Charging Cable

A single cable supporting USB data and charging can be constructed as follows:

    Bridge the following pins together:

        Pin 5 (USB VBUS +5 V)

        Pin 7 (Charger +5 V)

        Pin 8 (Charger +5 V)

    Supply a regulated +5 V source

    Connect USB D+ and D− normally

    Ground Pin 2 to enable dock mode

Electrical Safety

    All +5 V pins are input-only

    The WT6000 does not backfeed power

    Bridging USB VBUS and charger pins is safe and confirmed by testing

Physical Connector Notes

    Zebra’s factory cable uses a heavily overmolded connector filled with adhesive

    The overmold can be carefully removed and reused

    The original connector shell provides proper retention and strain relief

    Rebuilding a custom cable inside the original shell is feasible

Motivation

This documentation exists to support:

    Hardware repair

    Development access (ADB, recovery)

    Custom accessories

    Long-term reuse of otherwise locked-down enterprise hardware

It is intended to complement—not replace—official documentation where available.
Disclaimer

This information is provided for educational and experimental purposes.

    Incorrect wiring can permanently damage the device

    Use a current-limited, regulated 5 V power source

    Verify pin orientation before applying power

    Results are based on tested WT6000 hardware and may not apply universally
