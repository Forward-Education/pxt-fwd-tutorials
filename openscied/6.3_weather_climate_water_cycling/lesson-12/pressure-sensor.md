# Lesson 12 - Pressure Sensor

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
input.onButtonPressed(Button.B, function () {
    basic.showString("" + (radiogroupnumber))
})
let sensorinput = 0
let radiogroupnumber = 0
radiogroupnumber = 12
radio.setGroup(radiogroupnumber)
basic.showLeds(`
    . # # # .
    . # . # .
    . # # # .
    . # . . .
    . # . . .
    `)
basic.forever(function () {
    sensorinput = Math.round(opensciedModules.bmeAirPressure.pressure())
    radio.sendValue("pressure", sensorinput)
    basic.showString("" + (sensorinput))
})
```

## Lesson 12 - Pressure Sensor @showdialog

This project already has the code for **Pressure Sensor**.

Click **Done**, then download the code to your micro:bit.
