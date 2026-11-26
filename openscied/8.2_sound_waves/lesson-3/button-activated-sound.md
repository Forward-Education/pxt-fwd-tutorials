# Lesson 3 - Button-Activated Sound Source

```package
radio=radio
```

```template
// Plays the sound signal. Change the sound here and it changes
// for both buttons and for the radio.
function playSignal () {
    music.play(music.builtinPlayableSoundEffect(soundExpression.spring), music.PlaybackMode.UntilDone)
}
// Tells the other micro:bit to play the sound.
input.onButtonPressed(Button.A, function () {
    radio.sendString("A")
})
// Plays the sound when the other micro:bit sends a message.
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
    playSignal()
    basic.clearScreen()
})
// Plays the sound on this micro:bit.
input.onButtonPressed(Button.B, function () {
    basic.showString("B")
    playSignal()
    basic.clearScreen()
})
// Change this number to stop interference from other groups.
// Pick a number from 2 to 255 and tell your teacher what you picked.
let myRadioGroup = 1
radio.setGroup(myRadioGroup)
basic.showNumber(myRadioGroup)
// The maximum volume is 255.
music.setVolume(127)
```

## Lesson 3 - Button-Activated Sound Source @showdialog

In this tutorial you will use two micro:bits as sound sources. One micro:bit can make the other one play a sound by radio. Then you will change the code for your group.

The starter code is already in the workspace. Save a copy of your project before you start.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Use the code

Download the code to both micro:bits. Each one shows its radio group number when it starts.

- Press **A** to play the sound on the **other** micro:bit.
- Press **B** to play the sound on **this** micro:bit.

## Read the code

Find the ``playSignal`` function. Both buttons and the radio use this function, so the sound is always the same.

```blocks
// @highlight
function playSignal () {
    music.play(music.builtinPlayableSoundEffect(soundExpression.spring), music.PlaybackMode.UntilDone)
}
```

Find the ``myRadioGroup`` variable in the ``||basic:on start||`` block. Both micro:bits must have the same group number to talk to each other.

## Change the code

1. Set ``myRadioGroup`` to a number from **2** to **255**. Tell your teacher which number you picked, so no other group uses it.
2. Change the volume from **127** to a louder value. The maximum is **255**.
3. Change the sound in ``playSignal`` to a different sound.

Open the hint to see one example.

```blocks
function playSignal () {
    music.play(music.builtinPlayableSoundEffect(soundExpression.twinkle), music.PlaybackMode.UntilDone)
}
let myRadioGroup = 17
radio.setGroup(myRadioGroup)
basic.showNumber(myRadioGroup)
music.setVolume(255)
```

## Technical notes

- Button **A** sends the letter **A** by radio. It does not play a sound on this micro:bit.
- When a micro:bit gets a radio message, it shows the message, plays the sound, and clears the screen.
- Button **B** shows **B** and plays the sound on this micro:bit only.
- Radio only works between micro:bits on the same group. Any micro:bit nearby on the same group will also play the sound, which is why each group picks its own number.
- The sound is in one function, ``playSignal``, so changing it once changes it everywhere.

## Test your code

Download your code to **both** micro:bits.

- Do both micro:bits show your group number?
- Does pressing **A** play the new sound on the other micro:bit?

Click **Done**, then download the code to your micro:bit.
