# Lesson 3 - Station 1 Temperature Sensor

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
station_number = 1
outputchoice = "station"
basic.showNumber(station_number)
basic.forever(function () {
    inputcurrent = opensciedModules.bmeTemperature.readTemperature()
    if (outputchoice == "A") {
        led.plotBarGraph(
        inputcurrent,
        35
        )
    }
    if (outputchoice == "B") {
        basic.showNumber(inputcurrent)
    }
    if (outputchoice == "A" || outputchoice == "B") {
        serial.writeValue("temp data from micro:bit", inputcurrent)
        serial.writeNumbers([inputcurrent])
        datalogger.log(datalogger.createCV("temperature", inputcurrent))
    }
    basic.pause(1000)
})
```

## Lesson 3 - Station 1 Temperature Sensor

This project has the code for **Station 1 Temperature Sensor**.

Click **Done**, then download the code to your micro:bit.
