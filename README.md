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

Example 1: MAX7219 Display Demo.
/*
  Arduino Shield V2.0
  Example 1 - MAX7219 Display Demo

  DIN  -> D11
  CLK  -> D13
  CS   -> D10
*/

#include <LedControl.h>

#define DIN_PIN 11
#define CLK_PIN 13
#define CS_PIN 10

LedControl lc = LedControl(DIN_PIN, CLK_PIN, CS_PIN, 1);

void setup()
{
  lc.shutdown(0, false);     // Wake display
  lc.setIntensity(0, 8);     // Brightness (0-15)
  lc.clearDisplay(0);
}

void loop()
{
  // Count from 0000 to 9999
  for (int i = 0; i <= 9999; i++)
  {
    displayNumber(i);
    delay(5);
  }

  delay(1000);

  // Display HELLO
  lc.clearDisplay(0);

  lc.setChar(0, 4, 'H', false);
  lc.setChar(0, 3, 'E', false);
  lc.setChar(0, 2, 'L', false);
  lc.setChar(0, 1, 'L', false);
  lc.setChar(0, 0, 'O', false);

  delay(3000);

  lc.clearDisplay(0);

  // Countdown
  for (int i = 9; i >= 0; i--)
  {
    lc.clearDisplay(0);
    lc.setDigit(0, 0, i, false);
    delay(500);
  }

  lc.clearDisplay(0);
}

void displayNumber(int number)
{
  lc.setDigit(0, 0, number % 10, false);
  lc.setDigit(0, 1, (number / 10) % 10, false);
  lc.setDigit(0, 2, (number / 100) % 10, false);
  lc.setDigit(0, 3, (number / 1000) % 10, false);
}


Example 2 – Button Test (D7, D6, D5, D4)
This example verifies that all four push buttons on your shield are working.

/*
  Arduino Shield V2.0
  Example 2 - Button Test

  Button 1 -> D7
  Button 2 -> D6
  Button 3 -> D5
  Button 4 -> D4
*/

#define BTN1 7
#define BTN2 6
#define BTN3 5
#define BTN4 4

void setup()
{
  Serial.begin(9600);

  pinMode(BTN1, INPUT_PULLUP);
  pinMode(BTN2, INPUT_PULLUP);
  pinMode(BTN3, INPUT_PULLUP);
  pinMode(BTN4, INPUT_PULLUP);

  Serial.println("=== Arduino Shield Button Test ===");
  Serial.println("Press any button...");
}

void loop()
{
  if (digitalRead(BTN1) == LOW)
  {
    Serial.println("Button 1 Pressed");
    delay(200);
  }

  if (digitalRead(BTN2) == LOW)
  {
    Serial.println("Button 2 Pressed");
    delay(200);
  }

  if (digitalRead(BTN3) == LOW)
  {
    Serial.println("Button 3 Pressed");
    delay(200);
  }

  if (digitalRead(BTN4) == LOW)
  {
    Serial.println("Button 4 Pressed");
    delay(200);
  }
}

Example 2 – reaction time game 
uses: 
 - 4 digit 7 segment display
 - buzzer
 - button 1 (D7)

 #include <LedControl.h>

#define DIN 11
#define CLK 13
#define CS 10

#define BUZZER 9
#define BUTTON 7

LedControl lc = LedControl(DIN, CLK, CS, 1);

unsigned long startTime;
unsigned long reaction;

void setup()
{
  pinMode(BUTTON, INPUT_PULLUP);
  pinMode(BUZZER, OUTPUT);

  lc.shutdown(0, false);
  lc.setIntensity(0, 8);
  lc.clearDisplay(0);

  randomSeed(analogRead(A0));
}

void loop()
{
  // Ready
  showText("GO");

  delay(2000);

  lc.clearDisplay(0);

  // Random wait
  delay(random(2000, 5000));

  // Beep
  tone(BUZZER, 1000, 150);

  // Show 0000
  displayNumber(0);

  startTime = millis();

  while (digitalRead(BUTTON) == HIGH);

  reaction = millis() - startTime;

  displayNumber(reaction);

  delay(5000);
}

void displayNumber(int num)
{
  lc.setDigit(0, 0, num % 10, false);
  lc.setDigit(0, 1, (num / 10) % 10, false);
  lc.setDigit(0, 2, (num / 100) % 10, false);
  lc.setDigit(0, 3, (num / 1000) % 10, false);
}

void showText(String txt)
{
  lc.clearDisplay(0);

  if (txt == "GO")
  {
    lc.setChar(0, 1, 'G', false);
    lc.setChar(0, 0, 'O', false);
  }
}


Example 4 - countdown timer 
uses: 
- display
- button 1
- buzzer

  
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
3. Upload the example sketch again./*
  Arduino Shield V2.0
  Example 4 - Countdown Timer

  Button 1 -> Start Countdown
*/

#include <LedControl.h>

#define DIN     11
#define CLK     13
#define CS      10

#define BUTTON  7
#define BUZZER  9

LedControl lc = LedControl(DIN, CLK, CS, 1);

void setup()
{
  pinMode(BUTTON, INPUT_PULLUP);
  pinMode(BUZZER, OUTPUT);

  lc.shutdown(0, false);
  lc.setIntensity(0, 8);
  lc.clearDisplay(0);

  displayNumber(10);   // Initial countdown value
}

void loop()
{
  if (digitalRead(BUTTON) == LOW)
  {
    countdown(10);

    delay(1000);
  }
}

void countdown(int seconds)
{
  for (int i = seconds; i >= 0; i--)
  {
    displayNumber(i);
    delay(1000);
  }

  // Alarm
  for (int i = 0; i < 3; i++)
  {
    tone(BUZZER, 1000);
    delay(200);

    noTone(BUZZER);
    delay(200);
  }

  displayNumber(10);
}

void displayNumber(int num)
{
  lc.setDigit(0, 0, num % 10, false);
  lc.setDigit(0, 1, (num / 10) % 10, false);
  lc.setDigit(0, 2, (num / 100) % 10, false);
  lc.setDigit(0, 3, (num / 1000) % 10, false);
}



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
