# Lesson 7 - Teacher Data Hub

```package
radio=radio
microphone=microphone
```

```template
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 1) {
        _1stsensorcomplete = true
    } else if (receivedNumber == 2) {
        _2ndsensorcomplete = true
    }
    if (_1stsensorcomplete && _2ndsensorcomplete) {
        basic.showIcon(IconNames.Yes)
    }
})
input.onButtonPressed(Button.A, function () {
    basic.showString("A")
    radio.sendString("A")
    status = "A"
    ResetComplete()
})
input.onButtonPressed(Button.AB, function () {
    status = "A+B"
    basic.showIcon(IconNames.No)
    radio.sendString("X")
    ResetComplete()
})
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    radio.sendString("B")
    status = "B"
    ResetComplete()
})
radio.onReceivedValue(function (name, value) {
    label = "Sensor " + name
    if (name == "0") {
        sensor0value = value
    } else if (name == "1") {
        sensor1value = value
    }
    if (status == "A") {
        serial.writeValue(label, value)
    } else if (status == "B") {
        serial.writeNumbers([sensor0value, sensor1value])
    }
})
function ResetComplete () {
    _1stsensorcomplete = false
    _2ndsensorcomplete = false
    sensor0value = 0
    sensor1value = 0
}
let sensor1value = 0
let sensor0value = 0
let label = ""
let _2ndsensorcomplete = false
let _1stsensorcomplete = false
let status = ""
radio.setGroup(1)
basic.showString("+")
ResetComplete()
let statusAB = false
status = "-"
```

## Lesson 7 - Teacher Data Hub

This project has the code for **Teacher Data Hub**.

Click **Done**, then download the code to your micro:bit.
