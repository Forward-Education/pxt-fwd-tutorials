# Lesson 7 - Tilt Sensor Receiver and Data Logger

```package
radio=radio
microphone=microphone
datalogger=datalogger
```

```template
radio.onReceivedNumber(function (receivedNumber) {
    currentangle = receivedNumber
    serial.writeNumbers([currentangle, initialangle])
})
input.onButtonPressed(Button.A, function () {
    radio.sendString("A")
    serial.writeLine("Countdown....")
    goreceived = false
    basic.showIcon(IconNames.Happy)
})
function showRadioGroup () {
    basic.clearScreen()
    basic.pause(100)
    basic.showString("R")
    basic.pause(1000)
    basic.showNumber(myradiogroup)
    basic.pause(1000)
    basic.clearScreen()
}
input.onButtonPressed(Button.AB, function () {
    radio.sendString("A+B")
    showRadioGroup()
})
radio.onReceivedString(function (receivedString) {
    if (receivedString == "A+B") {
        showRadioGroup()
    } else if (receivedString == "ready") {
        basic.showString("+")
    } else if (receivedString == "go") {
        goreceived = true
    } else if (receivedString == "stop") {
        if (goreceived == true) {
            basic.showIcon(IconNames.Yes)
        }
    } else {
        basic.showString(receivedString)
    }
})
input.onButtonPressed(Button.B, function () {
    radio.sendString("B")
})
radio.onReceivedValue(function (name, value) {
    initialangle = value
    serial.writeLine("")
})
let initialangle = 0
let currentangle = 0
let goreceived = false
let myradiogroup = 0
serial.writeLine("Startup")
myradiogroup = 1
radio.setGroup(myradiogroup)
goreceived = false
basic.showIcon(IconNames.Heart)
```

## Lesson 7 - Tilt Sensor Receiver and Data Logger

This project has the code for **Tilt Sensor Receiver and Data Logger**.

Click **Done**, then download the code to your micro:bit.
