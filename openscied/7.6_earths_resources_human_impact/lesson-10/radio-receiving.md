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

## How to use the code

This micro:bit receives readings by radio from a sensor micro:bit. Keep it connected to the computer by USB and open **Show data** to graph the readings.

- At the start, a check mark shows.
- Press **A** to listen on radio group **1**.
- Press **B** to listen on radio group **2**.

Each reading scrolls on the screen and goes to the computer with the name the sender gave it.

## Technical notes

- Until you press **A** or **B**, the micro:bit uses its default radio group, so press a button first.
- Each reading is sent to the computer as soon as it arrives, then scrolls on the screen.
- Scrolling takes a few seconds. If readings come in faster than that, they wait in a queue and the screen falls behind.
- The sender must use the same group: **A** on the sender matches **A** here.

Click **Done**, then download the code to your micro:bit.
