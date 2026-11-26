# Lesson 12 - Pressure Sensor

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
let sensorinput = 0
let radiogroupnumber = 0
radiogroupnumber = 12
radio.setGroup(radiogroupnumber)
basic.showLeds(`
    . # # # .
    . # . # .
    . # # # .
    . # . . .
    . # . . .
    `)
// Reads the sensor and scrolls the value on the screen.
// Scrolling text takes a few seconds, so it gets its own loop
// to keep it from slowing down the radio sending.
basic.forever(function () {
    sensorinput = Math.round(opensciedModules.bmeAirPressure.pressure())
    basic.showNumber(sensorinput)
})
// Sends one reading every second, so the receiver gets evenly spaced data.
loops.everyInterval(1000, function () {
    radio.sendValue("pressure", sensorinput)
})
```

## Lesson 12 - Pressure Sensor

This project has the code for **Pressure Sensor**.

## How to use the code

When the micro:bit starts, it shows a **P** for pressure. Then it scrolls the air pressure reading over and over and sends a reading to the receiver every second.

## Technical notes

The code uses two loops that run at the same time:

- The ``||basic:forever||`` loop reads the pressure sensor and scrolls the value on the screen.
- The ``||loops:every 1000 ms||`` loop sends one reading by radio every second.

Scrolling text on the micro:bit takes a few seconds. If both jobs were in the same loop, a reading would only be sent after each scroll finished. Keeping them in separate loops means the receiver gets one reading every second, no matter what the screen is doing.

Click **Done**, then download the code to your micro:bit.
