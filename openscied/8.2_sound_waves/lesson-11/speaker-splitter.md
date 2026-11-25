# Lesson 11 - Speaker Splitter

```package
radio=radio
microphone=microphone
```

```template
input.onButtonPressed(Button.A, function () {
    music.setBuiltInSpeakerEnabled(true)
    pins.setAudioPinEnabled(false)
    basic.showString("A")
    v = 255
    for (let index = 0; index < 3; index++) {
        // Maximum volume is 500.
        music.setVolume(v)
        // Hz stands for Hertz, which is the unit of measurement
        // for frequency, specifically cycles per second.
        music.ringTone(100)
        basic.pause(200)
        music.stopAllSounds()
        basic.pause(500)
        v = v / 2
    }
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    music.setBuiltInSpeakerEnabled(true)
    pins.setAudioPinEnabled(false)
    basic.showString("B")
    music.setVolume(255)
    f = 40
    for (let index = 0; index < 8; index++) {
        music.ringTone(f)
        basic.pause(200)
        music.stopAllSounds()
        basic.pause(100)
        f = f * 2
    }
    basic.clearScreen()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    music.setBuiltInSpeakerEnabled(false)
    pins.setAudioPinEnabled(true)
    basic.showString("?")
    music.setVolume(255)
    for (let index = 0; index < 6; index++) {
        // Pick a random integer in this range.
        f = randint(40, 1000)
        music.ringTone(f)
        basic.pause(randint(50, 500))
        music.stopAllSounds()
    }
    basic.clearScreen()
})
let f = 0
let v = 0
basic.showIcon(IconNames.Heart)
```

## Lesson 11 - Speaker Splitter

This project has the code for **Speaker Splitter**.

Click **Done**, then download the code to your micro:bit.
