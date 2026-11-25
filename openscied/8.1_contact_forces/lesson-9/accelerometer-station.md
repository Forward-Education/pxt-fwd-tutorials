# Lesson 9 - Accelerometer Station

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    output = "X"
})
input.onGesture(Gesture.FreeFall, function () {
    basic.showIcon(IconNames.No)
    music.play(music.builtinPlayableSoundEffect(soundExpression.sad), music.PlaybackMode.UntilDone)
})
input.onButtonPressed(Button.AB, function () {
    output = "AB"
    basic.showString(station_name)
})
input.onButtonPressed(Button.B, function () {
    output = "Y"
})
let output = ""
let station_name = ""
station_name = "A"
output = "AB"
basic.showString(station_name)
music.setVolume(255)
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

This project has the code for **Accelerometer Station**.

Click **Done**, then download the code to your micro:bit.
