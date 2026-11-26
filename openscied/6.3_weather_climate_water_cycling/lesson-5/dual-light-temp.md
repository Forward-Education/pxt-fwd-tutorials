# Lesson 5 - Dual Light and Temperature Sensors

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    displaystate = "light"
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    displaystate = "menu"
})
input.onButtonPressed(Button.B, function () {
    displaystate = "temp"
    basic.clearScreen()
})
let displaystate = ""
displaystate = "menu"
// Shows the menu or a sensor value, depending on the last button pressed.
basic.forever(function () {
    if (displaystate == "menu") {
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
    } else if (displaystate == "light") {
        basic.showString("Li:" + opensciedModules.round(opensciedModules.light1.illuminance(), 1))
        basic.clearScreen()
    } else if (displaystate == "temp") {
        basic.showString("F:" + opensciedModules.round(opensciedModules.temperature1.readTemperature(opensciedEnums.TemperatureUnit.Fahrenheit), 1))
        basic.clearScreen()
    }
})
```

## Lesson 5 - Dual Light and Temperature Sensors

This project has the code for **Dual Light and Temperature Sensors**.

## How to use the code

When the micro:bit starts, it shows a menu that switches between a light icon and a temperature icon.

- Press **A** to show the light reading. It scrolls on the screen over and over.
- Press **B** to show the temperature reading. It scrolls on the screen over and over.
- Press **A+B** together to go back to the menu.

The micro:bit finishes what is on the screen before it switches, so a button press can take a moment to show.

## Technical notes

The buttons only change the ``displaystate`` variable. One ``||basic:forever||`` loop checks that variable and decides what to show:

- **menu**: the light icon and the **F** icon, half a second each.
- **light**: the light sensor reading in lux, rounded to 1 decimal place, with the label **Li:**.
- **temp**: the temperature in °F, rounded to 1 decimal place, with the label **F:**. Change ``Fahrenheit`` to ``Celsius`` in the block if you want °C.

The sensor is read again each time the text starts to scroll, so each new scroll shows a fresh reading. This code does not save data or send it to the computer.

Click **Done**, then download the code to your micro:bit.
