# Lesson 9 - Rotary Dial Station

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
})
opensciedModules.dial1.onRotated(opensciedEnums.ClockwiseCounterclockwise.Clockwise, function () {
    led.plotBarGraph(
    Math.abs(opensciedModules.dial1.position()) * 18,
    360
    )
})
opensciedModules.dial1.onRotated(opensciedEnums.ClockwiseCounterclockwise.Counterclockwise, function () {
    basic.showNumber(Math.abs(opensciedModules.dial1.position() * 18 - 360))
})
input.onButtonPressed(Button.AB, function () {
    basic.clearScreen()
    basic.showString(station_name)
})
input.onButtonPressed(Button.B, function () {
    basic.clearScreen()
})
let station_name = ""
station_name = "R"
basic.showString(station_name)
```

## Lesson 9 - Rotary Dial Station

This project has the code for **Rotary Dial Station**.

Click **Done**, then download the code to your micro:bit.
