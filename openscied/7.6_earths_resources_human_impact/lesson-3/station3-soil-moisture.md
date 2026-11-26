# Lesson 3 - Station 3 Soil Moisture Sensor

```package
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Shows the soil moisture as a bar graph and starts saving readings.
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
// Shows a face for the soil moisture and starts saving readings.
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
})
let inputcurrent = 0
let outputchoice = ""
let station_number = 0
station_number = 3
outputchoice = "station"
datalogger.setColumnTitles("soil moisture")
basic.showNumber(station_number)
// Reads the sensor and shows the reading the way A or B chose.
basic.forever(function () {
    inputcurrent = opensciedModules.round(opensciedModules.moisture1.moistureLevel(), 0)
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        100
        )
    } else if (outputchoice == "B") {
        if (inputcurrent > 50) {
            basic.showIcon(IconNames.Happy)
        } else if (inputcurrent > 20) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . # # # .
                . . . . .
                `)
        } else {
            basic.showIcon(IconNames.Sad)
        }
    }
})
// Saves one reading every second while A or B is on.
loops.everyInterval(1000, function () {
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("soil moisture", inputcurrent)
        datalogger.log(datalogger.createCV("soil moisture", inputcurrent))
    }
})
```

## Lesson 3 - Station 3 Soil Moisture Sensor

This project has the code for **Station 3 (Soil moisture)**. Set it up before class.

- Press **A** to show the soil moisture (%) as a bar graph.
- Press **B** to show a face: happy for wet soil, neutral in between, sad for dry soil.
- Press **A+B** to show the station number, stop saving readings and erase the data log.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Setup

Connect the soil moisture sensor and push its prongs into the soil.

## The faces

Find the ``||logic:if||`` block that chooses the face.

```blocks
let inputcurrent = 0
// @highlight
if (inputcurrent > 50) {
    basic.showIcon(IconNames.Happy)
} else if (inputcurrent > 20) {
    basic.showLeds(`
        . . . . .
        . # . # .
        . . . . .
        . # # # .
        . . . . .
        `)
} else {
    basic.showIcon(IconNames.Sad)
}
```

- Over 50%: happy face.
- Over 20% up to 50%: neutral face.
- 20% or less: sad face.

**Calibrate:** if only one face ever appears with your soil, change **20** and **50** to fit your readings from the bar graph.

## Saving the data

The ``||loops:every 1000 ms||`` block saves one reading every second while **A** or **B** is on. Switching between **A** and **B** keeps the data. Only **A+B** erases it, so save your data first.

## Check

Download the code. The micro:bit shows **3**. Press **B** and a face shows.

## How to use the code

- When it starts, the micro:bit shows **3**. It does not save data yet.
- Press **A** for the bar graph or **B** for the face. Either one starts saving a reading every second.
- Keep the micro:bit connected by USB and open **Show data** to watch the graph.
- Press **A+B** to stop. The data log is erased, so save your data first.

## Technical notes

The ``||basic:forever||`` loop reads the sensor and updates the screen. The ``||loops:every 1000 ms||`` loop sends the reading to the computer and saves it to the data log, once every second. The two jobs are kept apart so the readings stay one second apart.

The reading is the soil moisture in %, rounded to a whole number. The bar graph is full at 100%.

Click **Done**, then download the code to your micro:bit.
