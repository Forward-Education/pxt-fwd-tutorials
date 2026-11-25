# Lesson 12 - Slider Force Sensor System

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.0.0
all-fwd-blocks=github:forward-education/pxt-all-fwd-blocks#v2.0.1
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
let inputslide = 0
let status = ""
status = "home"
basic.forever(function () {
    inputslide = opensciedModules.slider1.position()
    if (status == "setup") {
        basic.showNumber(inputslide)
    } else if (status == "test") {
        if (inputslide > 50) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.Sad)
        }
    } else {
        basic.showIcon(IconNames.House)
    }
})
```

## Lesson 12 - Slider Force Sensor System

This project has the code for **Slider Force Sensor System**.

Click **Done**, then download the code to your micro:bit.
