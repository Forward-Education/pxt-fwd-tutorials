# Lesson 7 - Light Gate Timer

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
    opensciedModules.lcd1.clearScreen()
})
input.onButtonPressed(Button.AB, function () {
    // duration is the total time that the light detector was in the dark
    outputchoice = "station"
    // The value for Bbight/full light is stored right now.
    initiallightvalue = opensciedModules.solar1.lightLevel()
    basic.showString(station)
    opensciedModules.lcd1.clearScreen()
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    // rests the vairable that keeps track of when it went dark
    starttime = 0
    // keeps track of when resets when it went from dark back to light
    endtime = 0
    // resets the time it was in the dark
    duration = 0
    initiallightvalue = opensciedModules.solar1.lightLevel()
    highlightvalue = initiallightvalue * 0.9
    lowlightvalue = initiallightvalue * 0.6
    basic.showIcon(IconNames.Heart)
    opensciedModules.lcd1.clearScreen()
    opensciedModules.lcd1.printLineString("timer ready.   ", 1)
})
let sensorinput = 0
let lowlightvalue = 0
let highlightvalue = 0
let endtime = 0
let starttime = 0
let initiallightvalue = 0
let outputchoice = ""
let duration = 0
let station = ""
opensciedModules.initializeLcd()
opensciedModules.solar1.setSamplingRate(opensciedEnums.SamplingRate.Fast)
opensciedModules.lcd1.printLineString("press A or B", 1)
opensciedModules.lcd1.printLineString("              ", 2)
station = "L"
// duration is the total time that the light total time that detector was in the dark
duration = 0
outputchoice = "station"
basic.showString(station)
basic.forever(function () {
    sensorinput = opensciedModules.solar1.lightLevel()
    serial.writeValue("sensor input", opensciedModules.round(sensorinput, 2))
    if (outputchoice == "A") {
        led.plotBarGraph(
        sensorinput,
        100
        )
    }
    if (outputchoice == "B") {
        if (sensorinput < lowlightvalue && starttime == 0) {
            starttime = input.runningTime()
        }
        if (sensorinput > highlightvalue && (starttime > 0 && endtime == 0)) {
            endtime = input.runningTime()
            // calculates the difference between when end and start occured and then divides by 1000 to convert from milliseconds to seconds
            duration = (endtime - starttime) / 1000
            opensciedModules.lcd1.printLineString("duration (s):", 1)
            opensciedModules.lcd1.printLineString(convertToText(duration), 2)
            basic.showIcon(IconNames.Yes)
            outputchoice = "none"
        }
    }
})
```

## Lesson 7 - Light Gate Timer

This project has the code for **Light Gate Timer**.

Click **Done**, then download the code to your micro:bit.
