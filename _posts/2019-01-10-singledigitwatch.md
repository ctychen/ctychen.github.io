---
layout: post
title:  "Single digit Numitron watch"
date:   2019-01-10
excerpt: "The sketchiest timepiece ever"
project: true
tag:
- electronics
- code
- arduino
- wearable
comments: false
---

Numitron tubes are really just fancy 7-segment displays. Unlike Nixie tubes, which they are often confused for, these
only need 1 power supply and can run on low voltages. The 7 segment display is formed with low-power incandescent filaments.

After seeing [this](http://blog.thelifeofkenneth.com/2009/11/seven-segment-led-arduino-clock.html) 7-segment Arduino clock 
I wanted to see if I could make something similar using my IV-9 numitrons. I wanted it to be a watch for the extra challenge of 
trying to make something as small as possible with that (and because it looks super cool). 

What it looks like so far is here: 

![oof](https://lh3.googleusercontent.com/-tNUEH9lO8PY/XDpZKDj_PfI/AAAAAAABkv0/ZzsYkBKl0nAczV8Xll184mFmmlNAWhQXwCK8BGAs/s512/8873761104810410855%253Faccount_id%253D0)

## Parts List ##

* Arduino Nano 
* RTC (Real Time Clock) module. Mine has the DS1307 chip. Note that this needs a coin cell battery.
* Numitron tube: I'm using the IV9. Any similar one works, just make sure you check the wiring for the segments. 
* LiPo battery


## Wiring ##

Segments on the numitron are as follows:


![Segments](https://lh3.googleusercontent.com/-kBJcPBazEDs/XDpsgCT3BEI/AAAAAAABkxM/PIVFX81CACoVkE7TCDq4oWYzA1uBy31TgCK8BGAs/s512/3573453374630806147%253Faccount_id%253D0)


* Arduino Nano pin D9 to numitron segment g
* Arduino Nano pin D8 to numitron segment f
* Arduino Nano pin D7 to numitron segment e
* Arduino Nano pin D6 to numitron segment d
* Arduino Nano pin D5 to numitron segment c
* Arduino Nano pin D4 to numitron segment dot
* Arduino Nano pin D3 to numitron segment a
* Arduino Nano pin D2 to numitron segment b

* Arduino Nano pin A4 to DS1307/RTC SDA
* Arduino Nano pin A5 to DS1307/RTC SCL
* Arduino 5V to DS1307/RTC 5V
* Arduino GND to DS1307/RTC GND

## Code ##

Inspired by stuff on lifeonkenneth

```cpp
#include <Wire.h>

// I2C address
#define DS1307 B1101000

// pinout for the 7 segment display
// Starts top center, clock-wise, then
// center line, then dot
byte segment[] = {
  3, 2, 5, 6, 7, 8, 9, 4};

byte second=0, minute=27, hour=17;

void updatetime();
void printtime();
void print7digit(byte number);
byte DECTOBCD(byte val);
byte BCDTODEC(byte val);

void setup() {
  byte i;
  Wire.begin();

  for (i=0; i<8; i++) {
    pinMode(segment[i], OUTPUT);
    digitalWrite(segment[i], LOW);
  }
}

void loop() {
  updatetime();
  printtime();
}

// Pull current time off the DS1307
void updatetime() {
  Wire.beginTransmission(DS1307);
  Wire.write(0x00);
  Wire.endTransmission();
  Wire.requestFrom(DS1307, 3);
  // Don't actually use seconds value. Feel free to.
  second = BCDTODEC(Wire.read() & 0x7f);
  minute = BCDTODEC(Wire.read());
  hour   = BCDTODEC(Wire.read() & 0x3f); 
}

// Flash each digit of the time in turn on the 7 segment
void printtime() {
  byte j;
  // Convert from 24 hour to 12 hour mode
  // Should be done on the DS1307. I'm sorry.
  byte temphour = hour % 12;
  if (temphour == 0) {
    // Not zero based, not one based, but 12 based.
    temphour = 12;
  }
  
  // Only display highest digit if it's nonzero
  if (temphour > 9) {
    print7digit(temphour/10);
    delay(500); // Repeated magic values in my code? Never!
    for (j=0; j<8; j++) {
      digitalWrite(segment[j], LOW);
    }
    delay(150);
  }
  print7digit(temphour % 10);
  // Light the dot on last hour digit
  digitalWrite(segment[7], HIGH);
  delay(500);
  for (j=0; j<8; j++) {
    digitalWrite(segment[j], LOW);
  }
  delay(500);
  
  print7digit(minute/10);
  delay(500);
  for (j=0; j<8; j++) {
    digitalWrite(segment[j], LOW);
  }
  delay(150);
  print7digit(minute%10);
  delay(500);
  for (j=0; j<8; j++) {
    digitalWrite(segment[j], LOW);
  }
  delay(2000);
}

// Display a single digit on the 7 segment
void print7digit(byte number) {
  // Bitfield for digits 0-9
  const byte numtable[] = {
    B00111111,
    B00000110,
    B01011011,
    B01001111,
    B01100110,
    B01101101,
    B01111101,
    B00000111,
    B01111111,
    B01100111  };
  byte litpins = numtable[number];
  byte i;
  for (i=0; i<8; i++) {
    digitalWrite(segment[i], (litpins>>i) & 1);
  } 
} 

byte DECTOBCD(byte val) {
  return ((val/10)<<4) + (val%10);
}
byte BCDTODEC(byte val) {
  return (val>>4) * 10 + (val & 0xf);
}

```
