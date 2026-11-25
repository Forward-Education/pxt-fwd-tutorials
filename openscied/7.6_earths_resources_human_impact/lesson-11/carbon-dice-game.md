# Lesson 11 - Carbon Dice Game

```package
radio=radio
microphone=microphone
```

```template
function RunPA () {
    if (roll < 4) {
        for (let index = 0; index < 2; index++) {
            basic.showString(" PA")
        }
    } else if (roll == 4) {
        for (let index = 0; index < 2; index++) {
            basic.showString(" At")
        }
        _type = At
    } else {
        for (let index = 0; index < 2; index++) {
            basic.showString(" SD")
        }
        _type = SD
    }
}
function RunAt () {
    if (roll < 4) {
        for (let index = 0; index < 2; index++) {
            basic.showString(" At")
        }
    } else {
        for (let index = 0; index < 2; index++) {
            basic.showString(" PA")
        }
        _type = PA
    }
}
input.onButtonPressed(Button.A, function () {
    _type = At
    for (let index = 0; index < 2; index++) {
        basic.showString(" At")
    }
    roll = 0
})
function RunFF () {
    if (roll < 5) {
        for (let index = 0; index < 2; index++) {
            basic.showString(" FF")
        }
    } else {
        _type = At
        for (let index = 0; index < 2; index++) {
            basic.showString(" At")
        }
    }
    roll = 0
}
input.onButtonPressed(Button.AB, function () {
    _type = SD
    for (let index = 0; index < 2; index++) {
        basic.showString(" SD")
    }
    roll = 0
})
function RunSD () {
    if (roll < 6) {
        for (let index = 0; index < 2; index++) {
            basic.showString(" SD")
        }
    } else {
        _type = At
        for (let index = 0; index < 2; index++) {
            basic.showString(" At")
        }
    }
    roll = 0
}
input.onButtonPressed(Button.B, function () {
    _type = PA
    for (let index = 0; index < 2; index++) {
        basic.showString(" PA")
    }
    roll = 0
})
input.onGesture(Gesture.Shake, function () {
    if (roll == 0) {
        roll = randint(1, 6)
    }
    basic.showNumber(roll)
    if (_type == At) {
        RunAt()
    } else if (_type == PA) {
        RunPA()
    } else if (_type == SD) {
        RunSD()
    } else if (_type == FF) {
        RunFF()
    } else {
        basic.showString("?")
    }
    roll = 0
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    _type = FF
    for (let index = 0; index < 2; index++) {
        basic.showString(" FF")
    }
    roll = 0
})
let _type = 0
let roll = 0
let FF = 0
let SD = 0
let PA = 0
let At = 0
basic.showString("?")
At = 0
PA = 1
SD = 2
FF = 3
```

## Lesson 11 - Carbon Dice Game

This project has the code for **Carbon Dice Game**.

Click **Done**, then download the code to your micro:bit.
