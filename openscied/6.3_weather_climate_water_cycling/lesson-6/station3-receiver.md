# Lesson 6 - Station 3 Receiver

```package
radio=radio
microphone=microphone
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
let radiogroupnumber = 0
receiving = false
radiogroupnumber = 3
column1 = "Sensor 1 humidity (g/m3)"
column2 = "Sensor 2 humidity (g/m3)"
datalogger.mirrorToSerial(true)
radio.setGroup(radiogroupnumber)
basic.showString("R")
// Saves one row with both readings every second.
// It waits until both sensors have sent a reading, so every row is complete.
loops.everyInterval(1000, function () {
    if (receiving && got1 && got2) {
        datalogger.log(datalogger.createCV(column1, sensor1), datalogger.createCV(column2, sensor2))
    }
})
```

## Lesson 6 - Station 3 Receiver

This project has the code for **Station 3 Receiver**.

## How to use the code

When the micro:bit starts, it shows **R** for receiver. Start both sensors first, then the receiver.

- Press **A** to start. A check mark shows, the old data log is erased, and a plus sign shows while the micro:bit receives. Once both sensors have sent a reading, it saves one row with both readings every second.
- Press **B** to stop saving. A happy face shows.

While the micro:bit receives, the top-left light blinks for sensor 1 and the top-right light blinks for sensor 2. If a corner does not blink, check that sensor.

Pressing **A** again erases the saved data, so save your data before you start a new run.

## Technical notes

The two sensors send their readings at slightly different times. The receiver remembers the latest reading from each sensor, and the ``||loops:every 1000 ms||`` loop saves both together as one row. That way each row in the data log has a Sensor 1 reading and a Sensor 2 reading taken at about the same time.

Click **Done**, then download the code to your micro:bit.
