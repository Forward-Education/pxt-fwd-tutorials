# Lesson 12 - Accelerometer Force Sensor System

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    status = "setup"
})
input.onButtonPressed(Button.AB, function () {
    status = "home"
})
input.onButtonPressed(Button.B, function () {
    status = "test"
})
let inputacceleration = 0
let status = ""
status = "home"
basic.forever(function () {
    inputacceleration = input.acceleration(Dimension.Strength)
    if (status == "setup") {
        basic.showNumber(inputacceleration)
    } else if (status == "test") {
        if (inputacceleration > 1400) {
            basic.showIcon(IconNames.Sad)
            basic.pause(2000)
        } else {
            basic.showIcon(IconNames.Happy)
        }
    } else {
        basic.showIcon(IconNames.House)
    }
})
```

## Lesson 12 - Accelerometer Force Sensor System

This project has the code for **Accelerometer Force Sensor System**.

Click **Done**, then download the code to your micro:bit.
