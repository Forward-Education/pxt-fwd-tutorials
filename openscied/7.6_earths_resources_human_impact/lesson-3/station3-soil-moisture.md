# Lesson 3 - Station 3 Soil Moisture Sensor

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
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
let outputchoice = ""
let station_number = 0
station_number = 3
outputchoice = "station"
basic.showNumber(station_number)
basic.forever(function () {
    inputcurrent = opensciedModules.moisture1.moistureLevel()
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        100
        )
    }
    if (outputchoice == "B") {
        if (inputcurrent >= 50) {
            basic.showIcon(IconNames.Happy)
        } else if (inputcurrent > 20 && inputcurrent < 50) {
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
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("soil moisture data from micro:bit", inputcurrent)
        serial.writeNumbers([inputcurrent])
        datalogger.log(datalogger.createCV("soil moisture", inputcurrent))
    }
    basic.pause(1000)
})
```

## Lesson 3 - Station 3 Soil Moisture Sensor

This project has the code for **Station 3 Soil Moisture Sensor**.

Click **Done**, then download the code to your micro:bit.
