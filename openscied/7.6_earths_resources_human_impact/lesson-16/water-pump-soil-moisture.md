# Lesson 16 - Water Pump and Soil Moisture Sensor

```package
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Starts watering again.
input.onButtonPressed(Button.A, function () {
    running = true
    basic.clearScreen()
})
// Stops the system and turns the pump off.
input.onButtonPressed(Button.AB, function () {
    running = false
    opensciedModules.pump.setOn(false)
    basic.showIcon(IconNames.Yes)
})
let input2 = 0
let running = false
// The system starts as soon as the micro:bit gets power.
running = true
// Reads the soil once, then uses that one reading for the graph,
// the face and the pump.
basic.forever(function () {
    input2 = opensciedModules.moisture1.moistureLevel()
    serial.writeValue("soil moisture", input2)
    if (running) {
        if (input2 >= 50) {
            basic.showIcon(IconNames.Happy)
            opensciedModules.pump.setOn(false)
        } else if (input2 >= 20) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . # # # .
                . . . . .
                `)
            opensciedModules.pump.setOn(false)
        } else {
            basic.showIcon(IconNames.Sad)
            opensciedModules.pump.timedRun(500)
        }
    }
    basic.pause(500)
})
```

## Lesson 16 - Water Pump and Soil Moisture Sensor @showdialog

In this tutorial you will read how an automatic watering system works, and then change it for your design.

The starter code is already in the workspace. Save a copy of your project before you start.

## Use the code

Connect the soil moisture sensor and the water pump. Download the code and keep the micro:bit connected by USB.

The system starts as soon as the micro:bit gets power. Press **A+B** to stop it, and **A** to start it again.

Open **Show data** to watch the graph of the soil moisture (%).

## Read the reading

Find the ``||basic:forever||`` loop.

```blocks
let input2 = 0
basic.forever(function () {
    // @highlight
    input2 = opensciedModules.moisture1.moistureLevel()
    // @highlight
    serial.writeValue("soil moisture", input2)
})
```

The micro:bit reads the soil **once** each time through the loop. That one reading goes to the **Show data** graph and decides the face and the pump.

## Read the decisions

Find the ``||logic:if||`` block.

```blocks
let input2 = 0
// @highlight
if (input2 >= 50) {
    basic.showIcon(IconNames.Happy)
    opensciedModules.pump.setOn(false)
} else if (input2 >= 20) {
    basic.showLeds(`
        . . . . .
        . # . # .
        . . . . .
        . # # # .
        . . . . .
        `)
    opensciedModules.pump.setOn(false)
} else {
    basic.showIcon(IconNames.Sad)
    opensciedModules.pump.timedRun(500)
}
```

- 50% or more: happy face, pump off.
- 20% up to 50%: neutral face, pump off.
- Under 20%: sad face, and the pump runs for a 0.5 second burst.

The loop waits 0.5 seconds, then checks again. Short bursts give the water time to soak in before the next reading.

## Change it for your design

Change the numbers **50** and **20**, or the burst length **500** ms, to fit your plant and soil.

## Technical notes

- The soil moisture reading is in %, from 0 (dry) to 100 (wet).
- The reading goes to **Show data** every time through the loop, even after you press **A+B**. Only the face and the pump stop.
- **A+B** turns the pump off and shows a check mark. **A** clears the screen and starts again.
- The pump only runs when the soil is under 20%, and only for 0.5 seconds at a time. Then the loop waits 0.5 seconds and reads the soil again. This keeps the pump from flooding the plant.
- Water takes time to soak down to the sensor. If the pump runs too long, try a shorter burst.

## Test your system

Download your code and put the sensor in dry soil. The pump should start straight away. Add water and check that the face changes and the pump stops.

Click **Done** when your system works.
