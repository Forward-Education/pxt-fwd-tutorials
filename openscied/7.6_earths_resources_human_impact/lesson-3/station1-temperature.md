# Lesson 3 - Station 1 Temperature Sensor

```package
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Shows the temperature as a bar graph and starts saving readings.
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
})
// Shows the station number, stops saving readings and erases the log.
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
    basic.showNumber(station_number)
    datalogger.deleteLog()
})
// Shows the temperature as a number and starts saving readings.
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
})
let inputcurrent = 0
let outputchoice = ""
let station_number = 0
station_number = 1
outputchoice = "station"
datalogger.setColumnTitles("temperature")
basic.showNumber(station_number)
// Reads the sensor and shows the reading the way A or B chose.
// Scrolling a number takes a few seconds, so the display gets its own loop
// to keep it from slowing down the data logging.
basic.forever(function () {
    inputcurrent = opensciedModules.round(opensciedModules.bmeTemperature.readTemperature(), 1)
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    } else if (outputchoice == "B") {
        basic.showNumber(inputcurrent)
    }
})
// Saves one reading every second while A or B is on.
loops.everyInterval(1000, function () {
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("temperature", inputcurrent)
        datalogger.log(datalogger.createCV("temperature", inputcurrent))
    }
})
```

## Lesson 3 - Station 1 Temperature Sensor

This project has the code for **Station 1 (Temperature)**. Set it up before class.

- Press **A** to show the temperature (°C) as a bar graph.
- Press **B** to show the temperature as a number, rounded to 1 decimal place.
- Press **A+B** to show the station number, stop saving readings and erase the data log.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Setup

Connect the BME280 sensor to the breakout board.

## What A and B show

Find the ``||basic:forever||`` loop. The ``||logic:if||`` block checks ``outputchoice`` to choose what to show.

```blocks
let inputcurrent = 0
let outputchoice = ""
basic.forever(function () {
    inputcurrent = opensciedModules.round(opensciedModules.bmeTemperature.readTemperature(), 1)
    // @highlight
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    } else if (outputchoice == "B") {
        basic.showNumber(inputcurrent)
    }
})
```

The bar graph is full at 35 °C.

## Saving the data

Find the ``||loops:every 1000 ms||`` block.

```blocks
let inputcurrent = 0
let outputchoice = ""
// @highlight
loops.everyInterval(1000, function () {
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("temperature", inputcurrent)
        datalogger.log(datalogger.createCV("temperature", inputcurrent))
    }
})
```

While **A** or **B** is on, the micro:bit saves one reading every second. Switching between **A** and **B** keeps the data. Only **A+B** erases it, so save your data first.

## Check

Download the code. The micro:bit shows **1**. Press **A** and a bar graph shows.

## Technical notes

The ``||basic:forever||`` loop handles the display and the ``||loops:every 1000 ms||`` loop handles the data log. Scrolling a number takes a few seconds, so keeping the two jobs apart means the readings stay one second apart.

Click **Done**, then download the code to your micro:bit.
