# Lesson 16 - Water Pump and Soil Moisture Sensor

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
    basic.showIcon(IconNames.Yes)
})
let input2 = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    input2 = opensciedModules.moisture1.moistureLevel()
    serial.writeValue("data from micro:bit", input2)
    if (outputchoice == "A") {
        if (input2 >= 50) {
            basic.showIcon(IconNames.Happy)
            opensciedModules.pump.setOn(false)
        } else if (input2 > 20 && input2 < 50) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . # # # .
                . . . . .
                `)
            opensciedModules.pump.setOn(false)
        } else {
            basic.showIcon(IconNames.Sad)
            opensciedModules.pump.timedRun(500)
        }
    }
})
```

## Lesson 16 - Water Pump and Soil Moisture Sensor

This project has the code for **Water Pump and Soil Moisture Sensor**.

Click **Done**, then download the code to your micro:bit.
