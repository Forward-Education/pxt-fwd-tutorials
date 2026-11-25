# Lesson 7 - Buoy Sensor

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

## Lesson 7 - Buoy Sensor

This project has the code for **Buoy Sensor**.

Click **Done**, then download the code to your micro:bit.
