# Lesson 9 - Rotary Dial Station

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Works out how far the dial has turned from the start and shows it.
// Each click of the dial is 18 degrees (20 clicks make one full turn).
function showTurn () {
    degrees = opensciedModules.dial1.position() * 18
    if (degrees > 0) {
        direction = "CW"
    } else if (degrees < 0) {
        direction = "CCW"
    } else {
        direction = "start"
    }
    // The bar graph shows the current turn. A full bar is one full turn (360 degrees).
    led.plotBarGraph(
    Math.abs(degrees) % 360,
    360
    )
    opensciedModules.lcd1.printQuadrantString("Turn", 1)
    opensciedModules.lcd1.printQuadrantString(direction, 2)
    opensciedModules.lcd1.printQuadrantString("Degrees", 3)
    opensciedModules.lcd1.printQuadrantNumber(Math.abs(degrees), 4)
}
opensciedModules.dial1.onRotated(opensciedEnums.ClockwiseCounterclockwise.Clockwise, function () {
    showTurn()
})
opensciedModules.dial1.onRotated(opensciedEnums.ClockwiseCounterclockwise.Counterclockwise, function () {
    showTurn()
})
// Pressing the dial sets the current position as the new start (0 degrees).
opensciedModules.dialButton1.onEvent(jacdac.ButtonEvent.Down, function () {
    opensciedModules.dial1.resetPosition()
    showTurn()
})
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    basic.clearScreen()
    basic.showString(station_name)
})
let direction = ""
let degrees = 0
let station_name = ""
opensciedModules.initializeLcd()
station_name = "R"
basic.showString(station_name)
showTurn()
```

## Lesson 9 - Rotary Dial Station

This project has the code for the **Rotary Dial Station**.

## How to use the code

- Turn the dial. Each click is 18 degrees, so 20 clicks make one full turn.
- The LCD shows the direction from the start on line 1 (**CW** for clockwise, **CCW** for counterclockwise) and how many degrees from the start on line 2.
- The micro:bit bar graph shows the current turn. A full bar is one full turn (360 degrees).
- Press the dial to set the current position as the new start (0 degrees).
- Press **A** or **B** to clear the micro:bit screen. Press **A+B** together to show the station letter **R**.

## Technical notes

The ``||opensciedModules:dial1 position||`` block counts clicks from the start: clockwise clicks add 1 and counterclockwise clicks take away 1. The code multiplies the clicks by 18 to get degrees, and shows the size of the angle with the direction on the line above it.

Click **Done**, then download the code to your micro:bit.
