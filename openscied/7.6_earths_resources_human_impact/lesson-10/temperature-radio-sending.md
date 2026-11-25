# Lesson 10 - Temperature Sensor with Radio Sending

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    radio.setGroup(1)
    basic.clearScreen()
    datalogger.deleteLog()
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    radio.setGroup(2)
    basic.clearScreen()
    datalogger.deleteLog()
})
let inputcurrenttemp = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    inputcurrenttemp = opensciedModules.bmeTemperature.temperature()
    if (outputchoice == "A" || outputchoice == "B") {
        basic.showNumber(inputcurrenttemp)
        serial.writeValue("temp data from micro:bit", inputcurrenttemp)
        serial.writeNumbers([inputcurrenttemp])
        datalogger.log(datalogger.createCV("temp", inputcurrenttemp))
        radio.sendValue("temp", inputcurrenttemp)
    }
    basic.pause(5000)
})
```

## Lesson 10 - Temperature Sensor with Radio Sending

This project has the code for **Temperature Sensor with Radio Sending**.

Click **Done**, then download the code to your micro:bit.
