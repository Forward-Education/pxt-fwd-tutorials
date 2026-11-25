# Lesson 5 - Student Data Client

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

Click **Done**, then download the code to your micro:bit.
