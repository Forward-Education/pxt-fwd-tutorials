# Lesson 10 - CO2 Sensor with Radio (Example)

```package
radio=radio
microphone=microphone
openscied=github:Forward-Education/pxt-openscied#v1.1.0
```

```template
input.onButtonPressed(Button.A, function () {
    outputchoice = "A"
})
input.onButtonPressed(Button.AB, function () {
    outputchoice = "station"
})
input.onButtonPressed(Button.B, function () {
    outputchoice = "B"
})
let OUTPUT = 0
let HUMIDITY = 0
let CO2 = 0
let outputchoice = ""
outputchoice = "station"
basic.showIcon(IconNames.Yes)
radio.setGroup(1)
basic.forever(function () {
    CO2 = opensciedModules.eCO2.eco2()
    HUMIDITY = opensciedModules.bmeHumidity.humidity()
    if (outputchoice == "A") {
        OUTPUT = CO2
        serial.writeValue("CO2: ", OUTPUT)
        radio.sendValue("CO2:", OUTPUT)
    }
    if (outputchoice == "B") {
        OUTPUT = HUMIDITY
        serial.writeValue("Humidity", OUTPUT)
        radio.sendValue("Humidity", OUTPUT)
    }
    basic.showNumber(OUTPUT)
    basic.pause(5000)
})
```

## Lesson 10 - CO2 Sensor with Radio (Example)

This project has the code for **CO2 Sensor with Radio (Example)**.

## Before you start

- Plug the micro:bit into the breakout board.
- Plug the module(s) into the breakout board.
- Switch the breakout board on. A green light shows when it has power.
- Plug the micro:bit into the computer with a USB cable.
- To connect to the micro:bit you must be using Google Chrome.
- This code may require a V2 micro:bit.

## How to use the code

This is an example of the CO2 sensor code with radio sending. Keep the micro:bit connected to the computer by USB and open **Show data** to graph the readings.

- At the start, a check mark shows. No data is sent yet.
- Press **A** to read CO2. The value scrolls, goes to the computer and is sent by radio.
- Press **B** to read humidity. The value scrolls, goes to the computer and is sent by radio.
- Press **A+B** to stop sending data.

Use the **Lesson 10 - Radio Receiving** code on a second micro:bit, and press **A** on it to listen on group 1.

## Technical notes

- The radio uses group **1**.
- CO2 comes from the eCO2 sensor in parts per million (ppm). Humidity comes from the BME280 sensor in %.
- The radio value is named **CO2:** in mode A and **Humidity** in mode B.
- The forever loop takes one reading, scrolls it, then waits 5 seconds. With the scroll time, readings are about 6 to 8 seconds apart.
- A button press takes effect on the next pass through the loop, so it can take a few seconds.
- Unlike the CO2 Sensor code, **A+B** does not show a check mark. The screen keeps scrolling the last reading, but nothing is sent. Before you press **A** or **B** for the first time, it scrolls **0**.

Click **Done**, then download the code to your micro:bit.
