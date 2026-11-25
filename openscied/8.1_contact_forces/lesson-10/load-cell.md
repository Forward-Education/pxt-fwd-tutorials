# Lesson 10 - Digital Load Cell

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    opensciedModules.lcd1.printLineNumber(Math.round(opensciedModules.weight1.weight()), 1)
    opensciedModules.lcd1.printLineString("Weight", 2)
})
input.onButtonPressed(Button.AB, function () {
    opensciedModules.weight1.tare()
    opensciedModules.lcd1.printLineNumber(Math.round(opensciedModules.weight1.weight()), 1)
    opensciedModules.lcd1.printLineString("Tare", 2)
})
input.onButtonPressed(Button.B, function () {
    Force = opensciedModules.weight1.weight() * 0.00981
    opensciedModules.lcd1.printLineNumber(Force, 1)
    opensciedModules.lcd1.printLineString("Force", 2)
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    opensciedModules.weight1.calibrate(50)
    opensciedModules.lcd1.printLineNumber(Math.round(opensciedModules.weight1.weight()), 1)
    opensciedModules.lcd1.printLineString("Calibration", 2)
})
let Force = 0
opensciedModules.initializeLcd()
opensciedModules.lcd1.printLineString("Hello", 1)
opensciedModules.lcd1.printLineString("World", 2)
basic.pause(5000)
opensciedModules.lcd1.clearScreen()
```

## Lesson 10 - Digital Load Cell

This project has the code for **Digital Load Cell**.

Click **Done**, then download the code to your micro:bit.
