# Lesson 9 - Flex Station

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
let bend = 0
let station_name = ""
opensciedModules.initializeLcd()
station_name = "F"
basic.showString(station_name)
// Reads the flex sensor once, shows the bend on the LCD and a face on the micro:bit.
// The face uses the same rounded number that is on the LCD.
basic.forever(function () {
    bend = Math.round(opensciedModules.flex1.flex())
    opensciedModules.lcd1.printQuadrantString("Bend %", 1)
    opensciedModules.lcd1.printQuadrantNumber(bend, 2)
    if (bend < 8) {
        basic.showIcon(IconNames.Happy)
    } else if (bend < 15) {
        basic.showIcon(IconNames.Asleep)
    } else {
        basic.showIcon(IconNames.Sad)
    }
})
```

## Lesson 9 - Flex Station

This project has the code for the **Flex Station**.

## How to use the code

No buttons are needed. Bend the flex sensor and watch the LCD and the micro:bit.

- The LCD shows how much the sensor is bent, in %.
- The micro:bit shows a face:
    - under 8%: happy face
    - 8% up to 15%: sleepy face
    - 15% or more: sad face

## Technical notes

The numbers **8** and **15** in the ``||logic:if||`` block set when the face changes. Every flex sensor is a little different, so in Lesson 11 you will change these numbers to match your sensor.

Click **Done**, then download the code to your micro:bit.
