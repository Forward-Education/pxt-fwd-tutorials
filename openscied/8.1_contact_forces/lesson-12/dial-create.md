# Lesson 12 - Rotary Dial Force Sensor

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
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
opensciedModules.initializeLcd()
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

## Lesson 12 - Rotary Dial Force Sensor

In this tutorial you will program the **rotary dial** to sense a collision and tell you if it was **small** or **large**. A collision turns the dial, and a bigger collision turns it more.

The system has two modes:

- **Setup mode** (button **A**): shows the sensor reading on the LCD, so you can see what numbers a collision makes.
- **Test mode** (button **B**): shows a **small square** for a small collision or a **big square** for a large one.

The buttons already switch modes. **A+B** shows a dot while the system waits.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Plan your program

Before you code, draw a flowchart with your group.

- What should the LCD show in setup mode?
- How will the micro:bit decide between a small and a large collision?
- What number of clicks will you compare the reading to?

## Find your sensor

Find the ``||opensciedModules:dial1 position||`` block. It counts the clicks the dial has turned: clockwise adds 1 and counterclockwise takes away 1. The ``||math:absolute of||`` block turns a negative number positive, so a turn either way counts.

```blocks
let inputposition = 0
inputposition = Math.abs(opensciedModules.dial1.position())
```

## Show the reading in setup mode

Make a variable called ``inputposition``. At the top of the ``||basic:forever||`` loop, set it to the clicks. In the **setup** part of the ``||logic:if||`` block, print it on the LCD.

```blocks
let inputposition = 0
let status = ""
basic.forever(function () {
    // @highlight
    inputposition = Math.abs(opensciedModules.dial1.position())
    if (status == "setup") {
        // @highlight
        opensciedModules.lcd1.printQuadrantString("Clicks", 1)
        // @highlight
        opensciedModules.lcd1.printQuadrantNumber(inputposition, 2)
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

Download and press **A**. Flick the dial quickly. Does the LCD always catch how far it turned?

## Why the collision gets missed

Printing to the LCD takes time, but a collision lasts only a split second. While the loop is busy printing, it is not reading the sensor, so the biggest moment of a collision can be missed.

The fix is a **second loop** that does nothing but read the sensor and keep the **biggest** reading, called the **peak**.

## Add a loop that keeps the peak

1. Make a variable called ``peakposition``.
2. Drag the ``inputposition`` block out of the first loop and into a new ``||basic:forever||`` loop.
3. In the new loop, if the reading is bigger than the peak, save it as the new peak.
4. In setup mode, also print ``peakposition`` on line 2 of the LCD (quadrants 3 and 4).

```blocks
let inputposition = 0
let peakposition = 0
// @highlight
basic.forever(function () {
    inputposition = Math.abs(opensciedModules.dial1.position())
    if (inputposition > peakposition) {
        peakposition = inputposition
    }
})
```

## Start a new peak each launch

Each time you press **A** or **B**, the dial should go back to 0 clicks and the peak should start over.

Add ``||opensciedModules:reset dial1 position||`` and set ``peakposition`` to 0 in the **A** and **B** button blocks.

```blocks
let peakposition = 0
let status = ""
input.onButtonPressed(Button.A, function () {
    // @highlight
    opensciedModules.dial1.resetPosition()
    // @highlight
    peakposition = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    // @highlight
    opensciedModules.dial1.resetPosition()
    // @highlight
    peakposition = 0
    status = "test"
})
```

## Show small or large in test mode

1. Make a variable called ``largeCollision`` and set it to **3** in ``||basic:on start||``.
2. In the **test** part of the display loop, show a big square if ``peakposition`` is more than ``largeCollision``, and a small square if not.

```blocks
let peakposition = 0
let largeCollision = 0
let status = ""
largeCollision = 3
basic.forever(function () {
    if (status == "setup") {

    } else if (status == "test") {
        // @highlight
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

## Download and tune

Download your code to the micro:bit and attach the dial to your system.

1. Press **A**, then make a collision that measures **5 N** on the force scale. Write down the peak clicks.
2. Change ``largeCollision`` so a 5 N collision is just under it.
3. Press **B** and test. A 5 N collision should show a small square, and a harder one a big square.

Open the hint to compare your code with the sample program. It prints the clicks and the peak on the LCD in every mode.

```blocks
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
largeCollision = 3
status = "home"
basic.forever(function () {
    inputposition = Math.abs(opensciedModules.dial1.position())
    if (inputposition > peakposition) {
        peakposition = inputposition
    }
})
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

## Technical notes

- The dial counts clicks, not force. A harder collision turns it more clicks. The absolute value means a turn in either direction counts the same.
- The code uses **two loops**. One loop only reads the dial and saves the biggest number of clicks (the peak). The other loop prints to the LCD and shows the screen. Because the first loop never waits for the LCD, it does not miss the short moment of a collision.
- The peak only goes up. Pressing **A** or **B** sets the dial back to 0 clicks and the peak back to 0.
- ``largeCollision`` is a threshold. Every system is built a little differently, so the number of clicks for a 5 N collision is different for each group. That is why you measure first in setup mode and then change the number.

## Run your trials

Run trials with collisions of about **20 N**. Press **B** before each trial and record the result.

- Did your system show the right square each time?
- If not, what would you change: the number, the way the dial is attached, or something else?

Click **Done**, then download the code to your micro:bit.
