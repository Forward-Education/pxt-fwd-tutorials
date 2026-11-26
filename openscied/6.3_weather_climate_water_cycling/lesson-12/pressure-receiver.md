# Lesson 12 - Pressure Radio Receiver

```package
radio=radio
microphone=microphone
```

```template
// Sends each reading to the computer right away and remembers it for the screen.
// The top-left light blinks for each reading.
radio.onReceivedValue(function (name, value) {
    serial.writeValue(name, value)
    pressure = value
    received = true
    led.toggle(0, 0)
})
let received = false
let pressure = 0
let radiogroupnumber = 0
received = false
radiogroupnumber = 12
radio.setGroup(radiogroupnumber)
basic.showLeds(`
    . # # # .
    . # . # .
    . # # # .
    . # . . .
    . # . . .
    `)
// Scrolls the latest reading on the screen.
// Scrolling takes a few seconds, so it runs in its own loop
// to keep it from holding up incoming readings.
basic.forever(function () {
    if (received) {
        basic.showNumber(pressure)
    }
})
```

## Lesson 12 - Pressure Radio Receiver

This project has the code for **Pressure Radio Receiver**.

## How to use the code

When the micro:bit starts, it shows a **P** for pressure. Keep it connected to the computer by USB to see the data in the data viewer.

- Each reading from the sensor goes to the computer right away.
- The latest reading scrolls on the screen.
- The top-left light blinks each time a reading comes in. If it stops blinking, check the sensor.

## Technical notes

The radio block only saves the reading and sends it to the computer. Scrolling the reading happens in a separate ``||basic:forever||`` loop. Scrolling text takes a few seconds, so if it happened in the radio block, readings could pile up or get lost while the screen was busy.

Click **Done**, then download the code to your micro:bit.
