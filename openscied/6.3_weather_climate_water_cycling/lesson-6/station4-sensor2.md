# Lesson 6 - Station 4, Sensor 2

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v0.0.6
```

```template
function calcAbsHumidity () {
    abshumidityfactor = 13.247 * (opensciedModules.bmeHumidity.humidity() / (273.15 + opensciedModules.bmeTemperature.temperature()))
    abshumidityexponent = 2.7183 ** (17.67 * opensciedModules.bmeTemperature.temperature() / (243.5 + opensciedModules.bmeTemperature.temperature()))
    abshumidityinitial = abshumidityfactor * abshumidityexponent
    abshumidityrounded = Math.round(abshumidityinitial * 100) / 100
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
let abshumidityinitial = 0
let abshumidityexponent = 0
let abshumidityfactor = 0
let datasendstate = 0
let sensornumber = 0
let radiogroupnumber = 0
radiogroupnumber = 4
sensornumber = 2
radio.setGroup(radiogroupnumber)
basic.showString("" + (radiogroupnumber))
datasendstate = 0
basic.forever(function () {
    calcAbsHumidity()
    if (datasendstate == 1) {
        basic.showString("" + (abshumidityrounded))
        radio.sendValue("sensor 2", abshumidityrounded)
    }
})
```

## Lesson 6 - Station 4, Sensor 2

This project has the code for **Station 4, Sensor 2**.

Click **Done**, then download the code to your micro:bit.
