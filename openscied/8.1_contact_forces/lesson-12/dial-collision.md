# Lesson 12 - Rotary Dial Force Sensor System

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    status = "setup"
})
input.onButtonPressed(Button.B, function () {
    status = "test"
})
let inputposition = 0
let status = ""
status = "home"
basic.forever(function () {
    inputposition = opensciedModules.dial4.position()
    if (status == "setup") {
        basic.showNumber(inputposition)
    } else if (status == "test") {
        if (inputposition > 0) {
            basic.showIcon(IconNames.Happy)
        } else if (inputposition < 0) {
            basic.showIcon(IconNames.Sad)
        } else {
            basic.showIcon(IconNames.House)
        }
    }
})
```

## Lesson 12 - Rotary Dial Force Sensor System

This project has the code for **Rotary Dial Force Sensor System**.

Click **Done**, then download the code to your micro:bit.
