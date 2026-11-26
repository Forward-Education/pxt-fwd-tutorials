# Lesson 9 - Tilt Station

```package
radio=radio
```

```template
input.onButtonPressed(Button.A, function () {
    output = "A"
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    output = "B"
    basic.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    output = "AB"
    basic.showString(station_name)
})
let output = ""
let station_name = ""
station_name = "T"
output = "AB"
basic.showString(station_name)
// A shows the tilt as a bar graph (a full bar is 90 degrees).
// B shows the tilt angle as a number. Tilting the other way gives a negative number.
basic.forever(function () {
    if (output == "A") {
        led.plotBarGraph(
        Math.abs(input.rotation(Rotation.Pitch)),
        90
        )
    } else if (output == "B") {
        basic.showNumber(input.rotation(Rotation.Pitch))
    }
})
```

## Lesson 9 - Tilt Station

This project has the code for the **Tilt Station**.

## How to use the code

- Press **A** to show the tilt as a bar graph. A full bar is 90 degrees (standing straight up).
- Press **B** to show the tilt angle in degrees. Tilting forward and back give opposite signs (+ or -).
- Press **A+B** together to show the station letter **T**.

## Technical notes

The ``||input:rotation pitch||`` block gives the tilt from -180 to 180 degrees. The bar graph uses the size of the angle (no sign), so it fills the same way in both directions and is full at 90 degrees.

Click **Done**, then download the code to your micro:bit.
