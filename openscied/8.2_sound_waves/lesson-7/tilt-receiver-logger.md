# Lesson 7 - Tilt Sensor Receiver and Data Logger

```package
radio=radio
```

```template
// Sends each angle to the computer with the starting angle,
// so Show data graphs them together.
radio.onReceivedNumber(function (receivedNumber) {
    currentangle = receivedNumber
    serial.writeNumbers([currentangle, initialangle])
})
// Gets ready for a new run and tells the transmitter to start.
function startRun (button: string) {
    radio.sendString(button)
    serial.writeLine("Countdown....")
    goreceived = false
    basic.showIcon(IconNames.Happy)
}
// Closed run.
input.onButtonPressed(Button.A, function () {
    startRun("A")
})
// Open run.
input.onButtonPressed(Button.B, function () {
    startRun("B")
})
function showRadioGroup () {
    basic.clearScreen()
    basic.pause(100)
    basic.showString("R")
    basic.pause(1000)
    basic.showNumber(myRadioGroup)
    basic.pause(1000)
    basic.clearScreen()
}
// Shows the radio group on both micro:bits, so you can check
// they are on the same group.
input.onButtonPressed(Button.AB, function () {
    radio.sendString("A+B")
    showRadioGroup()
})
radio.onReceivedString(function (receivedString) {
    if (receivedString == "A+B") {
        showRadioGroup()
    } else if (receivedString == "ready") {
        basic.showString("+")
    } else if (receivedString == "go") {
        goreceived = true
    } else if (receivedString == "stop") {
        if (goreceived == true) {
            basic.showIcon(IconNames.Yes)
        }
    } else {
        basic.showString(receivedString)
    }
})
// Saves the starting (resting) angle sent by the transmitter.
radio.onReceivedValue(function (name, value) {
    if (name == "InitDeg") {
        initialangle = value
        serial.writeLine("")
    }
})
let initialangle = 0
let currentangle = 0
let goreceived = false
let myRadioGroup = 0
serial.writeLine("Startup")
// Set this to your station number. The transmitter must use the same number.
myRadioGroup = 1
radio.setGroup(myRadioGroup)
goreceived = false
basic.showIcon(IconNames.Heart)
```

## Lesson 7 - Tilt Sensor Receiver and Data Logger

This project has the code for **Tilt Sensor Receiver and Data Logger**. It goes on the micro:bit connected to the computer by USB.

## Before you start

- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

- Set ``myRadioGroup`` to your station number before you download. The transmitter must use the same number.
- Press **A** for a closed run or **B** for an open run. A happy face shows and the transmitter starts its countdown.
- A check mark shows when the run is finished.
- Press **A+B** together to show **R** and the radio group on both micro:bits.

Open **Show data** to see the current angle and the starting angle graphed over time.

## Technical notes

- The receiver does not measure anything. It only listens on the radio and passes data to the computer.
- Each angle from the transmitter is written to the serial port with the starting angle (``InitDeg``), so **Show data** draws two lines: the moving angle and a flat line at rest.
- Countdown numbers and **+** sent by the transmitter scroll on this screen, so you can see the countdown from the computer side.
- The check mark only shows if a ``go`` message arrived first. If no check mark shows, the micro:bits may be on different radio groups.
- Pressing **A** or **B** clears the ``go`` flag, then sends the letter to the transmitter, which starts the run.

Click **Done**, then download the code to your micro:bit.
