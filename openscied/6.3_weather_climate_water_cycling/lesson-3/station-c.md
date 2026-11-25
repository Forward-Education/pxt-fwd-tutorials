# Lesson 3 - Sensor Station C (Light)

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v0.0.6
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
let luxrounded = 0
let inputcurrent = 0
let columnname = ""
let scrolldisplay = false
let logging = false
logging = false
scrolldisplay = false
columnname = "Light intensity (lux)"
basic.showLeds(`
    # . . . #
    # . . . .
    # . . . #
    # . . . #
    # # # . #
    `)
basic.forever(function () {
    inputcurrent = opensciedModules.light1.illuminance()
    luxrounded = Math.round(inputcurrent * 10) / 10
    output = luxrounded
    if (logging == true) {
        datalogger.log(datalogger.createCV(columnname, output))
        datalogger.mirrorToSerial(true)
    }
    if (scrolldisplay == true) {
        basic.showString("Li:")
        basic.showString("" + (output))
        basic.clearScreen()
    }
})
```

## Lesson 3 - Sensor Station C (Light) @showdialog

This project already has the code for **Sensor Station C (Light)**.

Click **Done**, then download the code to your micro:bit.
