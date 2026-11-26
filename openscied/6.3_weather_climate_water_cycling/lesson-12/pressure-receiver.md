# Lesson 12 - Pressure Radio Receiver

```package
radio=radio
```

```template
input.onButtonPressed(Button.B, function () {
    basic.showString("" + (radiogroupnumber))
})
radio.onReceivedValue(function (name, value) {
    serial.writeValue(name, value)
    basic.showString("" + (value))
})
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
```

## Lesson 12 - Pressure Radio Receiver

This project has the code for **Pressure Radio Receiver**. It matches the code students read on the lesson slides.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

When the micro:bit starts, it shows a **P** for pressure. Keep it connected to the computer by USB and open **Show data** to graph the pressure.

- Each reading from the sensor goes to the computer and scrolls on the screen.
- Press **B** to show the radio group number (12).

## Technical notes

The receiver listens on radio group **12**. The sensor micro:bit must use the same group.

Click **Done**, then download the code to your micro:bit.
