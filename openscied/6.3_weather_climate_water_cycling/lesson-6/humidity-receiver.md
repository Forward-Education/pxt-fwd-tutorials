# Lesson 6 - Humidity Receiver

```package
radio=radio
datalogger=datalogger
```

```template
input.onButtonPressed(Button.A, function () {
    basic.showIcon(IconNames.Yes)
    basic.pause(500)
    datalogger.deleteLog(datalogger.DeleteType.Full)
    datalogger.setColumnTitles(column1, column2)
    got1 = false
    got2 = false
    receiving = true
    basic.showLeds(`
        . . # . .
        . . # . .
        # # # # #
        . . # . .
        . . # . .
        `)
})
input.onButtonPressed(Button.B, function () {
    receiving = false
    basic.showIcon(IconNames.Happy)
})
// Remembers the latest reading from each sensor.
// While receiving, a corner light blinks for each reading:
// top-left for sensor 1, top-right for sensor 2.
radio.onReceivedValue(function (name, value) {
    if (name == "sensor 1") {
        sensor1 = value
        got1 = true
        if (receiving) {
            led.toggle(0, 0)
        }
    } else if (name == "sensor 2") {
        sensor2 = value
        got2 = true
        if (receiving) {
            led.toggle(4, 0)
        }
    }
})
let sensor2 = 0
let sensor1 = 0
let got2 = false
let got1 = false
let column2 = ""
let column1 = ""
let receiving = false
let stationnumber = 0
// Set this to the station number (3, 4 or 5). It must match the station's senders.
stationnumber = 3
receiving = false
column1 = "Sensor 1 humidity (g/m3)"
column2 = "Sensor 2 humidity (g/m3)"
datalogger.mirrorToSerial(true)
radio.setGroup(stationnumber)
basic.showNumber(stationnumber)
// Saves one row with both readings every second.
// It waits until both sensors have sent a reading, so every row is complete.
loops.everyInterval(1000, function () {
    if (receiving && got1 && got2) {
        datalogger.log(datalogger.createCV(column1, sensor1), datalogger.createCV(column2, sensor2))
    }
})
```

## Lesson 6 - Humidity Receiver @showdialog

This tutorial sets up the **3 receivers**, one for each of Stations 3, 4 and 5. Each receiver is plugged into a computer and saves both sensors' readings, so you can graph them in **Show data**.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Station number

At the top of ``||basic:on start||`` is ``stationnumber``. It is the radio group, so it must match the two senders at that station.

## How to use the code

When the micro:bit starts, it shows the station number. Start both senders first, then the receiver.

- Press **A** to start. A check mark shows, the old data log is erased, and a plus sign shows while the micro:bit receives. Once both sensors have sent a reading, it saves one row with both readings every second.
- Press **B** to stop saving. A happy face shows.

While the micro:bit receives, the top-left light blinks for sensor 1 and the top-right light blinks for sensor 2. If a corner does not blink, check that sensor.

Pressing **A** again erases the saved data, so save your data before you start a new run.

## Download to each receiver

Set ``stationnumber`` and download. Repeat for each station.

For example, the receiver for Station 4 uses ``stationnumber`` 4.

**Check:** when it starts, the micro:bit shows the station number. Pressing **A** shows a plus sign, and **Show data** shows two graphs.

## Technical notes

The two sensors send their readings at slightly different times. The receiver remembers the latest reading from each sensor, and the ``||loops:every 1000 ms||`` loop saves both together as one row. That way each row in the data log has a Sensor 1 reading and a Sensor 2 reading taken at about the same time.

Click **Done** when all 3 are downloaded.
