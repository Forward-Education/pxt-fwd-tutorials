# Lesson 3 - Sensor Station A (Temperature)

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
columnname = "Temperature (F)"
datalogger.mirrorToSerial(true)
basic.showLeds(`
    # . # # #
    . . # . .
    . . # # #
    . . # . .
    . . # . .
    `)
// Reads the sensor and scrolls the value on the screen.
// Scrolling text takes a few seconds, so it gets its own loop
// to keep it from slowing down the data logging.
basic.forever(function () {
    output = opensciedModules.round(opensciedModules.temperature1.readTemperature(opensciedEnums.TemperatureUnit.Fahrenheit), 1)
    if (scrolldisplay) {
        basic.showString("F:" + output)
    }
})
// Saves one reading every second, so the data is evenly spaced over time.
loops.everyInterval(1000, function () {
    if (logging) {
        datalogger.log(datalogger.createCV(columnname, output))
    }
})
```

## Lesson 3 - Sensor Station A (Temperature)

This project has the code for **Sensor Station A (Temperature)**.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

- Press **A** to start. A check mark shows, the old data log is erased, and the micro:bit starts saving a temperature reading every second. The reading also scrolls on the screen.
- Press **A+B** together to stop. A happy face shows and the micro:bit stops saving readings.

Pressing **A** again erases the saved data, so save your data before you start a new run.

## Technical notes

The code uses two loops that run at the same time:

- The ``||basic:forever||`` loop reads the temperature sensor and scrolls the value on the screen.
- The ``||loops:every 1000 ms||`` loop saves one reading to the data log every second.

Scrolling text on the micro:bit takes a few seconds. If both jobs were in the same loop, the data would only be saved after each scroll finished, and the readings would not be evenly spaced. Keeping them in separate loops means you get one reading every second, no matter what the screen is doing.

Click **Done**, then download the code to your micro:bit.
