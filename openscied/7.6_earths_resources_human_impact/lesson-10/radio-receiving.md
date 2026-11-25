# Lesson 10 - Radio Receiving

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    radio.setGroup(1)
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    radio.setGroup(2)
    basic.clearScreen()
})
radio.onReceivedValue(function (name, value) {
    basic.showNumber(value)
    serial.writeValue(name, value)
})
basic.clearScreen()
basic.showIcon(IconNames.Yes)
```

## Lesson 10 - Radio Receiving

This project has the code for **Radio Receiving**.

Click **Done**, then download the code to your micro:bit.
