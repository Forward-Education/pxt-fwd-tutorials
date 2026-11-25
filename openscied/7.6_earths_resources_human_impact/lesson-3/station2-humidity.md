# Lesson 3 - Station 2 Humidity Sensor

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
    datalogger.deleteLog()
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
    basic.showNumber(station_number)
    datalogger.deleteLog()
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
    datalogger.deleteLog()
})
let inputcurrent = 0
let abshumidityrounded = 0
let outputchoice = ""
let station_number = 0
station_number = 2
outputchoice = "station"
basic.showNumber(station_number)
basic.forever(function () {
    calcAbsHumidity()
    inputcurrent = abshumidityrounded
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    }
    if (outputchoice == "B") {
        music.setVolume(inputcurrent * 6)
        music.play(music.tonePlayable(inputcurrent * 20, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    }
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("humidity data from micro:bit", inputcurrent)
        serial.writeNumbers([inputcurrent])
        datalogger.log(datalogger.createCV("humidity", inputcurrent))
    }
    basic.pause(1000)
})
```

## Lesson 3 - Station 2 Humidity Sensor

This project has the code for **Station 2 Humidity Sensor**.

Click **Done**, then download the code to your micro:bit.
