# Lesson 10 - Temperature Sensor with Radio Sending

```package
radio=radio
microphone=microphone
datalogger=datalogger
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
    radio.setGroup(1)
    basic.clearScreen()
    datalogger.deleteLog()
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
    radio.setGroup(2)
    basic.clearScreen()
    datalogger.deleteLog()
})
let inputcurrenttemp = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
basic.forever(function () {
    inputcurrenttemp = opensciedModules.bmeTemperature.readTemperature()
    if (outputchoice == "A" || outputchoice == "B") {
        basic.showNumber(inputcurrenttemp)
        serial.writeValue("temp data from micro:bit", inputcurrenttemp)
        serial.writeNumbers([inputcurrenttemp])
        datalogger.log(datalogger.createCV("temp", inputcurrenttemp))
        radio.sendValue("temp", inputcurrenttemp)
    }
    basic.pause(5000)
})
```

## Lesson 10 - Temperature Sensor with Radio Sending

This project has the code for **Temperature Sensor with Radio Sending**.

## How to use the code

Keep the micro:bit connected to the computer by USB and open **Show data** to graph the readings.

- At the start, a check mark shows. No data is sent or saved yet.
- Press **A** to start on radio group **1**.
- Press **B** to start on radio group **2**.

Pressing **A** or **B** erases the data log, so save your data first. The code has no stop button. Unplug the micro:bit to stop it.

## Technical notes

- The temperature comes from the BME280 sensor in °C. It is not rounded, so the number on the screen can be long.
- Every pass through the forever loop, the micro:bit scrolls the temperature, sends it to the computer, saves it to the data log and sends it by radio as **temp**. Then it waits 5 seconds. With the scroll time, readings are more than 5 seconds apart.
- The computer gets each reading twice: once as **temp data from micro:bit** and once as a plain number.
- Use the **Lesson 10 - Radio Receiving** code on a second micro:bit, set to the same group.

Click **Done**, then download the code to your micro:bit.
