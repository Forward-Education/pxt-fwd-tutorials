# Lesson 11 - Speaker Splitter

```package
radio=radio
```

```template
// Plays sound on the micro:bit's own speaker.
function useBuiltInSpeaker () {
    music.setBuiltInSpeakerEnabled(true)
    pins.setAudioPinEnabled(false)
}
// Plays sound on the Speaker:bit speaker.
function useExternalSpeaker () {
    music.setBuiltInSpeakerEnabled(false)
    pins.setAudioPinEnabled(true)
}
// Plays a low pitch 3 times, getting quieter each time.
input.onButtonPressed(Button.A, function () {
    useBuiltInSpeaker()
    basic.showString("A")
    v = 255
    for (let index = 0; index < 3; index++) {
        // Maximum volume is 255.
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
// Plays 8 pitches, doubling the frequency each time.
input.onButtonPressed(Button.B, function () {
    useBuiltInSpeaker()
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
// Plays 6 random pitches on the Speaker:bit.
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    useExternalSpeaker()
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

## Lesson 11 - Speaker Splitter @showdialog

A speaker system can split sound so that low pitches go to one speaker and high pitches go to another. In this tutorial you will play sound on two speakers, and then change the code so each pitch goes to the right speaker.

**Wiring:** slide the micro:bit into the Speaker:bit edge connector, with the micro:bit screen facing out. The Speaker:bit plays the sound the micro:bit sends to its audio pin. The micro:bit's own speaker is the second speaker.

The starter code is already in the workspace. Save a copy of your project before you start.

## Use the code

Download the code to your micro:bit.

- Press **A** to play a low pitch 3 times on the micro:bit speaker, getting quieter each time.
- Press **B** to play 8 pitches from low to high on the micro:bit speaker.
- Touch the **logo** to play 6 random pitches on the Speaker:bit.

## Read the code

Find the ``useBuiltInSpeaker`` and ``useExternalSpeaker`` functions.

```blocks
// @highlight
function useBuiltInSpeaker () {
    music.setBuiltInSpeakerEnabled(true)
    pins.setAudioPinEnabled(false)
}
// @highlight
function useExternalSpeaker () {
    music.setBuiltInSpeakerEnabled(false)
    pins.setAudioPinEnabled(true)
}
```

Each function turns one speaker on and the other one off. Each button block calls one of them before it plays any sound.

## Make a crossover

Make low pitches play on the Speaker:bit and higher pitches play on the micro:bit speaker.

1. Make a new function called ``routeByFrequency``.
2. In it, add an ``||logic:if else||`` block: if ``f`` is less than **200**, call ``useExternalSpeaker``, else call ``useBuiltInSpeaker``.
3. In the **B** block and the **logo** block, call ``routeByFrequency`` just before each ``||music:ring tone||`` block. Remove the speaker call at the top of those blocks.

Open the hint to see one answer.

```blocks
let f = 0
function useBuiltInSpeaker () {
    music.setBuiltInSpeakerEnabled(true)
    pins.setAudioPinEnabled(false)
}
function useExternalSpeaker () {
    music.setBuiltInSpeakerEnabled(false)
    pins.setAudioPinEnabled(true)
}
// Low pitches go to the Speaker:bit, higher pitches to the micro:bit.
function routeByFrequency () {
    if (f < 200) {
        useExternalSpeaker()
    } else {
        useBuiltInSpeaker()
    }
}
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    music.setVolume(255)
    f = 40
    for (let index = 0; index < 8; index++) {
        routeByFrequency()
        music.ringTone(f)
        basic.pause(200)
        music.stopAllSounds()
        basic.pause(100)
        f = f * 2
    }
    basic.clearScreen()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    basic.showString("?")
    music.setVolume(255)
    for (let index = 0; index < 6; index++) {
        f = randint(40, 1000)
        routeByFrequency()
        music.ringTone(f)
        basic.pause(randint(50, 500))
        music.stopAllSounds()
    }
    basic.clearScreen()
})
```

## Technical notes

- Only one speaker is on at a time. ``useBuiltInSpeaker`` turns on the micro:bit speaker and turns off the audio pin. ``useExternalSpeaker`` does the opposite.
- Button **A** plays 100 Hz three times on the micro:bit speaker. The volume is cut in half each time: 255, about 127, then about 64.
- Button **B** plays 8 pitches on the micro:bit speaker, doubling each time: 40, 80, 160, 320, 640, 1280, 2560 and 5120 Hz. Each tone lasts 0.2 seconds.
- The **logo** plays 6 random pitches from 40 to 1000 Hz on the Speaker:bit. Each one lasts a random time from 50 to 500 milliseconds.
- The small micro:bit speaker is weak at low pitches. That is why a crossover sends low pitches to the bigger Speaker:bit.

## Test your crossover

Download your code and press **B**.

- Which pitches come from the Speaker:bit? Which come from the micro:bit?
- Touch the logo. Does each random pitch go to the speaker you expected?

Click **Done**, then download the code to your micro:bit.
