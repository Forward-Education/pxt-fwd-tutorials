# Lesson 7 - Tsunameter (Slides Version)

```package
radio=radio
microphone=microphone
```

```template
radio.onReceivedNumber(function (receivedNumber) {
    if (status == "W") {
        BUOYheight = receivedNumber
    }
})
input.onButtonPressed(Button.A, function () {
    initialBUOYinput = BUOYinput
    basic.showString("-")
    music.play(music.tonePlayable(262, music.beat(BeatFraction.Sixteenth)), music.PlaybackMode.UntilDone)
    basic.clearScreen()
})
function DisplayNewWarning () {
    if (maxBUOYheight > 0 && maxBUOYheight >= 0) {
        basic.showString("!")
    }
}
input.onButtonPressed(Button.B, function () {
    if (status == "W") {
        status = "L"
    } else if (status == "L") {
        status = "W"
    }
    basic.showString(status)
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    DisplayNewWarning()
})
let maxBUOYheight = 0
let BUOYinput = 0
let initialBUOYinput = 0
let BUOYheight = 0
let status = ""
radio.setGroup(1)
status = "L"
basic.showString(status)
loops.everyInterval(2000, function () {
    if (status == "W") {
        DisplayNewWarning()
    }
    basic.clearScreen()
    maxBUOYheight = 0
})
basic.forever(function () {
    if (status == "L") {
        BUOYinput = Math.round(1000 * input.magneticForce(Dimension.Strength) ** 0.33)
        BUOYheight = BUOYinput - initialBUOYinput
    }
    if (BUOYheight > maxBUOYheight) {
        maxBUOYheight = BUOYheight
    }
    serial.writeValue("Height", BUOYheight)
})
```

## Lesson 7 - Tsunameter (Slides Version)

This project has the code for **Tsunameter (Slides Version)**.

Click **Done**, then download the code to your micro:bit.
