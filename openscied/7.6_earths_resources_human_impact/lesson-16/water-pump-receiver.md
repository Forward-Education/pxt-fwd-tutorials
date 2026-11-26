# Lesson 16 - Water Pump Receiver

```package
radio=radio
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
// Runs the pump in short bursts while the sender says the soil is dry.
// If the messages stop, the pump stops after the last burst.
radio.onReceivedValue(function (name, value) {
    if (name == "pump") {
        if (value == 1) {
            opensciedModules.pump.timedRun(500)
        } else {
            opensciedModules.pump.setOn(false)
        }
    }
})
let stationNumber = 0
// Set this to your station number (1 to 7). It must match the sender.
stationNumber = 1
radio.setGroup(stationNumber)
basic.showNumber(stationNumber)
```

## Lesson 16 - Water Pump Receiver @showdialog

This micro:bit is the **receiver**. It listens for the sender's radio message and runs the pump.

Save a copy of your project before you start.

## Set the station number

Find ``stationNumber`` in ``||basic:on start||`` and change it to your station number (1 to 7). It must be the same number as the sender.

## Read the receiver

Find the ``||radio:on radio received||`` block.

```blocks
radio.onReceivedValue(function (name, value) {
    // @highlight
    if (name == "pump") {
        if (value == 1) {
            opensciedModules.pump.timedRun(500)
        } else {
            opensciedModules.pump.setOn(false)
        }
    }
})
```

- It only acts on messages named **"pump"**.
- **1** runs the pump for 500 ms (0.5 seconds).
- **0** turns the pump off.

The pump only runs in short bursts, so if the sender stops or goes out of range, the pump stops too.

## Technical notes

- The receiver has no button controls. It only acts on radio messages. To stop the pump, press **A+B** on the sender.
- The radio group is the station number. If the pump never runs, check that both micro:bits show the same number.
- Each **1** message runs the pump for 500 ms. The sender sends about every 0.5 seconds, so the bursts join up while the soil stays dry.
- The receiver does not show the soil reading or send any data to the computer.

## Test

Download this code to the receiver micro:bit with the pump connected. Both micro:bits show the same station number. Put the sender's sensor in dry soil and check that the pump runs.

Click **Done** when the system works.
