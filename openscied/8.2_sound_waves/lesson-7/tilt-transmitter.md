# Lesson 7 - Tilt Sensor Transmitter

```package
radio=radio
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
    armed = false
    RecordInitialAngle()
    Countdown()
}
// Shows the frequency in Hz (cycles per second).
// Counting 5 crossings gives 4 full cycles, so the number of
// cycles is one less than the number of crossings.
function DisplayFrequency () {
    basic.clearScreen()
    // With fewer than 2 crossings there is no time to divide by,
    // so a question mark shows instead.
    if (totaltimeintervals == 0) {
        basic.showString("?")
    } else {
        frequency = Math.round((numberofcycles - 1) / totaltimeintervals * 100) / 100
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
// Saves the resting angle and sends it to the receiver.
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
    basic.showNumber(myRadioGroup)
    basic.pause(1000)
    basic.showIcon(IconNames.Heart)
    go = false
}
// Shows the radio group on both micro:bits, so you can check
// they are on the same group.
input.onButtonPressed(Button.AB, function () {
    radio.sendString("A+B")
    ShowRadioGroup()
})
// Counts each upward swing through the resting angle.
// The stick must first swing at least 2 degrees below the resting
// angle (armed), so small jitter at rest is not counted twice.
function CycleChecker () {
    if (currentangle <= startangle - 2) {
        armed = true
    }
    if (armed && currentangle >= startangle) {
        armed = false
        if (numberofcycles == 0) {
            lastcycletime = currenttime
            starttime = currenttime
            maxstoptime = starttime + 10
        } else {
            TimeIntervalTracker()
        }
        numberofcycles = numberofcycles + 1
    }
}
// Lets buttons A, B or A+B on the other micro:bit start this one.
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
    // Shifts the angle so the micro:bit lying face down reads 90 degrees.
    if (currentroll >= 0) {
        currentangle = currentroll - 90
    } else {
        currentangle = currentroll + 270
    }
    sum3angles = currentangle + (_1pastangle + _2pastangle)
    // Average of the current angle and the last two angles, to the tenths place.
    recentangleavg = Math.round(sum3angles * 10 / 3) / 10
}
// Adds the time since the last crossing to the total time.
// The total is the time from the first crossing to the last one.
function TimeIntervalTracker () {
    interval = currenttime - lastcycletime
    totaltimeintervals = totaltimeintervals + interval
    lastcycletime = currenttime
}
// Counts down 3, 2, 1 before data collection. Release the stick at 1.
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
    maxstoptime = input.runningTime() / 1000 + 10
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
let startangle = 0
let currentangle = 0
let _1pastangle = 0
let _2pastangle = 0
let open = false
let frequency = 0
let totaltimeintervals = 0
let numberofcycles = 0
let delaycounter = 0
let armed = false
let go = false
let myRadioGroup = 0
// Set this to your station number. The receiver must use the same number.
myRadioGroup = 1
radio.setGroup(myRadioGroup)
basic.showIcon(IconNames.Heart)
// Collects angle data for 10 seconds after the first crossing
// (or 10 seconds after the countdown if there is no crossing),
// then shows the frequency.
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
        } else {
            radio.sendString("stop")
            DisplayFrequency()
        }
    }
})
```

## Lesson 7 - Tilt Sensor Transmitter

This project has the code for **Tilt Sensor Transmitter**. It goes on the micro:bit taped to the vibrating stick.

## How to use the code

- Set ``myRadioGroup`` to your station number before you download. The receiver micro:bit must use the same number.
- Press **A** for a closed run or **B** for an open run. You can also press the buttons on the receiver.
- A 3, 2, 1 countdown shows. Release the stick at **1**.
- The micro:bit sends angle data by radio for 10 seconds, then scrolls the frequency in Hz (cycles per second).
- Press **A+B** together to show the radio group on both micro:bits.

If a **?** shows, the stick did not vibrate enough to measure. Try again.

## Technical notes

- ``CycleChecker`` counts each time the stick swings up through its resting angle. The stick must first swing at least 2 degrees below the resting angle, so small jitter at rest is not counted twice.
- ``DisplayFrequency`` divides the number of full cycles by the time between the first and last crossing. Five crossings make four full cycles, so it uses (crossings - 1) / time.
- With this method a long stick reads about 1.4 Hz and a short stick about 2.05 Hz, which matches the graphs.

Click **Done**, then download the code to your micro:bit.
