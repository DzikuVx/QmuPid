# QmuPid

QmuPid is a PID (or rather PID and FeedForward) Arduino library with some interesting features:

* floating point processing
* positive and negative feedback controller output
* Both `Iterm` and `Dterm` are looptime independent - no need to retune ater changing processing frequency
* Output constraining
* Iterm constraining
* Output threshold

## Installation

1. Download ZIP file (`Clone or download` button)
2. Unzip to `Arduino/libraries` folder
3. `#include "QmuPid.h"` in your sketch

## Example usage

```
#include "QmuPid.h"

#define INPUT_PIN A0
#define OUTPUT_PIN 6

// Initialize with P, I, D and FF gains
QmuPid pidController(15, 3, 0, 0);

void setup()
{
    pinMode(OUTPUT_PIN, OUTPUT);
    pinMode(INPUT_PIN, INPUT);

    pidController.setItermProperties(-20, 20); //Limit Iterm to -20:20
    pidController.setSetpoint(200); //Target setpoint
}

void loop() {

    int output = pidController.compute(analogRead(INPUT_PIN), millis());
    
    analogWrite(OUTPUT_PIN);
    delay(100);
}


```
