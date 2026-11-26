# Lesson 5 - Buoy Sensor

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
function checkForExtremes () {
    if (!(wavecomplete)) {
        if (nowposition > maxposition) {
            maxposition = nowposition
        }
        if (nowposition < minposition) {
            minposition = nowposition
        }
        if (nowposition > 800) {
            increst = true
        }
        if (increst) {
            if (nowposition <= 0) {
                completedcrest = true
                increst = false
            }
        }
        if (nowposition < -500) {
            intrough = true
        }
        if (intrough) {
            if (nowposition >= 0) {
                completedtrough = true
                intrough = false
            }
        }
    }
}
function CalculateMagnetPosition () {
    mforceiny = input.magneticForce(Dimension.Y)
    if (mforceiny < 0) {
        mdistance = Math.round(-1000 * Math.sqrt(Math.abs(mforceiny)))
    } else if (mforceiny > 0) {
        mdistance = Math.round(1000 * Math.sqrt(mforceiny))
    } else {
        mdistance = 0
    }
}
function ShowSensor () {
    music.ringTone(262)
    basic.showNumber(sensorid)
    music.stopAllSounds()
}
radio.onReceivedString(function (receivedString) {
    status = receivedString
    if (status == "A") {
        basic.showString("A")
        ResetValues()
    } else if (status == "B") {
        basic.showString("B")
        ResetValues()
    } else if (status == "X") {
        basic.showIcon(IconNames.No)
        music.play(music.tonePlayable(165, music.beat(BeatFraction.Quarter)), music.PlaybackMode.UntilDone)
        basic.clearScreen()
    }
})
function ResetValues () {
    samplecounter = 0
    nowposition = 0
    minposition = 0
    maxposition = 0
    increst = false
    intrough = false
    completedcrest = false
    completedtrough = false
    music.play(music.tonePlayable(262, music.beat(BeatFraction.Quarter)), music.PlaybackMode.UntilDone)
    basic.showNumber(sensorid)
    CalculateMagnetPosition()
    initdistance = mdistance
    wavecomplete = false
    senddata = true
    music.stopAllSounds()
}
function EndDataCollection () {
    if (samplecounter >= 5) {
        music.ringTone(659)
        basic.showIcon(IconNames.Yes)
        senddata = false
        radio.sendNumber(sensorid)
    }
    music.stopAllSounds()
}
function checkDataToSend () {
    if (status == "B") {
        checkForExtremes()
        if (completedcrest) {
            samplecounter += 1
            EndDataCollection()
        }
    }
    if (senddata) {
        radio.sendValue(idlabel, nowposition)
    }
}
let senddata = false
let initdistance = 0
let samplecounter = 0
let status = ""
let mdistance = 0
let mforceiny = 0
let completedtrough = false
let intrough = false
let completedcrest = false
let increst = false
let minposition = 0
let maxposition = 0
let nowposition = 0
let wavecomplete = false
let idlabel = ""
let sensorid = 0
sensorid = 0
idlabel = convertToText(sensorid)
radio.setGroup(1)
ResetValues()
basic.pause(500)
basic.clearScreen()
basic.forever(function () {
    if (senddata) {
        CalculateMagnetPosition()
        nowposition = mdistance - initdistance
        checkDataToSend()
    }
})
```

## Lesson 5 - Buoy Sensor

This project has the code for **Buoy Sensor**.

## How to use the code

This micro:bit is a buoy sensor. It uses the compass (magnetometer) to measure how far a magnet on the moving water is from the micro:bit. The teacher data hub controls it by radio.

1. Before you download, set ``sensorid`` in ``||basic:on start||``. Use **0** for the first sensor and **1** for the second.
2. At the start, the sensor plays a tone, shows its ID and saves its starting position. It then starts sending readings.
3. When the hub sends **A**, the sensor shows **A**, plays a tone, shows its ID, saves a new starting position and sends readings until the hub stops it.
4. When the hub sends **B**, the sensor does the same, but stops on its own after a wave crest passes. It then plays a tone, shows a check mark and tells the hub it has finished.
5. When the hub sends **X**, the sensor shows an X and plays a low tone.

Keep the water and magnet still when a mode starts, because that is the starting position.

## Technical notes

- All micro:bits use radio group **1**.
- The sensor reads the magnetic force on the Y axis. It takes the square root and multiplies by 1000, keeping the sign, so the number changes more evenly as the magnet moves. It then subtracts the starting value, so 0 means "at rest".
- The forever loop sends a reading as fast as it can, as a radio value named after ``sensorid``.
- In mode B, a crest starts when the reading goes above 800 and ends when it drops back to 0 or below. The sensor then stops sending and sends its ``sensorid`` as a radio number.
- The code also tracks the trough (below -500) and the highest and lowest values, but these are not used to stop or send data.

Click **Done**, then download the code to your micro:bit.
