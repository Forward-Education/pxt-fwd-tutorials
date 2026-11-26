# Lesson 10 - Digital Load Cell

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Sets the reading to zero with nothing on the load cell.
input.onButtonPressed(Button.AB, function () {
    opensciedModules.weight1.tare()
    basic.showIcon(IconNames.Yes)
    basic.pause(500)
    basic.clearScreen()
})
// Calibrates the load cell. Hold the logo with a 50 g mass on the load cell.
input.onLogoEvent(TouchButtonEvent.LongPressed, function () {
    opensciedModules.weight1.calibrate(50)
    basic.showIcon(IconNames.Happy)
    basic.pause(500)
    basic.clearScreen()
})
let Force = 0
let Mass = 0
opensciedModules.initializeLcd()
// Reads the load cell and shows the mass (g) and the force (N) on the LCD.
basic.forever(function () {
    // The load cell block gives kilograms, so x 1000 changes it to grams.
    Mass = Math.round(opensciedModules.weight1.weight() * 1000)
    // x 0.00981 changes grams into newtons (the force of gravity on the mass).
    Force = opensciedModules.round(Mass * 0.00981, 2)
    serial.writeValue("Force (N)", Force)
    opensciedModules.lcd1.printQuadrantString("Mass g", 1)
    opensciedModules.lcd1.printQuadrantNumber(Mass, 2)
    opensciedModules.lcd1.printQuadrantString("Force N", 3)
    opensciedModules.lcd1.printQuadrantNumber(Force, 4)
})
```

## Lesson 10 - Digital Load Cell

This project has the code for the **Digital Load Cell**.

## How to use the code

- The LCD shows the mass in grams (g) on line 1 and the force in newtons (N) on line 2.
- With nothing on the load cell, press **A+B** together to set the reading to zero. A check mark shows.
- To calibrate, put a 50 g mass on the load cell and hold the **logo** until a happy face shows.
- To project the force for the class, open **Show data** in MakeCode while the micro:bit is connected by USB.

## Technical notes

- The load cell block gives the mass in kilograms, so the code multiplies by **1000** to get grams.
- The code multiplies grams by **0.00981** to get the force of gravity in newtons. A 100 g mass gives about 0.98 N.

Click **Done**, then download the code to your micro:bit.
