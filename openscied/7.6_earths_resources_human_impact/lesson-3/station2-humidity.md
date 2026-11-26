# Lesson 3 - Station 2 Humidity Sensor

```package
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Reads the absolute humidity (g/m3), rounded to 2 decimal places.
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
// Shows the humidity as a bar graph and starts saving readings.
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
// Plays the humidity as a sound and starts saving readings.
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
})
let inputcurrent = 0
let abshumidityrounded = 0
let outputchoice = ""
let station_number = 0
station_number = 2
outputchoice = "station"
datalogger.setColumnTitles("humidity")
basic.showNumber(station_number)
// Reads the sensor and shows or plays the reading the way A or B chose.
// Each tone lasts a beat, so the output gets its own loop
// to keep it from slowing down the data logging.
basic.forever(function () {
    calcAbsHumidity()
    inputcurrent = abshumidityrounded
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    } else if (outputchoice == "B") {
        music.setVolume(inputcurrent * 6)
        music.play(music.tonePlayable(inputcurrent * 20, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
})
// Saves one reading every second while A or B is on.
loops.everyInterval(1000, function () {
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("humidity", inputcurrent)
        datalogger.log(datalogger.createCV("humidity", inputcurrent))
    }
})
```

## Lesson 3 - Station 2 Humidity Sensor @showdialog

This project has the code for **Station 2 (Absolute humidity)**. Set it up before class.

- Press **A** to show the absolute humidity (g/m3) as a bar graph.
- Press **B** to hear it as a sound. More humid air plays a higher, louder tone.
- Press **A+B** to show the station number, stop saving readings and erase the data log.

## Setup

Connect the BME280 sensor to the breakout board.

## The humidity and the sound

Find the ``||basic:forever||`` loop. It calls ``calcAbsHumidity`` to read the absolute humidity, then the sound blocks turn it into a tone.

```blocks
let abshumidityrounded = 0
let inputcurrent = 0
let outputchoice = ""
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
basic.forever(function () {
    // @highlight
    calcAbsHumidity()
    inputcurrent = abshumidityrounded
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    } else if (outputchoice == "B") {
        // @highlight
        music.setVolume(inputcurrent * 6)
        // @highlight
        music.play(music.tonePlayable(inputcurrent * 20, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
})
```

## Saving the data

The ``||loops:every 1000 ms||`` block saves one reading every second while **A** or **B** is on. Switching between **A** and **B** keeps the data. Only **A+B** erases it, so save your data first.

## Check

Download the code. The micro:bit shows **2**. Press **B** and a tone plays.

## Technical notes

The ``||basic:forever||`` loop handles the display and sound, and the ``||loops:every 1000 ms||`` loop handles the data log. Each tone lasts a beat, so keeping the two jobs apart means the readings stay one second apart.

Click **Done**, then download the code to your micro:bit.
