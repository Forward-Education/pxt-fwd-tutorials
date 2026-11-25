# Lesson 12 - Pressure Radio Receiver

```package
radio=radio
microphone=microphone
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

## Lesson 12 - Pressure Radio Receiver @showdialog

This project already has the code for **Pressure Radio Receiver**.

Click **Done**, then download the code to your micro:bit.
