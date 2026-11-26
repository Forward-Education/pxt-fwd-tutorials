# Lesson 3 - Light-Activated Sound Source

```package
radio=radio
```

```template
// Shows the light level so you can choose your own thresholds.
input.onButtonPressed(Button.A, function () {
    basic.showNumber(lightlevel)
})
let lightlevel = 0
// The maximum value for volume is 255.
music.setVolume(127)
// Reads the light level once each time through the loop,
// then picks a face and a sound for that level.
basic.forever(function () {
    // The light level goes from 0 (dark) to 255 (bright).
    lightlevel = input.lightLevel()
    if (lightlevel <= 130) {
        basic.showIcon(IconNames.Sad)
        music.stopAllSounds()
    } else if (lightlevel < 200) {
        basic.showIcon(IconNames.Happy)
        music.play(music.builtinPlayableSoundEffect(soundExpression.happy), music.PlaybackMode.UntilDone)
    } else {
        basic.showIcon(IconNames.Umbrella)
        music.play(music.builtinPlayableSoundEffect(soundExpression.soaring), music.PlaybackMode.UntilDone)
    }
})
```

## Lesson 3 - Light-Activated Sound Source @showdialog

The micro:bit has a light sensor in its screen. In this tutorial you will use light to turn sound on and off, and then change the code so it works well in your classroom.

The starter code is already in the workspace. Save a copy of your project before you start.

## Use the code

Download the code to your micro:bit.

- In the dark, a sad face shows and there is no sound.
- In medium light, a happy face shows and the micro:bit plays a happy sound.
- In bright light, an umbrella shows and the micro:bit plays a soaring sound.

Press **A** to see the light level right now. Try it in the dark, in normal room light and with a flashlight.

## Read the thresholds

Find the ``||logic:if||`` block in the ``||basic:forever||`` loop.

```blocks
let lightlevel = 0
basic.forever(function () {
    lightlevel = input.lightLevel()
    // @highlight
    if (lightlevel <= 130) {
        basic.showIcon(IconNames.Sad)
        music.stopAllSounds()
    } else if (lightlevel < 200) {
        basic.showIcon(IconNames.Happy)
        music.play(music.builtinPlayableSoundEffect(soundExpression.happy), music.PlaybackMode.UntilDone)
    } else {
        basic.showIcon(IconNames.Umbrella)
        music.play(music.builtinPlayableSoundEffect(soundExpression.soaring), music.PlaybackMode.UntilDone)
    }
})
```

- Which light levels are dark, medium and bright?
- Do these numbers match the light levels you saw when you pressed **A**?

## Change the code

1. Change **130** and **200** so the three faces match the light in your classroom. Use the numbers you saw when you pressed **A**.
2. Change the volume from **127** to a louder value. The maximum is **255**.
3. Change one of the sounds to a different sound.

Open the hint to see one example.

```blocks
let lightlevel = 0
music.setVolume(255)
basic.forever(function () {
    lightlevel = input.lightLevel()
    if (lightlevel <= 150) {
        basic.showIcon(IconNames.Sad)
        music.stopAllSounds()
    } else if (lightlevel < 220) {
        basic.showIcon(IconNames.Happy)
        music.play(music.builtinPlayableSoundEffect(soundExpression.giggle), music.PlaybackMode.UntilDone)
    } else {
        basic.showIcon(IconNames.Umbrella)
        music.play(music.builtinPlayableSoundEffect(soundExpression.soaring), music.PlaybackMode.UntilDone)
    }
})
```

## Technical notes

- The light sensor gives a number from 0 (dark) to 255 (bright). The code reads it once each time through the ``||basic:forever||`` loop.
- Two numbers split the light into three ranges: 130 or less is dark, from 131 to 199 is medium, and 200 or more is bright.
- Each sound plays until it is done before the loop reads the light again. So the face can take a moment to change after the light changes.
- The volume is set once at the start. 127 is about half of the maximum of 255.

## Test your code

Download your code and test it in the dark, in medium light and in bright light.

- Does each light level give the face and sound you expected?
- If not, press **A** to check the light level and change your numbers.

Click **Done**, then download the code to your micro:bit.
