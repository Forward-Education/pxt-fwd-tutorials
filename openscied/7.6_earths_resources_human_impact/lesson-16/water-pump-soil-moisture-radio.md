# Lesson 16 - Water Pump and Soil Moisture with Radio (Example)

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
radio.onReceivedValue(function (name, value) {
    if (value == on) {
        opensciedModules.pump.timedRun(500)
    } else {
        opensciedModules.pump.setOn(false)
    }
})
let input2 = 0
let on = 0
let outputchoice = ""
radio.setGroup(1)
outputchoice = "station"
let off = 0
on = 1
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    input2 = opensciedModules.moisture1.moistureLevel()
    serial.writeValue("data from micro:bit", input2)
    if (outputchoice == "A") {
        if (input2 >= 50) {
            basic.showIcon(IconNames.Happy)
            radio.sendValue("pump?", off)
        } else if (input2 > 20 && input2 < 50) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . # # # .
                . . . . .
                `)
            radio.sendValue("pump?", off)
        } else {
            basic.showIcon(IconNames.Sad)
            radio.sendValue("pump?", on)
        }
    }
})
```

## Lesson 16 - Water Pump and Soil Moisture with Radio (Example)

This project has the code for **Water Pump and Soil Moisture with Radio (Example)**.

Click **Done**, then download the code to your micro:bit.
