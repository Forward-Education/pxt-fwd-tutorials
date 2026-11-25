# Lesson 3 - Sensor Station B (Humidity)

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
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
let inputcurrent = 0
let abshumidityrounded = 0
let columnname = ""
let scrolldisplay = false
let logging = false
logging = false
scrolldisplay = false
columnname = "Abs. humidity (g/m3)"
basic.showString("H")
basic.forever(function () {
    calcAbsHumidity()
    inputcurrent = abshumidityrounded
    if (logging == true) {
        datalogger.log(datalogger.createCV(columnname, inputcurrent))
        datalogger.mirrorToSerial(true)
    }
    if (scrolldisplay == true) {
        basic.showString("H:")
        basic.showString("" + (inputcurrent))
        basic.clearScreen()
    }
})
```

## Lesson 3 - Sensor Station B (Humidity)

This project has the code for **Sensor Station B (Humidity)**.

Click **Done**, then download the code to your micro:bit.
