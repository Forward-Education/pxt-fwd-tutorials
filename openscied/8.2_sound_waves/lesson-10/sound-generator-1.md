# Lesson 10 - Sound Generator 1

```package
radio=radio
```

```template
// Plays the same pitch 3 times, getting quieter each time.
// The bar graph shows the volume.
input.onButtonPressed(Button.A, function () {
    basic.showString("A")
    v = 250
    for (let index = 0; index < 3; index++) {
        // Maximum volume is 255.
        music.setVolume(v)
        led.plotBarGraph(v, 255)
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
// Plays 4 pitches at the same volume, doubling the frequency each time.
// The bar graph shows the frequency.
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    music.setVolume(150)
    f = 200
    for (let index = 0; index < 4; index++) {
        led.plotBarGraph(f, 1600)
        music.ringTone(f)
        basic.pause(500)
        music.stopAllSounds()
        basic.pause(200)
        f = f * 2
    }
    basic.clearScreen()
})
// Plays 5 short random pitches.
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

## Lesson 10 - Sound Generator 1 @showdialog

In this tutorial you will use the micro:bit to make sounds with different **volumes** and **frequencies**. Then you will change the code to make your own sounds.

The starter code is already in the workspace. Save a copy of your project before you start.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Use the code

Download the code to your micro:bit.

- Press **A** to play the same pitch 3 times, getting quieter each time. The bar graph shows the volume.
- Press **B** to play 4 pitches at the same volume, from low to high. The bar graph shows the frequency.
- Touch the **logo** to play 5 short random pitches.

## Read the code

Find the ``||loops:repeat||`` loop in the ``||input:on button B pressed||`` block.

```blocks
let f = 0
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    music.setVolume(150)
    f = 200
    // @highlight
    for (let index = 0; index < 4; index++) {
        led.plotBarGraph(f, 1600)
        music.ringTone(f)
        basic.pause(500)
        music.stopAllSounds()
        basic.pause(200)
        f = f * 2
    }
    basic.clearScreen()
})
```

- What frequency does it start at?
- What happens to the frequency each time through the loop?
- What do you hear as the frequency gets higher?

## Change the code

1. In the **B** block, change the starting frequency or how it changes each time through the loop.
2. In the **A** block, change the pitch from **262** Hz or how the volume changes.

Open the hint to see one example.

```blocks
let f = 0
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    music.setVolume(150)
    f = 100
    for (let index = 0; index < 5; index++) {
        led.plotBarGraph(f, 1600)
        music.ringTone(f)
        basic.pause(500)
        music.stopAllSounds()
        basic.pause(200)
        f = f * 2
    }
    basic.clearScreen()
})
```

## Technical notes

- Button **A** plays 262 Hz (middle C) three times. The volume starts at 250 and is cut in half each time: 250, 125, then about 62. Each tone lasts 0.5 seconds with a 0.2 second gap.
- Button **B** plays 200, 400, 800 and 1600 Hz at volume 150. Each tone is double the frequency of the one before. The bar graph is full at 1600 Hz.
- The **logo** plays 5 random pitches from 40 to 1000 Hz. Each one lasts only 50 milliseconds, so they sound like quick chirps.
- Volume on the micro:bit is a number from 0 to 255, not decibels.

## Test your code

Download your code and listen.

- Do you hear the change you expected?
- Does the bar graph match what you hear?

Click **Done**, then download the code to your micro:bit.
