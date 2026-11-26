# Lesson 9 - Accelerometer Station

```package
radio=radio
```

```template
input.onButtonPressed(Button.A, function () {
    output = "X"
})
input.onButtonPressed(Button.B, function () {
    output = "Y"
})
input.onButtonPressed(Button.AB, function () {
    output = "AB"
    basic.showString(station_name)
})
// When the micro:bit is dropped, it shows an X and plays a sad sound.
input.onGesture(Gesture.FreeFall, function () {
    basic.showIcon(IconNames.No)
    music.play(music.builtinPlayableSoundEffect(soundExpression.sad), music.PlaybackMode.UntilDone)
})
let output = ""
let station_name = ""
station_name = "A"
output = "AB"
basic.showString(station_name)
music.setVolume(255)
// Shows the acceleration on the X or Y axis as a bar graph.
// A full bar is 1023 mg, which is about 1 g (the pull of gravity).
basic.forever(function () {
    if (output == "X") {
        led.plotBarGraph(
        input.acceleration(Dimension.X),
        1023
        )
    } else if (output == "Y") {
        led.plotBarGraph(
        input.acceleration(Dimension.Y),
        1023
        )
    }
})
```

## Lesson 9 - Accelerometer Station

This project has the code for the **Accelerometer Station**.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

- Press **A** to show the acceleration on the **X** axis (left and right) as a bar graph.
- Press **B** to show the acceleration on the **Y** axis (forward and back) as a bar graph.
- Press **A+B** together to show the station letter **A**.
- If the micro:bit falls, it shows an **X** and plays a sad sound.

## Technical notes

The accelerometer measures acceleration in milli-g (mg). 1000 mg is about 1 g, the pull of gravity. A full bar graph is 1023 mg, so a full bar means about 1 g on that axis. Tilting the micro:bit so the axis points straight down fills the bar.

Click **Done**, then download the code to your micro:bit.
