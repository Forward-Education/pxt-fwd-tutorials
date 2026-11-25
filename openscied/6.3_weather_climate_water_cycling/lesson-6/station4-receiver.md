# Lesson 6 - Station 4 Receiver

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    displaystate = 1
    latestavalue = -1
    latestbvalue = -1
    basic.showLeds(`
        . . # . .
        . . # . .
        # # # # #
        . . # . .
        . . # . .
        `)
})
input.onButtonPressed(Button.B, function () {
    displaystate = 0
    basic.showString("" + (radiogroupnumber))
})
radio.onReceivedValue(function (name, value) {
    if (displaystate == 1) {
        if (name == "sensor 1") {
            latestavalue = value
        }
        if (name == "sensor 2") {
            latestbvalue = value
        }
        if (name == "sensor 1" || name == "sensor 2") {
            serial.writeValue("Sensor-1-Humidity", latestavalue)
            serial.writeValue("Sensor-2-Humidity", latestbvalue)
        }
    }
})
let latestbvalue = 0
let latestavalue = 0
let displaystate = 0
let radiogroupnumber = 0
radiogroupnumber = 4
let sensor_1 = "sensor 1"
let sensor_2 = "sensor 2"
displaystate = 0
latestavalue = 0
latestbvalue = 0
radio.setGroup(radiogroupnumber)
basic.showString("" + (radiogroupnumber))
```

## Lesson 6 - Station 4 Receiver

This project has the code for **Station 4 Receiver**.

Click **Done**, then download the code to your micro:bit.
