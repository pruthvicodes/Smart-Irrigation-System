# Smart Irrigation System (Automatic Plant Watering)

An Arduino-based system that **waters plants automatically**. A soil-moisture sensor checks how dry the soil is: when it's dry, a relay switches on a water pump, and when there's enough moisture, the pump turns off. A 16×2 LCD shows the current soil status and whether the motor is on.

> First-year engineering team project (2023–24).

---

## How it works

The sensor gives an analog reading from 0 to 1023. A higher value means drier soil.

| Sensor reading | Soil status | Pump |
|---|---|---|
| > 950 | Dry | **ON** |
| 400 – 950 | Medium moisture | OFF |
| < 400 | Wet | OFF |

The Arduino reads the sensor 10 times a second, switches the relay, and prints the status to the LCD and the Serial Monitor.

---

## Components

- Arduino Uno
- Soil-moisture sensor (FC-28) with its comparator module
- 5 V single-channel relay module
- Mini submersible DC water pump + 9 V battery
- 16×2 LCD with I2C adapter (address `0x27`)
- Jumper wires, breadboard, water reservoir and tubing

---

## Wiring

| Component | Pin | Arduino |
|---|---|---|
| Soil-moisture sensor | AO / VCC / GND | **A0** / 5V / GND |
| Relay module | IN / VCC / GND | **D7** / 5V / GND |
| LCD (I2C) | SDA / SCL / VCC / GND | **A4** / **A5** / 5V / GND |
| Water pump | Powered by the 9 V battery, switched through the relay's COM and NO terminals | |

The relay module is **active-LOW**: the code sets pin 7 `LOW` to switch the pump **on**.

---

## Code

| Sketch | Purpose |
|---|---|
| [`soil_moisture_test/`](soil_moisture_test/soil_moisture_test.ino) | Step 1: read the sensor and print dry / medium / wet to the Serial Monitor (for testing and calibration) |
| [`plant_watering_system/`](plant_watering_system/plant_watering_system.ino) | Step 2: the full system, with pump control via the relay and status on the LCD |

### Running it
1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Install the **LiquidCrystal I2C** library: **Sketch → Include Library → Manage Libraries**, then search for "LiquidCrystal I2C".
3. Open a sketch, select **Arduino Uno** and the right COM port, and click **Upload**.
4. Open the **Serial Monitor** at **9600 baud** to see live readings.

> The 400 and 950 thresholds depend on your sensor and soil. Run `soil_moisture_test` first and adjust them if needed.

---

## Possible improvements

- Average several readings to avoid the pump flickering on and off near a threshold
- Add a Wi-Fi module (ESP8266 / ESP32) to monitor soil moisture from a phone
- Log moisture data over time and use it to predict watering needs

---

## Author

**Prithviraj Chavan**: [LinkedIn](https://www.linkedin.com/in/prithvirajshahajichavan) · [GitHub](https://github.com/pruthvicodes)

*Circuit and code adapted from the Tech at Home YouTube tutorial series.*
