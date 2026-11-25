# Lesson 3 - Sensor Station A (Temperature)

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    basic.showIcon(IconNames.Yes)
    basic.pause(500)
    datalogger.deleteLog(datalogger.DeleteType.Full)
    datalogger.setColumnTitles(columnname)
    logging = true
    scrolldisplay = true
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    scrolldisplay = false
    logging = false
    basic.showIcon(IconNames.Happy)
})
let output = 0
let columnname = ""
let scrolldisplay = false
let logging = false
logging = false
scrolldisplay = false
columnname = "Temperature (F)"
basic.showLeds(`
    # . # # #
    . . # . .
    . . # # #
    . . # . .
    . . # . .
    `)
basic.forever(function () {
    output = opensciedModules.round(opensciedModules.temperature1.readTemperature(opensciedEnums.TemperatureUnit.Fahrenheit), 1)
    if (logging == true) {
        datalogger.log(datalogger.createCV(columnname, output))
        datalogger.mirrorToSerial(true)
    }
    if (scrolldisplay == true) {
        basic.showString("F:")
        basic.showString("" + (output))
    }
})
```

## Lesson 3 - Sensor Station A (Temperature)

This project has the code for **Sensor Station A (Temperature)**.

Click **Done**, then download the code to your micro:bit.
