# Lesson 12 - Accelerometer Force Sensor

```package
radio=radio
```

```template
input.onButtonPressed(Button.A, function () {
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    status = "test"
})
input.onButtonPressed(Button.AB, function () {
    status = "home"
})
let status = ""
status = "home"
// Shows what each mode does on the screen. You will fill in setup and test.
basic.forever(function () {
    if (status == "setup") {

    } else if (status == "test") {

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

## Lesson 12 - Accelerometer Force Sensor @showdialog

In this tutorial you will program the micro:bit's **accelerometer** to sense a collision and tell you if it was **small** or **large**.

The system has two modes:

- **Setup mode** (button **A**): shows the sensor reading, so you can see what numbers a collision makes.
- **Test mode** (button **B**): shows a **small square** for a small collision or a **big square** for a large one.

The buttons already switch modes. **A+B** shows a dot while the system waits.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Plan your program

Before you code, draw a flowchart with your group.

- What should the micro:bit show in setup mode?
- How will it decide between a small and a large collision?
- What number will you compare the reading to?

## Find your sensor

The accelerometer measures acceleration in milli-g (mg). Sitting still, it reads about 1000 mg (1 g).

Find the ``||input:acceleration (mg) strength||`` block in ``||input:Input||``. **Strength** combines all three directions, so it works no matter which way the collision pushes.

```blocks
let inputacceleration = 0
inputacceleration = input.acceleration(Dimension.Strength)
```

## Show the reading in setup mode

Make a variable called ``inputacceleration``. At the top of the ``||basic:forever||`` loop, set it to the acceleration strength. In the **setup** part of the ``||logic:if||`` block, show the number.

```blocks
let inputacceleration = 0
let status = ""
basic.forever(function () {
    // @highlight
    inputacceleration = input.acceleration(Dimension.Strength)
    if (status == "setup") {
        // @highlight
        basic.showNumber(inputacceleration)
    } else if (status == "test") {

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

Download and press **A**. Tap the micro:bit hard while a number scrolls. Did the number change?

## Why the collision gets missed

Scrolling a number takes a few seconds, but a collision lasts only a split second. While the loop is busy scrolling, it is not reading the sensor, so most collisions are missed.

The fix is a **second loop** that does nothing but read the sensor and keep the **biggest** reading, called the **peak**.

## Add a loop that keeps the peak

1. Make a variable called ``peakacceleration``.
2. Drag the ``inputacceleration`` block out of the first loop and into a new ``||basic:forever||`` loop.
3. In the new loop, if the reading is bigger than the peak, save it as the new peak.
4. Change the setup mode to show ``peakacceleration``.

```blocks
let inputacceleration = 0
let peakacceleration = 0
// @highlight
basic.forever(function () {
    inputacceleration = input.acceleration(Dimension.Strength)
    if (inputacceleration > peakacceleration) {
        peakacceleration = inputacceleration
    }
})
```

## Start a new peak each launch

The peak should start over each time you press **A** or **B**. Pressing a button jolts the micro:bit too, so wait half a second first.

Add a ``||basic:pause (ms) 500||`` and set ``peakacceleration`` to 0 in the **A** and **B** button blocks.

```blocks
let peakacceleration = 0
let status = ""
input.onButtonPressed(Button.A, function () {
    // @highlight
    basic.pause(500)
    // @highlight
    peakacceleration = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    // @highlight
    basic.pause(500)
    // @highlight
    peakacceleration = 0
    status = "test"
})
```

## Show small or large in test mode

1. Make a variable called ``largeCollision`` and set it to **1400** in ``||basic:on start||``.
2. In the **test** part of the display loop, show a big square if ``peakacceleration`` is more than ``largeCollision``, and a small square if not.

```blocks
let peakacceleration = 0
let largeCollision = 0
let status = ""
largeCollision = 1400
basic.forever(function () {
    if (status == "setup") {
        basic.showNumber(peakacceleration)
    } else if (status == "test") {
        // @highlight
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

## Download and tune

Download your code to the micro:bit and attach it to your system.

1. Press **A**, then make a collision that measures **5 N** on the force scale. Write down the peak.
2. Change ``largeCollision`` so a 5 N collision is just under it.
3. Press **B** and test. A 5 N collision should show a small square, and a harder one a big square.

Open the hint to compare your code with the sample program.

```blocks
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
largeCollision = 1400
status = "home"
basic.forever(function () {
    inputacceleration = input.acceleration(Dimension.Strength)
    if (inputacceleration > peakacceleration) {
        peakacceleration = inputacceleration
    }
})
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

## Technical notes

- The accelerometer reads about 1000 mg even when the micro:bit sits still, because gravity always pulls on it. A collision adds to that number.
- The code uses **two loops**. One loop only reads the sensor and saves the biggest reading (the peak). The other loop shows the screen. Because the first loop never waits for the screen, it does not miss the short moment of a collision.
- The peak only goes up. It goes back to 0 when you press **A** or **B**, after a half second pause so the button press is not counted.
- ``largeCollision`` is a threshold. Every system is built a little differently, so the number that matches a 5 N collision is different for each group. That is why you measure first in setup mode and then change the number.

## Run your trials

Run trials with collisions of about **20 N**. Press **B** before each trial and record the result.

- Did your system show the right square each time?
- If not, what would you change: the number, the way the sensor is attached, or something else?

Click **Done**, then download the code to your micro:bit.
