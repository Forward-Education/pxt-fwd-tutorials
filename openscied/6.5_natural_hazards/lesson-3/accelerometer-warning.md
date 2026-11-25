# Lesson 3 - Accelerometer Warning

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    status = "default"
    basic.showString("A")
    basic.pause(500)
    maxinput = initialinput
})
function DisplayNewWarning () {
    if (maxinput > 2000 && maxinput < 4000) {
        basic.showString("!")
    }
}
input.onButtonPressed(Button.B, function () {
    status = "warn"
    basic.showString("B")
    basic.pause(500)
    maxinput = initialinput
})
let nextinput = 0
let maxinput = 0
let status = ""
let initialinput = 0
input.setAccelerometerRange(AcceleratorRange.EightG)
initialinput = input.acceleration(Dimension.Strength)
status = "default"
serial.writeString(status)
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
loops.everyInterval(500, function () {
    basic.clearScreen()
    if (status == "warn") {
        DisplayNewWarning()
    }
    maxinput = initialinput
})
basic.forever(function () {
    // The maximum value that can be detected is 8000 mg (or 8g)
    nextinput = input.acceleration(Dimension.Strength)
    serial.writeValue("Input", nextinput)
    if (nextinput > maxinput) {
        maxinput = nextinput
    }
})
```

## Lesson 3 - Accelerometer Warning

This project has the code for **Accelerometer Warning**.

Click **Done**, then download the code to your micro:bit.
