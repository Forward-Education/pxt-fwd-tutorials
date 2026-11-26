# Lesson 3 - Sensor Station C (Light)

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    basic.showIcon(IconNames.Yes)
    basic.pause(500)
    datalogger.deleteLog(datalogger.DeleteType.Full)
    datalogger.setColumnTitles(columnname)
    logging = true
    scrolldisplay = true
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    scrolldisplay = false
    logging = false
    basic.showIcon(IconNames.Happy)
})
let output = 0
let columnname = ""
let scrolldisplay = false
let logging = false
logging = false
scrolldisplay = false
columnname = "Light intensity (lux)"
datalogger.mirrorToSerial(true)
basic.showLeds(`
    # . . . #
    # . . . .
    # . . . #
    # . . . #
    # # # . #
    `)
// Reads the sensor and scrolls the value on the screen.
// Scrolling text takes a few seconds, so it gets its own loop
// to keep it from slowing down the data logging.
basic.forever(function () {
    output = opensciedModules.round(opensciedModules.light1.illuminance(), 1)
    if (scrolldisplay) {
        basic.showString("Li:" + output)
        basic.clearScreen()
    }
})
// Saves one reading every second, so the data is evenly spaced over time.
loops.everyInterval(1000, function () {
    if (logging) {
        datalogger.log(datalogger.createCV(columnname, output))
    }
})
```

## Lesson 3 - Sensor Station C (Light)

This project has the code for **Sensor Station C (Light)**.

## How the code works

The code uses two loops that run at the same time:

- The ``||basic:forever||`` loop reads the light sensor and scrolls the value on the screen.
- The ``||loops:every 1000 ms||`` loop saves one reading to the data log every second.

Scrolling text on the micro:bit takes a few seconds. If both jobs were in the same loop, the data would only be saved after each scroll finished, and the readings would not be evenly spaced. Keeping them in separate loops means you get one reading every second, no matter what the screen is doing.

Click **Done**, then download the code to your micro:bit.
