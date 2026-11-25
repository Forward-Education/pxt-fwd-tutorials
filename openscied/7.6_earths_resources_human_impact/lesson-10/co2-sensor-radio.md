# Lesson 10 - CO2 Sensor with Radio (Example)

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
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
radio.setGroup(1)
basic.forever(function () {
    CO2 = opensciedModules.eCO2.eco2()
    HUMIDITY = opensciedModules.bmeHumidity.humidity()
    if (outputchoice == "A") {
        OUTPUT = CO2
        serial.writeValue("CO2: ", OUTPUT)
        radio.sendValue("CO2:", OUTPUT)
    }
    if (outputchoice == "B") {
        OUTPUT = HUMIDITY
        serial.writeValue("Humidity", OUTPUT)
        radio.sendValue("Humidity", OUTPUT)
    }
    basic.showNumber(OUTPUT)
    basic.pause(5000)
})
```

## Lesson 10 - CO2 Sensor with Radio (Example)

This project has the code for **CO2 Sensor with Radio (Example)**.

Click **Done**, then download the code to your micro:bit.
