# Lesson 3 - Combined Sensor Code

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
function calcAbsHumidity () {
    abshumidityfactor = 13.247 * (inputcurrenthumidity / (273.15 + inputcurrenttemp))
    abshumidityexponent = 2.7183 ** (17.67 * inputcurrenttemp / (243.5 + inputcurrenttemp))
    abshumidityinitial = abshumidityfactor * abshumidityexponent
    abshumidityrounded = Math.round(abshumidityinitial * 100) / 100
}
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
    datalogger.deleteLog()
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    basic.clearScreen()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    outputchoice = "C"
    basic.clearScreen()
})
let inputcurrentsoil = 0
let abshumidityrounded = 0
let abshumidityinitial = 0
let abshumidityexponent = 0
let inputcurrenttemp = 0
let inputcurrenthumidity = 0
let abshumidityfactor = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    inputcurrenttemp = opensciedModules.bmeTemperature.temperature()
    inputcurrenthumidity = opensciedModules.bmeHumidity.humidity()
    inputcurrentsoil = opensciedModules.moisture1.moistureLevel()
    calcAbsHumidity()
    if (outputchoice == "A") {
        basic.showNumber(inputcurrenttemp)
    }
    if (outputchoice == "B") {
        basic.showNumber(abshumidityrounded)
    }
    if (outputchoice == "C") {
        basic.showNumber(inputcurrentsoil)
    }
    if (outputchoice == "A" || outputchoice == "B" || outputchoice == "C") {
        let humiditytotenthsplace = 0
        serial.writeValue("temp data from micro:bit", inputcurrenttemp)
        serial.writeValue("abs humidity data from micro:bit", abshumidityrounded)
        serial.writeValue("soil moisture data from micro:bit", inputcurrentsoil)
        serial.writeNumbers([
        inputcurrenttemp,
        abshumidityrounded,
        inputcurrentsoil
        ])
        datalogger.log(
        datalogger.createCV("temp", inputcurrenttemp),
        datalogger.createCV("humidity", abshumidityrounded),
        datalogger.createCV("soil moisture", inputcurrentsoil)
        )
    }
    basic.pause(1000)
})
```

## Lesson 3 - Combined Sensor Code

This project has the code for **Combined Sensor Code**.

Click **Done**, then download the code to your micro:bit.
