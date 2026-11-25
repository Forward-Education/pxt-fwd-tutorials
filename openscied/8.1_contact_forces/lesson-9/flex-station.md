# Lesson 9 - Flex Station

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    output = "A"
})
input.onButtonPressed(Button.AB, function () {
    output = "station"
    basic.showString(station_name)
})
input.onButtonPressed(Button.B, function () {
    output = "B"
})
let output = ""
let station_name = ""
station_name = "F"
output = "station"
basic.showString(station_name)
basic.forever(function () {
    if (output == "A") {
        basic.showNumber(opensciedModules.flex1.flex())
    }
    if (output == "B") {
        if (opensciedModules.flex1.isPastThreshold(8, opensciedEnums.OverUnder.Under)) {
            basic.showIcon(IconNames.Happy)
        }
        if (opensciedModules.flex1.isPastThreshold(8, opensciedEnums.OverUnder.Over) && opensciedModules.flex1.isPastThreshold(15, opensciedEnums.OverUnder.Under)) {
            basic.showIcon(IconNames.Asleep)
        }
        if (opensciedModules.flex1.isPastThreshold(15, opensciedEnums.OverUnder.Over)) {
            basic.showIcon(IconNames.Sad)
        }
    }
})
```

## Lesson 9 - Flex Station

This project has the code for **Flex Station**.

Click **Done**, then download the code to your micro:bit.
