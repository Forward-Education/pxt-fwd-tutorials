# Lesson 5 - Teacher Data Hub

```package
radio=radio
microphone=microphone
```

```template
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 1) {
        _1stsensorcomplete = true
    } else if (receivedNumber == 2) {
        _2ndsensorcomplete = true
    }
    if (_1stsensorcomplete && _2ndsensorcomplete) {
        basic.showIcon(IconNames.Yes)
    }
})
input.onButtonPressed(Button.A, function () {
    basic.showString("A")
    radio.sendString("A")
    status = "A"
    ResetComplete()
})
input.onButtonPressed(Button.AB, function () {
    status = "A+B"
    basic.showIcon(IconNames.No)
    radio.sendString("X")
    ResetComplete()
})
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    radio.sendString("B")
    status = "B"
    ResetComplete()
})
radio.onReceivedValue(function (name, value) {
    label = "Sensor " + name
    if (name == "0") {
        sensor0value = value
    } else if (name == "1") {
        sensor1value = value
    }
    if (status == "A") {
        serial.writeValue(label, value)
    } else if (status == "B") {
        serial.writeNumbers([sensor0value, sensor1value])
    }
})
function ResetComplete () {
    _1stsensorcomplete = false
    _2ndsensorcomplete = false
    sensor0value = 0
    sensor1value = 0
}
let sensor1value = 0
let sensor0value = 0
let label = ""
let _2ndsensorcomplete = false
let _1stsensorcomplete = false
let status = ""
radio.setGroup(1)
basic.showString("+")
ResetComplete()
let statusAB = false
status = "-"
```

## Lesson 5 - Teacher Data Hub

This project has the code for **Teacher Data Hub**.

## How to use the code

This micro:bit controls the buoy sensors and collects their data. Keep it connected to the computer by USB and open **Show data**.

- At the start, it shows **+**. Nothing is graphed yet.
- Press **A** to start mode A. It sends **A** to the sensors, and each sensor's reading is graphed as its own line (**Sensor 0**, **Sensor 1**).
- Press **B** to start mode B. It sends **B** to the sensors. The sensors stop on their own after a wave passes, and the hub graphs both sensors together.
- Press **A+B** to stop. It sends **X** to the sensors, shows an X, and stops graphing.

A check mark shows when the hub has heard that both sensors have finished.

## Technical notes

- All micro:bits use radio group **1**.
- The sensors send their readings as radio values named **0** and **1** (the sensor ID).
- In mode A, each reading is sent to the computer as soon as it arrives, with the label **Sensor 0** or **Sensor 1**.
- In mode B, the hub keeps the latest value from each sensor. Each time either sensor sends, the hub sends both values as one row of two numbers. This keeps the two sensors lined up in time.
- Pressing **A**, **B** or **A+B** resets both values to 0 and clears the "finished" flags.
- When a sensor finishes, it sends its ID as a radio number. The hub shows the check mark only after it gets both **1** and **2**.

Click **Done**, then download the code to your micro:bit.
