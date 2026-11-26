# Lesson 12 - Accelerometer Force Sensor System

```package
radio=radio
```

```template
// Each button waits half a second before starting, so the jolt of
// pressing the button is not counted as a collision. Then the peak starts over.
input.onButtonPressed(Button.A, function () {
    basic.pause(500)
    peakacceleration = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    basic.pause(500)
    peakacceleration = 0
    status = "test"
})
input.onButtonPressed(Button.AB, function () {
    status = "home"
})
let inputacceleration = 0
let peakacceleration = 0
let largeCollision = 0
let status = ""
// Collisions with a peak above this number (mg) count as large.
largeCollision = 1400
status = "home"
// Reads the accelerometer as fast as it can and keeps the biggest reading.
// It has its own loop so a split-second collision is not missed
// while the screen is busy.
basic.forever(function () {
    inputacceleration = input.acceleration(Dimension.Strength)
    if (inputacceleration > peakacceleration) {
        peakacceleration = inputacceleration
    }
})
// Shows the result on the screen.
basic.forever(function () {
    if (status == "setup") {
        basic.showNumber(peakacceleration)
    } else if (status == "test") {
        if (peakacceleration > largeCollision) {
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

## Lesson 12 - Accelerometer Force Sensor System

This project has the code for the **Accelerometer Force Sensor System**. It is the sample program (answer key) for the **Accelerometer Force Sensor** create tutorial.

## How to use the code

- Press **A** for setup mode. The screen scrolls the biggest reading (mg) since you pressed **A**.
- Press **B** for test mode. The screen shows a big square if the biggest reading since you pressed **B** is over 1400 mg, and a small square if not.
- Press **A+B** together to wait. A dot shows.

Each time you press **A** or **B**, the micro:bit waits half a second, then starts a new peak.

## Technical notes

The code uses two loops that run at the same time:

- The first ``||basic:forever||`` loop reads the accelerometer as fast as it can and keeps the biggest reading in ``peakacceleration``.
- The second ``||basic:forever||`` loop shows the result on the screen.

Scrolling a number takes a few seconds. If both jobs were in the same loop, a collision that lasts a split second could happen while the number scrolls and be missed. To tune the system, change ``largeCollision`` (1400 mg).

Click **Done**, then download the code to your micro:bit.
