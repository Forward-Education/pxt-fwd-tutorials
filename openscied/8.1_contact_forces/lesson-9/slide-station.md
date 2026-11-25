# Lesson 9 - Slider Station

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
input.onButtonPressed(Button.A, function () {
    output = "A"
    music.setVolume(0)
})
input.onButtonPressed(Button.AB, function () {
    output = "station"
    basic.showString(station_name)
    music.setVolume(0)
})
input.onButtonPressed(Button.B, function () {
    output = "B"
    basic.clearScreen()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    music.setVolume(127)
    music.ringTone(262)
})
let output = ""
let station_name = ""
music.setBuiltInSpeakerEnabled(true)
station_name = "S"
output = "station"
basic.showString(station_name)
basic.forever(function () {
    if (output == "A") {
        led.plotBarGraph(
        opensciedModules.slider1.position(),
        98
        )
    }
    if (output == "B") {
        music.setVolume(opensciedModules.slider1.position())
        music.ringTone(262)
        basic.clearScreen()
    }
})
```

## Lesson 9 - Slider Station

This project has the code for **Slider Station**.

Click **Done**, then download the code to your micro:bit.
