# Lesson 6 - Station 5, Sensor 1

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
function calcAbsHumidity () {
    abshumidityrounded = opensciedModules.round(opensciedModules.bmeHumidity.absoluteHumidity(), 2)
}
input.onButtonPressed(Button.A, function () {
    basic.showString("" + (sensornumber))
    basic.pause(500)
    datasendstate = 1
})
input.onButtonPressed(Button.B, function () {
    basic.showString("" + (radiogroupnumber))
    datasendstate = 0
})
let abshumidityrounded = 0
let datasendstate = 0
let sensornumber = 0
let radiogroupnumber = 0
radiogroupnumber = 5
sensornumber = 1
radio.setGroup(radiogroupnumber)
basic.showString("" + (radiogroupnumber))
datasendstate = 0
basic.forever(function () {
    calcAbsHumidity()
    if (datasendstate == 1) {
        basic.showString("" + (abshumidityrounded))
        radio.sendValue("sensor 1", abshumidityrounded)
    }
})
```

## Lesson 6 - Station 5, Sensor 1

This project has the code for **Station 5, Sensor 1**.

Click **Done**, then download the code to your micro:bit.
