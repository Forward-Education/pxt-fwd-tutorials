# Lesson 9 - Slider Station

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// A: bar graph only, no sound.
input.onButtonPressed(Button.A, function () {
    output = "A"
    volume = 0
    music.setVolume(volume)
    music.stopAllSounds()
})
// B: the slider sets the volume of the tone.
input.onButtonPressed(Button.B, function () {
    output = "B"
    basic.clearScreen()
})
// Logo: plays the tone at the highest volume (255).
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    output = "logo"
    basic.clearScreen()
    volume = 255
    music.setVolume(volume)
    music.ringTone(262)
})
input.onButtonPressed(Button.AB, function () {
    output = "station"
    volume = 0
    music.setVolume(volume)
    music.stopAllSounds()
    basic.showString(station_name)
})
let position = 0
let volume = 0
let output = ""
let station_name = ""
opensciedModules.initializeLcd()
music.setBuiltInSpeakerEnabled(true)
station_name = "S"
output = "station"
basic.showString(station_name)
// Reads the slider and shows the position and the volume on the LCD.
basic.forever(function () {
    position = Math.round(opensciedModules.slider1.position())
    if (output == "A") {
        led.plotBarGraph(
        position,
        100
        )
    } else if (output == "B") {
        // Changes 0 to 100% into a volume from 0 to 255.
        volume = Math.round(Math.map(position, 0, 100, 0, 255))
        music.setVolume(volume)
        // 262 Hz is Middle C.
        music.ringTone(262)
    }
    opensciedModules.lcd1.printQuadrantString("Slider %", 1)
    opensciedModules.lcd1.printQuadrantNumber(position, 2)
    opensciedModules.lcd1.printQuadrantString("Volume", 3)
    opensciedModules.lcd1.printQuadrantNumber(volume, 4)
})
```

## Lesson 9 - Slider Station

This project has the code for the **Slider Station**.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

- Press **A** to show the slider position as a bar graph. There is no sound.
- Press **B** to play Middle C. Move the slider to change the volume.
- Touch the **logo** to play Middle C at the highest volume (255).
- Press **A+B** together to stop the sound and show the station letter **S**.

The LCD shows the slider position (%) on line 1 and the volume (0 to 255) on line 2.

## Technical notes

The slider reads from 0 to 100%, but the volume goes from 0 to 255. The ``||math:map||`` block changes the slider reading into a volume, so the top of the slider is the full volume, 255. This is louder than the original version of this code.

Click **Done**, then download the code to your micro:bit.
