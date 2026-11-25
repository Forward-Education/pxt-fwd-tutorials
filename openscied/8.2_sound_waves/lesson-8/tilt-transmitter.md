# Lesson 8 - Tilt Sensor Transmitter

```package
radio=radio
microphone=microphone
datalogger=datalogger
```

```template
// Resets settings for new data collection.
function StartingSettings () {
    go = false
    basic.showIcon(IconNames.Happy)
    basic.pause(1000)
    delaycounter = 3
    numberofcycles = 0
    totaltimeintervals = 0
    RecordInitialAngle()
    Countdown()
}
function DisplayFrequency () {
    basic.clearScreen()
    // If no vibrations were detected, the total-time-intervals will be = 0, in which case this displays a question mark, rather than produce a divide by zero math error.  If total-time-intervals are not zero then some vibrations were detected, and a frequency calculation can be displayed.
    if (totaltimeintervals == 0) {
        basic.showString("?")
    } else {
        frequency = numberofcycles / totaltimeintervals
        basic.showNumber(frequency)
    }
}
input.onButtonPressed(Button.A, function () {
    open = false
    StartingSettings()
})
// Shifts the values for the past two angles.
function UpdatePastAngles () {
    _2pastangle = _1pastangle
    _1pastangle = currentangle
}
function RecordInitialAngle () {
    CalculateTiltAngle()
    startangle = currentangle
    _1pastangle = currentangle
    _2pastangle = currentangle
    radio.sendValue("InitDeg", startangle)
}
function ShowRadioGroup () {
    basic.showString("T")
    basic.pause(1000)
    basic.showNumber(myradiogroup)
    basic.pause(1000)
    basic.showIcon(IconNames.Heart)
    go = false
}
// Shows my-radiogroup number on both micro:bits. This allows the user to check if they are on the same radio channel or now
input.onButtonPressed(Button.AB, function () {
    radio.sendString("A+B")
    ShowRadioGroup()
})
// Checks if it is time to collect data for a peak
function CycleChecker () {
    // looks for enough vibration that the angle has changed by at least 3 degrees before it determines that the stick was deformed enough to count as vibrations having started
    if (Math.abs(maxangle - minangle) > 2) {
        if (currentangle >= startangle && _1pastangle < startangle) {
            if (numberofcycles == 0) {
                lastcycletime = currenttime
                starttime = currenttime
                maxstoptime = starttime + 10
            } else if (numberofcycles >= 1) {
                TimeIntervalTracker()
            }
            numberofcycles = numberofcycles + 1
        }
    }
}
// To detect whether buttons A, B, or A+B are pressed onteh other micro:bit
radio.onReceivedString(function (receivedString) {
    if (receivedString == "A") {
        open = false
        StartingSettings()
    } else if (receivedString == "B") {
        open = true
        StartingSettings()
    } else if (receivedString == "A+B") {
        ShowRadioGroup()
    }
})
input.onButtonPressed(Button.B, function () {
    open = true
    StartingSettings()
})
function CalculateTiltAngle () {
    currentroll = input.rotation(Rotation.Roll)
    // shifts the default orientation of the micro:bit (facedown) to register as 90 degrees.
    if (currentroll >= 0) {
        currentangle = currentroll - 90
    } else if (currentroll < 0) {
        currentangle = currentroll + 270
    }
    if (currentangle < minangle) {
        minangle = currentangle
    } else if (currentangle > maxangle) {
        maxangle = currentangle
    }
    sum3angles = currentangle + (_1pastangle + _2pastangle)
    // Calculates the average of the current angle and the last two angles to the tenths place.
    recentangleavg = Math.round(sum3angles * 10 / 3) / 10
}
// Tracks the time for every cycle to complete and adds it to total-elapsed time
function TimeIntervalTracker () {
    interval = currenttime - lastcycletime
    totaltimeintervals = totaltimeintervals + interval
    lastcycletime = currenttime
}
// Runs countdown timer before data collection.
function Countdown () {
    while (delaycounter > 0) {
        radio.sendString(convertToText(delaycounter))
        basic.showNumber(delaycounter)
        basic.pause(1000)
        delaycounter = delaycounter - 1
    }
    radio.sendString("+")
    basic.showString("+")
    basic.pause(500)
    maxstoptime = currenttime + 10
    radio.sendString("go")
    go = true
}
let interval = 0
let recentangleavg = 0
let sum3angles = 0
let currentroll = 0
let maxstoptime = 0
let starttime = 0
let currenttime = 0
let lastcycletime = 0
let minangle = 0
let maxangle = 0
let startangle = 0
let currentangle = 0
let _1pastangle = 0
let _2pastangle = 0
let open = false
let frequency = 0
let totaltimeintervals = 0
let numberofcycles = 0
let delaycounter = 0
let go = false
let myradiogroup = 0
myradiogroup = 1
radio.setGroup(myradiogroup)
basic.showIcon(IconNames.Heart)
basic.forever(function () {
    currenttime = input.runningTime() / 1000
    if (go == true) {
        if (currenttime <= maxstoptime) {
            CalculateTiltAngle()
            CycleChecker()
            UpdatePastAngles()
            if (numberofcycles > 0 || open == true) {
                radio.sendNumber(recentangleavg)
            }
        } else if (currenttime > maxstoptime) {
            radio.sendString("stop")
            DisplayFrequency()
        }
    }
})
```

## Lesson 8 - Tilt Sensor Transmitter

This project has the code for **Tilt Sensor Transmitter**.

Click **Done**, then download the code to your micro:bit.
