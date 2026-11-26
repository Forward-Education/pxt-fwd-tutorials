# Lesson 7 - Light Gate Timer

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Aim mode: the bar graph shows how much light reaches the sensor.
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
    opensciedModules.lcd1.printLineString("Aim the light", 1)
    opensciedModules.lcd1.printLineString("at the sensor", 2)
})
// Timer mode: waits 1 second so your hands are clear, saves the full light
// level, then sets the start (60%) and stop (90%) levels from it.
input.onButtonPressed(Button.B, function () {
    outputchoice = "wait"
    starttime = 0
    endtime = 0
    duration = 0
    basic.showIcon(IconNames.Heart)
    opensciedModules.lcd1.printLineString("Hands clear...", 1)
    opensciedModules.lcd1.printLineString("", 2)
    basic.pause(1000)
    initiallightvalue = opensciedModules.solar1.lightLevel()
    highlightvalue = initiallightvalue * 0.9
    lowlightvalue = initiallightvalue * 0.6
    opensciedModules.lcd1.printLineString("Timer ready", 1)
    opensciedModules.lcd1.printLineString("Full light " + Math.round(initiallightvalue) + "%", 2)
    outputchoice = "B"
})
let sensorinput = 0
let lowlightvalue = 0
let highlightvalue = 0
let initiallightvalue = 0
let endtime = 0
let starttime = 0
let duration = 0
let outputchoice = ""
let station = ""
opensciedModules.initializeLcd()
// The solar sensor sends a new reading every 20 ms instead of every 100 ms,
// so short shadows are timed accurately.
opensciedModules.solar1.setSamplingRate(opensciedEnums.SamplingRate.Fast)
station = "L"
outputchoice = "none"
basic.showString(station)
opensciedModules.lcd1.printLineString("Press A or B", 1)
opensciedModules.lcd1.printLineString("", 2)
// Reads the sensor as fast as it can. In timer mode the timer starts when the
// light drops below 60% of full light and stops when it rises above 90%.
basic.forever(function () {
    sensorinput = opensciedModules.solar1.lightLevel()
    serial.writeValue("light (%)", opensciedModules.round(sensorinput, 2))
    if (outputchoice == "A") {
        led.plotBarGraph(
        sensorinput,
        100
        )
    } else if (outputchoice == "B") {
        if (sensorinput < lowlightvalue && starttime == 0) {
            starttime = input.runningTime()
        }
        if (sensorinput > highlightvalue && starttime > 0) {
            endtime = input.runningTime()
            // Running time is in milliseconds, so divide by 1000 to get seconds.
            duration = (endtime - starttime) / 1000
            outputchoice = "none"
            basic.showIcon(IconNames.Yes)
            opensciedModules.lcd1.printLineString("Time (s):", 1)
            opensciedModules.lcd1.printLineString(convertToText(opensciedModules.round(duration, 2)), 2)
        }
    }
})
```

## Lesson 7 - Light Gate Timer @showdialog

This project has the code for the **Light Gate Timer**. A flashlight shines on the solar sensor. When an object passes between them, its shadow starts the timer, and when the light comes back the timer stops. The LCD shows the time in seconds.

## Set up the hardware

Connect the **solar sensor** and the **LCD** to the micro:bit. Point a flashlight at the solar sensor.

## Aim the light

Press **A** for aim mode. The bar graph shows how much light reaches the sensor. Move the flashlight until the bar graph is as full as you can make it.

```blocks
let outputchoice = ""
// @highlight
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    basic.clearScreen()
    opensciedModules.lcd1.printLineString("Aim the light", 1)
    opensciedModules.lcd1.printLineString("at the sensor", 2)
})
```

## Arm the timer

Press **B** to arm the timer. A heart shows. Keep your hands clear for 1 second while the micro:bit saves the full light level. The LCD then shows **Timer ready** and the full light level in %.

```blocks
let outputchoice = ""
let starttime = 0
let endtime = 0
let duration = 0
let initiallightvalue = 0
let highlightvalue = 0
let lowlightvalue = 0
// @highlight
input.onButtonPressed(Button.B, function () {
    outputchoice = "wait"
    starttime = 0
    endtime = 0
    duration = 0
    basic.showIcon(IconNames.Heart)
    opensciedModules.lcd1.printLineString("Hands clear...", 1)
    opensciedModules.lcd1.printLineString("", 2)
    basic.pause(1000)
    initiallightvalue = opensciedModules.solar1.lightLevel()
    highlightvalue = initiallightvalue * 0.9
    lowlightvalue = initiallightvalue * 0.6
    opensciedModules.lcd1.printLineString("Timer ready", 1)
    opensciedModules.lcd1.printLineString("Full light " + Math.round(initiallightvalue) + "%", 2)
    outputchoice = "B"
})
```

The timer **starts** when the light drops below 60% of full light, and **stops** when it rises above 90% of full light.

## Test the timer

1. Press **B** and wait for **Timer ready**.
2. Block the sensor with your hand for about 4 seconds, then move your hand away.
3. A check mark shows and the LCD should show about **4** seconds.

Press **B** again before each new run.

## Technical notes

- The ``||opensciedModules:set solar1 sampling to fast||`` block makes the solar sensor send a reading every 20 ms instead of every 100 ms, so a quick shadow is not missed.
- The start and stop levels are a share of the full light level, so the timer works in bright and dim rooms.

If the timer never starts, the shadow is not dark enough. Dim the room lights, or move the flashlight closer to the sensor, then press **B** again.

Click **Done**, then download the code to your micro:bit.
