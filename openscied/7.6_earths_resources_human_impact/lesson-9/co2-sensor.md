# Lesson 9 - CO2 Sensor

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
})
let OUTPUT = 0
let HUMIDITY = 0
let CO2 = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    CO2 = opensciedModules.eCO2.eco2()
    HUMIDITY = opensciedModules.bmeHumidity.humidity()
    if (outputchoice == "A") {
        OUTPUT = CO2
        serial.writeValue("CO2: ", OUTPUT)
    }
    if (outputchoice == "B") {
        OUTPUT = HUMIDITY
        serial.writeValue("Humidity", OUTPUT)
    }
    basic.showNumber(OUTPUT)
    basic.pause(5000)
})
```

## Lesson 9 - CO2 Sensor

This project has the code for **CO2 Sensor**.

Click **Done**, then download the code to your micro:bit.
