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
