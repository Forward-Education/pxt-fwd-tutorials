# Lesson 5 - Student Data Client

```package
radio=radio
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
        music.play(music.tonePlayable(659, music.beat(BeatFraction.Eighth)), music.PlaybackMode.UntilDone)
    }
})
radio.onReceivedString(function (receivedString) {
    if (receivedString == "X") {
        basic.showIcon(IconNames.No)
        music.play(music.tonePlayable(165, music.beat(BeatFraction.Eighth)), music.PlaybackMode.UntilDone)
        Reset()
    } else if (receivedString == "A") {
        basic.showString("A")
        music.play(music.tonePlayable(659, music.beat(BeatFraction.Eighth)), music.PlaybackMode.UntilDone)
        Reset()
    } else if (receivedString == "B") {
        basic.showString("B")
        music.play(music.tonePlayable(659, music.beat(BeatFraction.Eighth)), music.PlaybackMode.UntilDone)
        Reset()
    }
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
function Reset () {
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
Reset()
let statusAB = false
status = "-"
```

## Lesson 5 - Student Data Client

This project has the code for **Student Data Client**.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

This micro:bit listens to the buoy sensors and the teacher data hub. It does not have any button controls. Keep it connected to the computer by USB and open **Show data**.

- At the start, it shows **+**.
- When the hub sends **A** or **B**, it shows that letter and plays a tone.
- When the hub sends **X**, it shows an X and plays a low tone.
- When both sensors report that they have finished, it shows a check mark and plays a tone.

## Technical notes

- All micro:bits use radio group **1**.
- The code is a copy of the teacher data hub without the buttons. It keeps the latest value from Sensor 0 and Sensor 1.
- The code only graphs readings when its ``status`` variable is **A** or **B**. The radio letters from the hub do not change ``status``, so it stays **-** and nothing is sent to **Show data**. See the teacher data hub for the graph.
- The check mark needs finish messages **1** and **2** from the sensors.

Click **Done**, then download the code to your micro:bit.
