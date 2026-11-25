# Lesson 3 - Light-Activated Sound Source

```package
radio=radio
microphone=microphone
```

```template
// The maximum value for volume is 255.
music.setVolume(127)
basic.forever(function () {
    // The maximum value for light level is 255.
    if (input.lightLevel() <= 130) {
        basic.showIcon(IconNames.Sad)
        music.stopAllSounds()
    } else if (input.lightLevel() > 130 && input.lightLevel() < 200) {
        basic.showIcon(IconNames.Happy)
        music.play(music.builtinPlayableSoundEffect(soundExpression.happy), music.PlaybackMode.UntilDone)
    } else if (input.lightLevel() >= 200) {
        basic.showIcon(IconNames.Umbrella)
        music.play(music.builtinPlayableSoundEffect(soundExpression.soaring), music.PlaybackMode.UntilDone)
    }
})
```

## Lesson 3 - Light-Activated Sound Source

This project has the code for **Light-Activated Sound Source**.

Click **Done**, then download the code to your micro:bit.
