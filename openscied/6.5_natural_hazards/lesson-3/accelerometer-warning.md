# Lesson 3 - Accelerometer Warning

```package
radio=radio
```

```template
input.onButtonPressed(Button.A, function () {
    status = "default"
    basic.showString("A")
    basic.pause(500)
})
// Shows a warning when the strongest shake was in the warning range.
// This is the function you will change.
function DisplayNewWarning () {
    if (maxinput > 2000 && maxinput < 4000) {
        basic.showString("!")
    }
}
input.onButtonPressed(Button.B, function () {
    status = "warn"
    basic.showString("B")
    basic.pause(500)
})
let nextinput = 0
let maxinput = 0
let status = ""
let initialinput = 0
input.setAccelerometerRange(AcceleratorRange.EightG)
initialinput = input.acceleration(Dimension.Strength)
status = "default"
basic.showIcon(IconNames.Heart)
basic.pause(1000)
basic.clearScreen()
// Every half second, checks the strongest shake since the last check,
// then starts over from the resting value.
loops.everyInterval(500, function () {
    basic.clearScreen()
    if (status == "warn") {
        DisplayNewWarning()
    }
    maxinput = initialinput
})
// Reads the accelerometer, sends the reading to the computer and keeps track
// of the strongest shake. The highest value it can read is 8000 mg (8 g).
basic.forever(function () {
    nextinput = input.acceleration(Dimension.Strength)
    serial.writeValue("Input", nextinput)
    if (nextinput > maxinput) {
        maxinput = nextinput
    }
})
```

## Lesson 3 - Accelerometer Warning @showdialog

The micro:bit's accelerometer can measure shaking, like the shaking during an earthquake. In this tutorial you will test a warning system, read how it works, and then change it to give **three warning levels**.

The starter code is already in the workspace.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Use the code

Download the code to your micro:bit and keep it connected by USB.

- Press **A** for record mode. The micro:bit only records the shaking.
- Press **B** for warning mode. A **!** flashes when the shaking is in the warning range.

Press **B**, then shake the micro:bit gently and then hard. Open **Show data** to watch the graph of the readings.

## Read the warning

Find the ``||logic:if||`` block in the ``DisplayNewWarning`` function.

```blocks
let maxinput = 0
function DisplayNewWarning () {
    // @highlight
    if (maxinput > 2000 && maxinput < 4000) {
        basic.showString("!")
    }
}
```

- What range of readings shows the **!**?
- When the micro:bit sits still, the reading is about 1000 mg. Why do you think it is not 0?

## Read the timer

Find the ``||loops:every 500 ms||`` block.

```blocks
let maxinput = 0
let initialinput = 0
let status = ""
function DisplayNewWarning () {}
// @highlight
loops.everyInterval(500, function () {
    basic.clearScreen()
    if (status == "warn") {
        DisplayNewWarning()
    }
    maxinput = initialinput
})
```

The ``||basic:forever||`` loop keeps the hardest shake in ``maxinput``. Every half second, this block checks that hardest shake for a warning, then starts over. That way a quick shake is not missed.

## Add three warning levels

Change only the ``DisplayNewWarning`` function.

1. Copy the ``||logic:if||`` block twice, so you have three.
2. Change the numbers and signs so each block covers a different range: low, medium and high shaking.
3. Change the **!** in each block to a different character, such as **L**, **M** and **H**.

Use your graph from **Show data** to choose the numbers. Open the hint to see one example.

```blocks
let maxinput = 0
function DisplayNewWarning () {
    if (maxinput > 1500 && maxinput < 2500) {
        basic.showString("L")
    }
    if (maxinput >= 2500 && maxinput < 4000) {
        basic.showString("M")
    }
    if (maxinput >= 4000) {
        basic.showString("H")
    }
}
```

## Test your warnings

Download your code, press **B**, and try gentle, medium and hard shakes.

- Does each kind of shake show the level you expected?
- Compare the letters with the graph in **Show data**. Change your numbers if a level shows at the wrong time.

## Technical notes

- The accelerometer measures in **mg** (thousandths of g). Sitting still, it reads about 1000 mg because of gravity.
- The code sets the range to **8 g**, so the highest reading is about 8000 mg.
- At the start, the micro:bit saves its resting reading. Keep it still while the heart shows.
- The ``||basic:forever||`` loop sends every reading to **Show data**, in both **A** and **B** mode.
- Every 0.5 seconds, the screen clears and the hardest shake is checked. A letter takes time to scroll, so a warning can stay on the screen a little longer than 0.5 seconds.
- If two of your ranges overlap, both letters can show, one after the other.

Click **Done**, then download the code to your micro:bit.
