# CUSTOM-ARDUINO-UNO-R3-SHILED-V2.0
Arduino UNO Universal Shield V2

User Manual & Developer Guide

Chapter 1 – Introduction

- Purpose of the shield
- Features
- Specifications
- Board overview
- Supported Arduino boards

Chapter 2 – Safety

- Reverse polarity protection
- Voltage limits
- Current limits
- Handling precautions

Chapter 3 – Hardware Layout

- Top view
- Bottom view
- Pin labels
- Connector locations
- Component locations

Chapter 4 – Pin Mapping

Feature| Arduino Pin
MAX7219 DIN| D11
MAX7219 CLK| D13
MAX7219 LOAD| D10
MAX7219 DOUT| D1
Buzzer| D9
SW1| D7
SW2| D6
SW3| D5
SW4| D4

Chapter 5 – Headers

- UART
- I2C
- SPI
- Analog
- Digital
- Power

Explain what every header is used for.

Chapter 6 – Example Programs

Example 1

Blink Buzzer

// code

Explanation:

- pinMode()
- digitalWrite()
- delay()

---

Example 2

Reading Push Buttons

// code

Explanation.

---

Example 3

Displaying Numbers on MAX7219

// code

Explanation of every function.

---

Example 4

Scrolling Text

// code

---

Example 5

Using UART

---

Example 6

Using SPI

---

Example 7

Using I2C

---

Chapter 7 – Libraries Required

- LedControl
- MD_MAX72XX
- SPI
- Wire

Explain why each library is used.

Chapter 8 – Troubleshooting

Troubleshooting Guide

The display does not turn ON

Possible reasons

- Arduino is not powered.
- Shield is not inserted properly.

What to do

1. Make sure the Arduino is powered.
2. Check that the shield is firmly connected.
3. Upload the example sketch again.

---

The display shows incorrect numbers

Possible reasons

- Incorrect program uploaded.
- Display initialization failed.

What to do

1. Restart the Arduino.
2. Upload the example program provided.
3. Ensure the display module is inserted correctly.

---

The buzzer does not make any sound

Possible reasons

- Buzzer disabled in the program.
- Buzzer is damaged.

What to do

1. Run the buzzer example program.
2. Restart the Arduino.
3. If there is still no sound, contact support.

---

Push buttons are not responding

Possible reasons

- Program is not running.
- Button is being pressed too quickly.

What to do

1. Restart the Arduino.
2. Press the button firmly once.
3. Test using the button example sketch.

---

I2C module is not working

What to do

1. Check that the sensor is connected to the I2C header.
2. Verify the sensor wiring.
3. Use an I2C Scanner sketch to detect the device.

---

UART module is not working

What to do

1. Ensure the TX and RX connections are correct.
2. Verify the baud rate in your program.
3. Restart both devices.

---

SPI module is not working

What to do

1. Ensure the module is connected to the SPI header.
2. Verify the program supports the connected module.
3. Restart the Arduino.

---

Arduino does not detect the shield

What to do

1. Remove the shield.
2. Reinsert it carefully.
3. Ensure all header pins are aligned correctly.
  

Board becomes hot

Warning
Disconnect power immediately.

Possible reasons

- Incorrect power supply.
- Short circuit.
- Incorrect wiring.

Do not continue using the board until the issue is identified.

Nothing works

1. Disconnect power.
2. Wait 10 seconds.
3. Reconnect power.
4. Upload the example sketch.
5. Test each feature one by one.

Please check the following:

- ✔ Arduino is powered.
- ✔ Shield is inserted correctly.
- ✔ Correct example sketch is uploaded.
- ✔ All modules are connected properly.
- ✔ USB cable is working.
- ✔ Arduino board is detected by the Arduino IDE.

If the problem still exists, provide:

- Shield version
- Arduino model
- Example program used
- Clear photos of the setup
- Description of the problem

Chapter 9 – PCB Features

- 2-layer PCB
- Reverse polarity protection
- Standard Arduino shield layout
- Stackable headers
- Universal expansion connectors

Chapter 10 – Revision History

V1.0

- Initial board

V2.0

- Added reverse polarity protection
- Added buzzer
- Added push buttons
- Added UART/I2C/SPI headers
- Improved layout

Chapter 11 – Future Expansion

- OLED
- NRF24L01
- GPS
- IMU
- Bluetooth
- Wi-Fi
- Sensors
