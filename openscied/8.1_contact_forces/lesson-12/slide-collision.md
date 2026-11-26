# Lesson 12 - Slider Force Sensor System

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Each button saves where the slider is now and starts a new peak.
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
// Collisions that move the slider more than this much (%) count as large.
largeCollision = 50
startslide = opensciedModules.slider1.position()
status = "home"
// Reads the slider as fast as it can and keeps the biggest movement
// since the last button press. It has its own loop so a split-second
// collision is not missed while the screens are busy.
basic.forever(function () {
    inputslide = Math.round(Math.abs(opensciedModules.slider1.position() - startslide))
    if (inputslide > peakslide) {
        peakslide = inputslide
    }
})
// Shows the movement and the peak on the LCD, and the result on the micro:bit.
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

## Lesson 12 - Slider Force Sensor System

This project has the code for the **Slider Force Sensor System**. It is the sample program (answer key) for the **Slider Force Sensor** create tutorial.

## How to use the code

- Press **A** for setup mode. Watch the LCD: line 1 shows how far the slider has moved (%) since you pressed **A**, and line 2 shows the peak (biggest movement).
- Press **B** for test mode. The micro:bit shows a big square if the peak is more than 50%, and a small square if not.
- Press **A+B** together to wait. A dot shows.

Each time you press **A** or **B**, the slider's position is saved as the new start and a new peak starts.

## Technical notes

The code uses two loops that run at the same time:

- The first ``||basic:forever||`` loop reads the slider as fast as it can and keeps the biggest movement in ``peakslide``. It counts movement in either direction.
- The second ``||basic:forever||`` loop shows the readings on the LCD and the result on the micro:bit.

Printing to the LCD takes time. Keeping the reading in its own loop means a quick collision is not missed. To tune the system, change ``largeCollision`` (50%).

Click **Done**, then download the code to your micro:bit.
