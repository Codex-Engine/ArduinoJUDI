# ArduinoJUDI
An Arduino library for building JUDI-compatible firmware

## Requirements
[ArduinoJson](https://github.com/bblanchon/ArduinoJson)

## Installation
ArduinoJUDI is a single header library, so you can just add `judi.hpp` directly to your project.

# Example
This is a minimal arduino sketch that just responds to the JUDI handshake.
```c++
#include "judi.hpp"

JUDI judi("your dev9ce", "$GME42069");

void check_comms(char currentChar) {
    if (judi.update(currentChar)) {
        if (judi["request"] == "device_info") {
            serializeJson(judi.device_info, Serial);
        }
    }
}

void setup() {
    Serial.begin(115200);
}

void loop() {
    if (Serial.available()) {
        check_comms(Serial.read());
    }
}

```
