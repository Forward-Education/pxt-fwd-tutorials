# Lesson 6 - Humidity Sender

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Shows the sensor number, then starts sending.
input.onButtonPressed(Button.A, function () {
    basic.showString("H" + sensornumber)
    basic.clearScreen()
    sending = true
})
// Stops sending.
input.onButtonPressed(Button.B, function () {
    sending = false
    basic.showIcon(IconNames.Happy)
})
let abshumidity = 0
let sending = false
let sensornumber = 0
let stationnumber = 0
// Set these two numbers to match the sticky note on this micro:bit.
stationnumber = 3
sensornumber = 1
sending = false
// The station number is also the radio group, so each station
// only talks to its own receiver.
radio.setGroup(stationnumber)
basic.showNumber(stationnumber)
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

## Lesson 6 - Humidity Sender

This tutorial sets up the **6 humidity senders** for Stations 3, 4 and 5. Each station has two senders that send absolute humidity (g/m3) by radio to the station's receiver.

You will use the same code for all 6 micro:bits and only change two numbers.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Setup

Put a BME280 sensor inside each humidity hood, with the cable through the cap to the breakout board.

## Station and sensor numbers

At the top of ``||basic:on start||`` are two numbers:

- ``stationnumber`` is the station (3, 4 or 5). It is also the radio group, so it must match the station's receiver.
- ``sensornumber`` is 1 or 2. It tells the receiver which graph the reading goes on.

## Buttons

- Press **A** to show **H** and the sensor number, then start sending one reading every second. The reading also scrolls on the screen.
- Press **B** to stop sending. A happy face shows.

## Download to each micro:bit

Set the two numbers to match the sticky note, then download. Repeat for all 6.

- ``stationnumber``: the station on the sticky note (3, 4 or 5).
- ``sensornumber``: the sensor on the sticky note (1 or 2).

For example, the sticky note **Station 4, Sensor 2** means ``stationnumber`` 4 and ``sensornumber`` 2.

**Check:** when it starts, the micro:bit shows the station number. Pressing **A** shows **H1** or **H2**.

## Technical notes

The code uses two loops that run at the same time:

- The ``||basic:forever||`` loop reads the humidity sensor and scrolls the value on the screen.
- The ``||loops:every 1000 ms||`` loop sends one reading by radio every second.

Scrolling text takes a few seconds. Keeping the two jobs in separate loops means the receiver gets one reading every second, no matter what the screen is doing.

Click **Done** when all 6 are downloaded.
