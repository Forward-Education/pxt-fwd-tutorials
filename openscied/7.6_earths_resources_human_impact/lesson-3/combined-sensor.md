# Lesson 3 - Combined Sensor Code

```package
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Reads the absolute humidity (g/m3), rounded to 2 decimal places.
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
// Scrolls the temperature.
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
})
// The first press erases the old log and starts a new one.
// The next press stops logging and keeps the data.
input.onButtonPressed(Button.AB, function () {
    if (logging) {
        logging = false
        basic.showIcon(IconNames.Happy)
    } else {
        datalogger.deleteLog()
        datalogger.setColumnTitles(
        "temperature",
        "humidity",
        "soil moisture"
        )
        logging = true
        basic.showIcon(IconNames.Yes)
    }
    outputchoice = "station"
})
// Scrolls the absolute humidity.
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
})
// Scrolls the soil moisture.
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    outputchoice = "C"
    basic.clearScreen()
})
let inputcurrentsoil = 0
let abshumidityrounded = 0
let inputcurrenttemp = 0
let logging = false
let outputchoice = ""
outputchoice = "station"
logging = false
basic.showIcon(IconNames.SmallSquare)
// Reads all three sensors and scrolls the value A, B or the logo chose.
// Scrolling takes a few seconds, so it gets its own loop
// to keep it from slowing down the data logging.
basic.forever(function () {
    inputcurrenttemp = opensciedModules.round(opensciedModules.bmeTemperature.readTemperature(), 1)
    calcAbsHumidity()
    inputcurrentsoil = opensciedModules.round(opensciedModules.moisture1.moistureLevel(), 0)
    if (outputchoice == "A") {
        basic.showNumber(inputcurrenttemp)
    } else if (outputchoice == "B") {
        basic.showNumber(abshumidityrounded)
    } else if (outputchoice == "C") {
        basic.showNumber(inputcurrentsoil)
    }
})
// Saves one row with all three readings every second while logging.
loops.everyInterval(1000, function () {
    if (logging) {
        datalogger.log(
        datalogger.createCV("temperature", inputcurrenttemp),
        datalogger.createCV("humidity", abshumidityrounded),
        datalogger.createCV("soil moisture", inputcurrentsoil)
        )
    }
})
```

## Lesson 3 - Combined Sensor Code

This project has the **Combined Sensor** code, one micro:bit per group, for Day 2. It saves temperature (°C), absolute humidity (g/m3) and soil moisture (%) together, every second. Set it up before class.

This code uses the logo, so it needs a **micro:bit V2**.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Setup

Connect the BME280 sensor and the soil moisture sensor to the breakout board. Push the soil moisture prongs into the soil.

## How to use the code

- Press **A+B** to start a new log. The old data is erased and a check mark shows.
- Press **A+B** again to stop. A happy face shows and the data is kept.
- Press **A** to scroll the temperature, **B** for the absolute humidity, or touch the **logo** for the soil moisture.

## Saving the data

Find the ``||loops:every 1000 ms||`` block.

```blocks
let logging = false
let inputcurrenttemp = 0
let abshumidityrounded = 0
let inputcurrentsoil = 0
// @highlight
loops.everyInterval(1000, function () {
    if (logging) {
        datalogger.log(
        datalogger.createCV("temperature", inputcurrenttemp),
        datalogger.createCV("humidity", abshumidityrounded),
        datalogger.createCV("soil moisture", inputcurrentsoil)
        )
    }
})
```

Each second it saves one row with three columns: temperature, humidity and soil moisture, the same as the sample data sheet.

## Check

Download the code. A small square shows on start. Press **A+B** and a check mark shows.

## Technical notes

The ``||basic:forever||`` loop reads the sensors and scrolls a value, and the ``||loops:every 1000 ms||`` loop saves the data. Scrolling takes a few seconds, so keeping the two jobs apart means the readings stay one second apart.

Click **Done**, then download the code to your micro:bit.
