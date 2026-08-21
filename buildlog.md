2026-07-17
recieved all parts, configured esp32 board to Arduino IDE, installed required libraries to run project (LovyanGFX and ArduinoJson) 
tested basic blink to ensure that esp32 board hardware functions, board selection,driver,upload path all correct
toolchain verified, esp32 uploading correctly

ran some troubleshooting after esp32 board did not blink as expected, turned out to be a computer port issue

<img width="2880" height="2160" alt="fdc1" src="https://github.com/user-attachments/assets/a8e6bf96-4eca-4da6-a204-821fc9863438" />

2026-07-19
tested a singular basic display
created display test to run, pin mapping with esp32 board and displa completed
fixed an issue where sketch would not compile, turns out to be wrong board type selected in arduino ide app

<img width="2880" height="2160" alt="fdc2" src="https://github.com/user-attachments/assets/2face9a2-5fd5-44e8-b316-d9baa96b1b80" />


2026-07-22
# Milestone 1: Three Display SPI Bring-up

## Objective

Verify that the ESP32-S3 can independently control three GC9A01 TFT displays using a shared SPI bus.

## Hardware

- ESP32-S3 N16R8
- 3x GC9A01 1.1" TFT displays
- Dupont jumper wires
- Silicone wires
- Lever connectors

## SPI Architecture

Shared:
- SCL → GPIO12
- SDA → GPIO11
- 3.3V → all displays
- GND → all displays

Independent:
- Display 1:
  - CS GPIO10
  - DC GPIO5
  - RST GPIO4

- Display 2:
  - CS GPIO9
  - DC GPIO6
  - RST GPIO7

- Display 3:
  - CS GPIO8
  - DC GPIO13
  - RST GPIO14

## Test

Display 1:
- Red background
- "ONE"

Display 2:
- Green background
- "TWO"

Display 3:
- Blue background
- "THREE"

## Result

PASS

All three displays initialized and displayed independent graphics.

## Problems Encountered

- Display 3 was temporarily connected with VCC/GND reversed.
- Resolved by correcting wiring before continuing testing.

## Lessons Learned

- SPI allows multiple devices to share clock and data lines.
- Each device requires its own chip select line.
- Labeling power connections prevents wiring mistakes.

<img width="2880" height="2160" alt="IMG_4620" src="https://github.com/user-attachments/assets/1f2607db-7ab3-42a0-83b9-dadbb0a201e2" />

2026-07-26
# Milestone 2 : Button Test
Hardware:
- 4-pin tactile push button
- GPIO15
- GND

Software:
- INPUT_PULLUP
- Falling-edge press detection
- 50 ms debounce
- millis()-based timing

Test:
- Button released → HIGH
- Button pressed → LOW
- One message per physical press
- Holding button does not repeatedly trigger events

Result:
PASS

# Milestone 3.1: RTC Communication
Software

Libraries:

Wire
RTClib by Adafruit
Test

ESP32 successfully detected RTC.

Initial RTC state:

2000-1-1 02:00:00

This indicated communication worked, but time had not been configured.

# Milestone 3.2: RTC Time Setting

Used:

rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));

RTC successfully updated.

Verified:

Seconds increasing
Correct date/time
Clock continues running

# Milestone 3.3: RTC Power Loss Test
Test
Set RTC time
Remove ESP32 USB power
Wait several minutes
Reconnect

Result:

RTC continued counting.

Observed:

Approximately 30 second offset
Determined to be caused by compile/upload delay when setting time
Result

✅ PASS

DS3231 backup battery operation confirmed.

2026-08-20
# Build Log - August 20, 2026

## Overview

Today focused on integrating the individual hardware components into a single working system. The three TFT displays, DS3231 RTC, and four push buttons were connected to the ESP32-S3 and tested independently before being combined into the main Arduino sketch.

This marks the transition from individual component testing to the first integrated prototype.

---

## 1. Three-TFT Display Integration

### Shared SPI Bus

All three GC9A01 TFT displays share the same SPI bus.

| TFT Pin | ESP32-S3 |
|---|---|
| VCC | 3.3V |
| GND | GND |
| SCL | GPIO12 |
| SDA | GPIO11 |

Each display has independent CS, DC, and RST pins.

### Display 1

| TFT Pin | ESP32-S3 |
|---|---|
| DC | GPIO5 |
| CS | GPIO10 |
| RST | GPIO4 |

### Display 2

| TFT Pin | ESP32-S3 |
|---|---|
| DC | GPIO6 |
| CS | GPIO9 |
| RST | GPIO7 |

### Display 3

| TFT Pin | ESP32-S3 |
|---|---|
| DC | GPIO13 |
| CS | GPIO8 |
| RST | GPIO14 |

### Wiring Strategy

Because the available 15 cm Dupont wires are limited, the wiring was redesigned to minimize unnecessary connectors.

- Dupont wires are used for one-to-one signal connections.
- Lever connectors are used only where a connection needs to branch.
- Shared connections include:
  - 3.3V
  - GND
  - SPI SCL
  - SPI SDA

This reduces wiring clutter and makes the eventual enclosure easier to design.

---

## 2. Push Button Integration

Four 4-pin tactile push buttons were connected to the ESP32-S3.

| Button | GPIO | Function |
|---|---|---|
| Button 1 | GPIO15 | Next |
| Button 2 | GPIO16 | Back |
| Button 3 | GPIO35 | Start/Stop |
| Button 4 | GPIO36 | Reset |

(images fil later)

