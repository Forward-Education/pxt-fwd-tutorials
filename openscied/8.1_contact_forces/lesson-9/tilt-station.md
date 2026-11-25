# Lesson 9 - Tilt Station

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    output = "A"
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    output = "AB"
    basic.showString(station_name)
})
input.onButtonPressed(Button.B, function () {
    output = "B"
    basic.clearScreen()
})
let output = ""
let station_name = ""
station_name = "T"
output = "AB"
basic.showString(station_name)
basic.forever(function () {
    if (output == "A") {
        led.plotBarGraph(
        Math.abs(input.rotation(Rotation.Pitch)),
        180
        )
    } else if (output == "B") {
        basic.showNumber(input.rotation(Rotation.Pitch))
    }
})
```

## Lesson 9 - Tilt Station

This project has the code for **Tilt Station**.

Click **Done**, then download the code to your micro:bit.
