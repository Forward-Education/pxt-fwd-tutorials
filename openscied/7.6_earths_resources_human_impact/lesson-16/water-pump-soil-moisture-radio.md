# Lesson 16 - Soil Moisture Radio Sender

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Starts sending again.
input.onButtonPressed(Button.A, function () {
    running = true
    basic.clearScreen()
})
// Stops sending and tells the receiver to turn the pump off.
input.onButtonPressed(Button.AB, function () {
    running = false
    radio.sendValue("pump", 0)
    basic.showIcon(IconNames.Yes)
})
let input2 = 0
let running = false
let stationNumber = 0
// Set this to your station number (1 to 7). It is also the radio group,
// so it must match the receiver.
stationNumber = 1
radio.setGroup(stationNumber)
basic.showNumber(stationNumber)
running = true
// Reads the soil once, shows a face and tells the receiver
// whether to run the pump: 1 = dry, run the pump. 0 = pump off.
basic.forever(function () {
    input2 = opensciedModules.moisture1.moistureLevel()
    serial.writeValue("soil moisture", input2)
    if (running) {
        if (input2 >= 50) {
            basic.showIcon(IconNames.Happy)
            radio.sendValue("pump", 0)
        } else if (input2 >= 20) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . # # # .
                . . . . .
                `)
            radio.sendValue("pump", 0)
        } else {
            basic.showIcon(IconNames.Sad)
            radio.sendValue("pump", 1)
        }
    }
    basic.pause(500)
})
```

## Lesson 16 - Soil Moisture Radio Sender

This system uses **two micro:bits**. This one, the **sender**, reads the soil and sends a message by radio. The **receiver** runs the pump.

Save a copy of your project before you start.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Set the station number

Find ``stationNumber`` in ``||basic:on start||``.

```blocks
let stationNumber = 0
// @highlight
stationNumber = 1
radio.setGroup(stationNumber)
basic.showNumber(stationNumber)
```

Change it to your station number (1 to 7). It is also the radio group, so each station only talks to its own pump. Use the same number on the receiver.

## Read the message

Find the ``||radio:radio send value||`` blocks.

```blocks
let input2 = 0
if (input2 >= 50) {
    basic.showIcon(IconNames.Happy)
    // @highlight
    radio.sendValue("pump", 0)
} else if (input2 >= 20) {
    basic.showLeds(`
        . . . . .
        . # . # .
        . . . . .
        . # # # .
        . . . . .
        `)
    // @highlight
    radio.sendValue("pump", 0)
} else {
    basic.showIcon(IconNames.Sad)
    // @highlight
    radio.sendValue("pump", 1)
}
```

The sender sends **"pump" = 1** when the soil is dry (under 20%) and **"pump" = 0** otherwise. It sends a message every 0.5 seconds.

Press **A+B** to stop sending (the pump turns off), and **A** to start again.

## Technical notes

- The radio group is the station number, so stations 1 to 7 do not control each other's pumps.
- While running, the sender sends a **"pump"** message about every 0.5 seconds. The receiver runs the pump for 0.5 seconds on each **1**, so the pump keeps running only while new **1** messages arrive.
- **A+B** sends one **"pump" = 0** and stops sending. If that one message is lost, the pump still stops after its last 0.5 second burst.
- The soil reading goes to the computer by USB every time through the loop, even after **A+B**. Open **Show data** to graph it.
- The sender does not run a pump itself.

## Download

Download this code to the sender micro:bit. It shows your station number when it starts. Then set up the receiver with the **Lesson 16 - Water Pump Receiver** code.

Click **Done** when the sender is downloaded.
