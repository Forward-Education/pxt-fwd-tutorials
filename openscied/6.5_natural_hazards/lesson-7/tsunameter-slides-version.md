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

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

This micro:bit is a tsunameter. It uses the compass (magnetometer) to measure how high a magnet on the water rises. Keep it connected to the computer by USB and open **Show data** to graph the height.

- At the start, it shows **L** (local mode).
- With the water still, press **A** to set the zero level. It shows **-** and plays a short tone.
- Press **B** to switch between **L** (local) and **W** (warning) mode.
- In **W** mode, a **!** shows every 2 seconds if the height is above the zero level. The height is only measured in **L** mode (see the technical notes).
- Touch the logo to check for a warning by hand (micro:bit V2 only).

## Technical notes

- The forever loop reads the magnetic strength, takes the cube root and multiplies by 1000. It subtracts the zero level set with **A** to get the height.
- The height is only updated in **L** mode. In **W** mode the height stays at the last local value.
- The forever loop sends the height to the computer as **Height** as fast as it can, in both modes.
- The highest height is kept and checked every 2 seconds, then reset to 0. Any height above 0 counts as a warning.
- The radio uses group **1**. In **W** mode, a radio number sets the height. This is the version on the lesson slides.

Click **Done**, then download the code to your micro:bit.
