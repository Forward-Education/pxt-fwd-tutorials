# Lesson 10 - Sound Generator 1

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    basic.showString("A")
    v = 250
    for (let index = 0; index < 3; index++) {
        // Maximum volume is 255.
        music.setVolume(v)
        // Hz stands for Hertz, which is the unit of measurement
        // for frequency, specifically cycles per second.
        music.ringTone(262)
        basic.pause(500)
        music.stopAllSounds()
        basic.pause(200)
        v = v / 2
    }
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    music.setVolume(150)
    f = 200
    for (let index = 0; index < 4; index++) {
        music.ringTone(f)
        basic.pause(500)
        music.stopAllSounds()
        basic.pause(200)
        f = f * 2
    }
    basic.clearScreen()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("?")
    music.setVolume(150)
    for (let index = 0; index < 5; index++) {
        // Pick a random integer in this range.
        f = randint(40, 1000)
        music.ringTone(f)
        basic.pause(50)
        music.stopAllSounds()
    }
    basic.clearScreen()
})
let f = 0
let v = 0
music.setBuiltInSpeakerEnabled(true)
basic.showIcon(IconNames.Heart)
```

## Lesson 10 - Sound Generator 1

This project has the code for **Sound Generator 1**.

Click **Done**, then download the code to your micro:bit.
