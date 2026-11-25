# Lesson 3 - Button-Activated Sound Source

```package
radio=radio
microphone=microphone
audio-recording=audio-recording
```

```template
input.onButtonPressed(Button.A, function () {
    radio.sendString("A")
})
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
    // if you change this sound to something other than "spring", then make the same change in the "on button B" blocks of code.
    music.play(music.builtinPlayableSoundEffect(soundExpression.spring), music.PlaybackMode.UntilDone)
    basic.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    // if you change this sound to something other than "spring", then make the same change in the "on radio received" blocks of code.
    music.play(music.builtinPlayableSoundEffect(soundExpression.spring), music.PlaybackMode.UntilDone)
    basic.clearScreen()
})
// Change this value to prevent interference from other groups. Pick a number between 2 and 255) and tell your teacher what you picked.
let myradiochannel = 1
radio.setGroup(myradiochannel)
basic.showNumber(myradiochannel)
// The maximum volume you can set this to is 255.
music.setVolume(127)
```

## Lesson 3 - Button-Activated Sound Source

This project has the code for **Button-Activated Sound Source**.

Click **Done**, then download the code to your micro:bit.
