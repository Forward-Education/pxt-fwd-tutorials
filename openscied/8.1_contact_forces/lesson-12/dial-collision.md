# Lesson 12 - Rotary Dial Force Sensor System

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Each button sets the dial back to 0 clicks and starts a new peak.
input.onButtonPressed(Button.A, function () {
    opensciedModules.dial1.resetPosition()
    peakposition = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    opensciedModules.dial1.resetPosition()
    peakposition = 0
    status = "test"
})
input.onButtonPressed(Button.AB, function () {
    status = "home"
})
let inputposition = 0
let peakposition = 0
let largeCollision = 0
let status = ""
opensciedModules.initializeLcd()
// Collisions that turn the dial more than this many clicks count as large.
largeCollision = 3
status = "home"
// Reads the dial as fast as it can and keeps the biggest number of clicks.
// It has its own loop so a split-second collision is not missed
// while the screens are busy.
basic.forever(function () {
    inputposition = Math.abs(opensciedModules.dial1.position())
    if (inputposition > peakposition) {
        peakposition = inputposition
    }
})
// Shows the clicks and the peak on the LCD, and the result on the micro:bit.
basic.forever(function () {
    opensciedModules.lcd1.printQuadrantString("Clicks", 1)
    opensciedModules.lcd1.printQuadrantNumber(inputposition, 2)
    opensciedModules.lcd1.printQuadrantString("Peak", 3)
    opensciedModules.lcd1.printQuadrantNumber(peakposition, 4)
    if (status == "setup") {
        basic.clearScreen()
    } else if (status == "test") {
        if (peakposition > largeCollision) {
            basic.showIcon(IconNames.Square)
        } else {
            basic.showIcon(IconNames.SmallSquare)
        }
    } else {
        basic.showLeds(`
            . . . . .
            . . . . .
            . . # . .
            . . . . .
            . . . . .
            `)
    }
})
```

## Lesson 12 - Rotary Dial Force Sensor System

This project has the code for the **Rotary Dial Force Sensor System**. It is the sample program (answer key) for the **Rotary Dial Force Sensor** create tutorial.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

- Press **A** for setup mode. Watch the LCD: line 1 shows the clicks since you pressed **A**, and line 2 shows the peak (most clicks).
- Press **B** for test mode. The micro:bit shows a big square if the peak is more than 3 clicks, and a small square if not.
- Press **A+B** together to wait. A dot shows.

Each time you press **A** or **B**, the dial is set back to 0 clicks and a new peak starts.

## Technical notes

The code uses two loops that run at the same time:

- The first ``||basic:forever||`` loop reads the dial as fast as it can and keeps the most clicks in ``peakposition``. It counts clicks in either direction.
- The second ``||basic:forever||`` loop shows the readings on the LCD and the result on the micro:bit.

Printing to the LCD takes time. Keeping the reading in its own loop means a quick collision is not missed. To tune the system, change ``largeCollision`` (3 clicks).

Click **Done**, then download the code to your micro:bit.
