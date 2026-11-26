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

## How to use the code

When the micro:bit starts, it shows a **P** for pressure. Keep it connected to the computer by USB and open **Show data** to graph the pressure.

- Each reading from the sensor goes to the computer and scrolls on the screen.
- Press **B** to show the radio group number (12).

## Technical notes

The receiver listens on radio group **12**. The sensor micro:bit must use the same group.

When a reading arrives, the ``||radio:on radio received||`` block does two things:

1. ``||serial:serial write value||`` sends the name and the number to the computer. This is what **Show data** graphs.
2. ``||basic:show string||`` scrolls the number on the screen.

The number scrolls inside the radio block, and scrolling takes a few seconds. Readings that arrive during a scroll wait in a queue, so the screen can fall behind the sensor. Each queued reading is still sent to the computer, so the graph in **Show data** gets them all, even if some arrive a little late. Use the graph, not the screen, for your data.

This code is kept the same as the code on the lesson slides.

Click **Done**, then download the code to your micro:bit.
