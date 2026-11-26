# Lesson 11 - Carbon Dice Game

```package
radio=radio
```

```template
// Moves the carbon to a reservoir and shows where it is.
function joinReservoir (newType: number) {
    _type = newType
    showReservoir()
}
// Scrolls the reservoir name twice, then leaves its first letter on the screen.
function showReservoir () {
    if (_type == At) {
        name = "At"
    } else if (_type == PA) {
        name = "PA"
    } else if (_type == SD) {
        name = "SD"
    } else {
        name = "FF"
    }
    for (let index = 0; index < 2; index++) {
        basic.showString(" " + name)
    }
    basic.showString(name.charAt(0))
}
// The rules from the station cards: on 1 to 4 the carbon stays,
// on 5 or 6 it moves to another reservoir.
function moveCarbon () {
    if (roll <= 4) {
        showReservoir()
    } else {
        basic.showArrow(ArrowNames.East)
        basic.pause(500)
        if (_type == At) {
            joinReservoir(PA)
        } else if (_type == PA) {
            joinReservoir(SD)
        } else if (_type == SD) {
            joinReservoir(At)
        } else {
            joinReservoir(At)
        }
    }
}
input.onButtonPressed(Button.A, function () {
    joinReservoir(At)
})
input.onButtonPressed(Button.B, function () {
    joinReservoir(PA)
})
input.onButtonPressed(Button.AB, function () {
    joinReservoir(SD)
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    joinReservoir(FF)
})
// Rolls the dice. Extra shakes are ignored until the result has finished.
input.onGesture(Gesture.Shake, function () {
    if (!(busy)) {
        busy = true
        if (_type < 0) {
            basic.showString("?")
        } else {
            roll = randint(1, 6)
            basic.showNumber(roll)
            basic.pause(500)
            moveCarbon()
        }
        busy = false
    }
})
let name = ""
let busy = false
let roll = 0
let _type = 0
let FF = 0
let SD = 0
let PA = 0
let At = 0
At = 0
PA = 1
SD = 2
FF = 3
// No reservoir yet. Press a button to choose one.
_type = -1
busy = false
basic.showString("?")
```

## Lesson 11 - Carbon Dice Game @showdialog

This project has the code for the **Carbon Dice Game**. Each student's micro:bit is a carbon atom that moves between reservoirs. Set it up before class.

This code uses the logo, so it needs a **micro:bit V2**.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## Choose a reservoir

Press a button to put the carbon in its starting reservoir:

| Button | Reservoir |
| --- | --- |
| **A** | Atmosphere (At) |
| **B** | Plants & Animals (PA) |
| **A+B** | Soil & Decomposers (SD) |
| **logo** | Fossil Fuels (FF) |

If you shake before choosing, the micro:bit shows **?**.

## The rules

Find the ``moveCarbon`` function.

```blocks
let roll = 0
let _type = 0
let At = 0
let PA = 0
let SD = 0
function showReservoir () {}
function joinReservoir (newType: number) {}
function moveCarbon () {
    // @highlight
    if (roll <= 4) {
        showReservoir()
    } else {
        basic.showArrow(ArrowNames.East)
        basic.pause(500)
        if (_type == At) {
            joinReservoir(PA)
        } else if (_type == PA) {
            joinReservoir(SD)
        } else if (_type == SD) {
            joinReservoir(At)
        } else {
            joinReservoir(At)
        }
    }
}
```

On a roll of 1 to 4 the carbon stays. On 5 or 6 it moves, as on the station cards. If your station cards send the carbon somewhere else, change the reservoir in that ``||logic:if||`` block.

## Technical notes

- Each reservoir is stored as a number: At = 0, PA = 1, SD = 2, FF = 3. At the start it is -1, which means no reservoir yet.
- A shake picks a random whole number from 1 to 6 with ``||math:pick random||``.
- On a 5 or 6 the carbon always moves in the same loop: At to PA, PA to SD, SD to At, and FF to At.
- The ``busy`` variable makes the micro:bit ignore extra shakes until one roll has finished. Button presses are not blocked, so do not press a button during a roll.
- A roll takes a few seconds because the name scrolls twice.
- The micro:bits do not talk to each other. The code does not use the radio.

## What the screen shows

Shake to roll. The micro:bit shows:

1. The roll (1 to 6).
2. An arrow if the carbon moves.
3. The reservoir name, twice.
4. The first letter of the reservoir, which stays on the screen.

Students should still check the station card for each move.

Click **Done**, then download the code to your micro:bit.
