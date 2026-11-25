# Lesson 5 - Dual Light and Temperature Sensors

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    displaystate = 1
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    displaystate = 0
})
input.onButtonPressed(Button.B, function () {
    displaystate = 2
    basic.clearScreen()
})
function cyclemenuchoice () {
    basic.showLeds(`
        # . . . #
        # . . . .
        # . . . #
        # . . . #
        # # # . #
        `)
    basic.pause(500)
    basic.showLeds(`
        # . # # #
        . . # . .
        . . # # #
        . . # . .
        . . # . .
        `)
    basic.pause(500)
}
let lightintensity = 0
let tempoutput = 0
let displaystate = 0
let stationlabel = "1.a"
displaystate = 0
basic.forever(function () {
    lightintensity = opensciedModules.light1.illuminance()
    tempoutput = opensciedModules.round(opensciedModules.bmeTemperature.readTemperature(opensciedEnums.TemperatureUnit.Fahrenheit), 1)
    if (displaystate == 0) {
        cyclemenuchoice()
    }
    if (displaystate == 1) {
        basic.showString("Li:")
        basic.showString("" + (opensciedModules.round(lightintensity, 1)))
        basic.clearScreen()
    }
    if (displaystate == 2) {
        basic.showString("F:")
        basic.showString("" + (tempoutput))
        basic.clearScreen()
    }
})
```

## Lesson 5 - Dual Light and Temperature Sensors

This project has the code for **Dual Light and Temperature Sensors**.

Click **Done**, then download the code to your micro:bit.
