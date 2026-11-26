# Lesson 12 - Slider Force Sensor

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

## Lesson 12 - Slider Force Sensor @showdialog

In this tutorial you will program the **slider** to sense a collision and tell you if it was **small** or **large**. A collision pushes the slider, and a bigger collision pushes it further.

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
- How far (%) must the slider move to count as a large collision?

## Find your sensor

Find the ``||opensciedModules:slider1 %||`` block. It gives the slider's position from 0 to 100%.

A collision **moves** the slider, so you need how far it moved since you pressed a button. Make a variable called ``startslide`` to save where the slider started. The movement is the reading take away the start. The ``||math:absolute of||`` block turns a negative number positive, so a push either way counts.

```blocks
let inputslide = 0
let startslide = 0
inputslide = Math.round(Math.abs(opensciedModules.slider1.position() - startslide))
```

## Show the reading in setup mode

1. In the **A** and **B** button blocks, set ``startslide`` to ``||opensciedModules:slider1 %||``.
2. Make a variable called ``inputslide``. At the top of the ``||basic:forever||`` loop, set it to the movement.
3. In the **setup** part of the ``||logic:if||`` block, print it on the LCD.

```blocks
let inputslide = 0
let startslide = 0
let status = ""
basic.forever(function () {
    // @highlight
    inputslide = Math.round(Math.abs(opensciedModules.slider1.position() - startslide))
    if (status == "setup") {
        // @highlight
        opensciedModules.lcd1.printQuadrantString("Move %", 1)
        // @highlight
        opensciedModules.lcd1.printQuadrantNumber(inputslide, 2)
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

Download and press **A**. Flick the slider quickly. Does the LCD always catch how far it moved?

## Why the collision gets missed

Printing to the LCD takes time, but a collision lasts only a split second. While the loop is busy printing, it is not reading the sensor, so the biggest moment of a collision can be missed.

The fix is a **second loop** that does nothing but read the sensor and keep the **biggest** reading, called the **peak**.

## Add a loop that keeps the peak

1. Make a variable called ``peakslide``.
2. Drag the ``inputslide`` block out of the first loop and into a new ``||basic:forever||`` loop.
3. In the new loop, if the reading is bigger than the peak, save it as the new peak.
4. In setup mode, also print ``peakslide`` on line 2 of the LCD (quadrants 3 and 4).

```blocks
let inputslide = 0
let startslide = 0
let peakslide = 0
// @highlight
basic.forever(function () {
    inputslide = Math.round(Math.abs(opensciedModules.slider1.position() - startslide))
    if (inputslide > peakslide) {
        peakslide = inputslide
    }
})
```

## Start a new peak each launch

Each time you press **A** or **B**, the movement and the peak should start over.

Set ``startslide`` to the slider position and ``peakslide`` to 0 in the **A** and **B** button blocks.

```blocks
let startslide = 0
let peakslide = 0
let status = ""
input.onButtonPressed(Button.A, function () {
    // @highlight
    startslide = opensciedModules.slider1.position()
    // @highlight
    peakslide = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    // @highlight
    startslide = opensciedModules.slider1.position()
    // @highlight
    peakslide = 0
    status = "test"
})
```

## Show small or large in test mode

1. Make a variable called ``largeCollision`` and set it to **50** in ``||basic:on start||``.
2. In the **test** part of the display loop, show a big square if ``peakslide`` is more than ``largeCollision``, and a small square if not.

```blocks
let peakslide = 0
let largeCollision = 0
let status = ""
largeCollision = 50
basic.forever(function () {
    if (status == "setup") {

    } else if (status == "test") {
        // @highlight
        if (peakslide > largeCollision) {
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

Download your code to the micro:bit and attach the slider to your system.

1. Press **A**, then make a collision that measures **5 N** on the force scale. Write down the peak.
2. Change ``largeCollision`` so a 5 N collision is just under it.
3. Press **B** and test. A 5 N collision should show a small square, and a harder one a big square.

Open the hint to compare your code with the sample program. It prints the movement and the peak on the LCD in every mode.

```blocks
input.onButtonPressed(Button.A, function () {
    startslide = opensciedModules.slider1.position()
    peakslide = 0
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    startslide = opensciedModules.slider1.position()
    peakslide = 0
    status = "test"
})
input.onButtonPressed(Button.AB, function () {
    status = "home"
})
let inputslide = 0
let startslide = 0
let peakslide = 0
let largeCollision = 0
let status = ""
opensciedModules.initializeLcd()
largeCollision = 50
startslide = opensciedModules.slider1.position()
status = "home"
basic.forever(function () {
    inputslide = Math.round(Math.abs(opensciedModules.slider1.position() - startslide))
    if (inputslide > peakslide) {
        peakslide = inputslide
    }
})
basic.forever(function () {
    opensciedModules.lcd1.printQuadrantString("Move %", 1)
    opensciedModules.lcd1.printQuadrantNumber(inputslide, 2)
    opensciedModules.lcd1.printQuadrantString("Peak %", 3)
    opensciedModules.lcd1.printQuadrantNumber(peakslide, 4)
    if (status == "setup") {
        basic.clearScreen()
    } else if (status == "test") {
        if (peakslide > largeCollision) {
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

- The slider gives its position from 0 to 100%. The code subtracts the starting position, so the reading is how far the slider **moved**. The absolute value means a push in either direction counts the same.
- The code uses **two loops**. One loop only reads the slider and saves the biggest movement (the peak). The other loop prints to the LCD and shows the screen. Because the first loop never waits for the LCD, it does not miss the short moment of a collision.
- The peak only goes up. Pressing **A** or **B** saves a new starting position and sets the peak back to 0.
- ``largeCollision`` is a threshold. Every system is built a little differently, so the movement for a 5 N collision is different for each group. That is why you measure first in setup mode and then change the number.

## Run your trials

Run trials with collisions of about **20 N**. Press **B** before each trial and record the result.

- Did your system show the right square each time?
- If not, what would you change: the number, the way the slider is attached, or something else?

Click **Done**, then download the code to your micro:bit.
