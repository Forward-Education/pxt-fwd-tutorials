# Lesson 6 - Station 3, Sensor 2

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    basic.showIcon(IconNames.Yes)
    basic.pause(500)
    basic.clearScreen()
    sending = true
})
// Shows which sensor this micro:bit is.
input.onButtonPressed(Button.AB, function () {
    basic.showString("H" + sensornumber)
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    sending = false
    basic.showIcon(IconNames.Happy)
})
let abshumidity = 0
let sending = false
let sensornumber = 0
let radiogroupnumber = 0
sending = false
radiogroupnumber = 3
sensornumber = 2
radio.setGroup(radiogroupnumber)
basic.showString("H" + sensornumber)
// Reads the sensor and scrolls the value on the screen.
// Scrolling text takes a few seconds, so it gets its own loop
// to keep it from slowing down the radio sending.
basic.forever(function () {
    abshumidity = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
    if (sending) {
        basic.showString("" + abshumidity)
        basic.clearScreen()
    }
})
// Sends one reading every second, so the receiver gets evenly spaced data.
loops.everyInterval(1000, function () {
    if (sending) {
        radio.sendValue("sensor " + sensornumber, abshumidity)
    }
})
```

## Lesson 6 - Station 3, Sensor 2

This project has the code for **Station 3, Sensor 2**.

## How to use the code

When the micro:bit starts, it shows **H** for humidity followed by the sensor number, such as **H1**.

- Press **A** to start. A check mark shows, then the micro:bit sends a humidity reading to the receiver every second. The reading also scrolls on the screen.
- Press **B** to stop sending. A happy face shows.
- Press **A+B** together to show **H** and the sensor number again, so you can tell the two sensors apart.

## Technical notes

The code uses two loops that run at the same time:

- The ``||basic:forever||`` loop reads the humidity sensor and scrolls the value on the screen.
- The ``||loops:every 1000 ms||`` loop sends one reading by radio every second.

Scrolling text on the micro:bit takes a few seconds. If both jobs were in the same loop, a reading would only be sent after each scroll finished. Keeping them in separate loops means the receiver gets one reading every second, no matter what the screen is doing.

Click **Done**, then download the code to your micro:bit.
