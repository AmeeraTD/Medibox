# Smart Medicine Alarm System

## Overview
This project implements a **Smart Medicine Alarm System** using an ESP32 microcontroller. It features an OLED display, a buzzer for alarms, and the ability to set multiple alarms for medicine reminders. The system also includes temperature and humidity monitoring, MQTT integration, and light-based adjustments using LDR sensors and a servo motor.

---

## Features
1. **Alarm System**:
   - Supports up to 3 alarms for medicine reminders.
   - Visual and auditory notifications using an OLED display and buzzer.
   - Cancel alarms via button input.

2. **Temperature and Humidity Monitoring**:
   - Uses a DHT22 sensor to measure environmental conditions.
   - Displays warnings for high/low temperature and humidity.

3. **Light Intensity Adjustment**:
   - Uses LDR sensors to measure light intensity.
   - Adjusts a servo motor based on light readings.

4. **MQTT Integration**:
   - Publishes sensor data (e.g., temperature, light readings).
   - Receives configuration updates via MQTT topics.

5. **Time Synchronization**:
   - Synchronizes with an NTP server for accurate timekeeping.

6. **Menu System**:
   - Navigate settings using buttons.
   - Configure alarms, set time, and adjust settings.

---

## Components
1. **Microcontroller**: ESP32
2. **Sensors**:
   - DHT22 (Temperature and Humidity)
   - LDR (Light Dependent Resistors)
3. **Output Devices**:
   - OLED Display (SSD1306, 128x64)
   - Buzzer
   - Servo Motor
4. **Input Devices**:
   - Buttons (`ok`, `up`, `down`, `cancel`)
5. **Other Components**:
   - WiFi module (integrated with ESP32)
   - MQTT broker (e.g., test.mosquitto.org)

---

## Setup Instructions

### **Hardware Connections**
- **OLED Display**: Connect to the I2C pins (`SDA` and `SCL`).
- **DHT22 Sensor**: Connect the data pin to GPIO12.
- **Buzzer**: Connect to GPIO23.
- **Buttons**: Connect `ok`, `up`, `down`, and `cancel` to GPIO33, GPIO32, GPIO27, and GPIO26, respectively.
- **LDR Sensors**: Connect `ldr_left` and `ldr_right` to GPIO34 and GPIO35.
- **Servo Motor**: Connect the control pin to GPIO14.

### **Software Setup**
1. Install the required libraries in your Arduino IDE:
   - Adafruit_GFX
   - Adafruit_SSD1306
   - DHT sensor library
   - PubSubClient
   - NTPClient
   - ESP32Servo
2. Configure WiFi credentials in the `setup()` function:
   ```cpp
   WiFi.begin("<SSID>", "<PASSWORD>");
   ```
3. Configure MQTT topics and broker settings in the `setup_mqtt()` function.
4. Upload the code to the ESP32 using the Arduino IDE.

---

## How to Use
1. **Power On**:
   - The system will connect to WiFi and synchronize time via NTP.
2. **Set Alarms**:
   - Use the menu system (`ok`, `up`, `down`, `cancel` buttons) to configure alarms.
3. **Disable Alarms**:
   - Navigate to the "Disable Alarm" option in the menu.
4. **Monitor Temperature and Humidity**:
   - The OLED display shows live readings and warnings for extreme conditions.
5. **Light Adjustment**:
   - The servo motor adjusts its position based on light intensity measured by the LDRs.
6. **MQTT**:
   - Sensor data is published to MQTT topics (`TEMP`, `LIGHT-L`, `LIGHT-R`).
   - Configuration updates can be sent via MQTT topics.

---

## MQTT Topics
- **Publish**:
  - `TEMP`: Sends temperature readings.
  - `LIGHT-L`: Sends left LDR readings.
  - `LIGHT-R`: Sends right LDR readings.
- **Subscribe**:
  - `ON-OFF`: Controls an external device (on/off states).
  - `ADMIN-SCHEDULE-ON`: Reserved for admin control.
  - `ADJUSTMENTS_MIN`: Adjusts the servo offset.
  - `ADJUSTMENTS_CF`: Configures gamma value for light adjustment.

---

## Customization
1. **Alarms**:
   - Modify the number of alarms or customize alarm tones in the `ring_buzzer()` function.
2. **MQTT Topics**:
   - Add new topics for more functionality.
3. **Sensor Thresholds**:
   - Change temperature and humidity warning thresholds in the `check_temp()` function.

---

## Troubleshooting
1. **WiFi Not Connecting**:
   - Verify SSID and password.
   - Ensure the network is operational.
2. **Alarms Not Triggering**:
   - Check the configured alarm times.
   - Verify button functionality.
3. **No MQTT Messages**:
   - Check MQTT broker status and connectivity.
   - Ensure correct topic subscriptions.
4. **Servo Not Moving**:
   - Verify connections and power supply.
   - Check LDR readings.

---

## Future Improvements
- Add support for multiple users and schedules.
- Integrate a mobile app for remote control and monitoring.
- Improve UI design for better usability.

---


## Acknowledgments
- Libraries and tools from Adafruit, Arduino, and the open-source community.
- MQTT broker support from `test.mosquitto.org`.
- Time synchronization using `NTPClient`.

