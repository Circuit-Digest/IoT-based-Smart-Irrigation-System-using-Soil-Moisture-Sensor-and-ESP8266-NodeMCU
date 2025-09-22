# IoT-based Smart Irrigation System using ESP8266 and Soil Moisture Sensor

![IoT Smart Irrigation System](https://circuitdigest.com/sites/default/files/projectimage_mic/IoT-based-Smart-Irrigation-System-using-Soil-Moisture-Sensor-and-ESP8266-NodeMCU.jpg)

## Overview

This project implements an intelligent irrigation system that automatically monitors soil moisture, temperature, and humidity levels to control water pump operations. The system uses IoT technology to send real-time data to ThingSpeak cloud platform for remote monitoring and control.

**Project Source:** [Circuit Digest - IoT Smart Irrigation System](https://circuitdigest.com/microcontroller-projects/iot-based-smart-irrigation-system-using-esp8266-and-soil-moisture-sensor)
**Projects:**[ESP8266 Projects](https://circuitdigest.com/esp8266-projects)


## Features

- **Automatic Irrigation Control**: Water pump activates when soil moisture drops below 50% and stops when it reaches 55%
- **Real-time Monitoring**: Continuous monitoring of soil moisture, temperature, and humidity
- **IoT Cloud Integration**: Data logging to ThingSpeak server for remote access
- **Smart Pump Control**: Relay-based pump control for safe operation
- **WiFi Connectivity**: Wireless data transmission and remote monitoring capabilities
- **Energy Efficient**: Uses millis() function instead of delay() for non-blocking operation

## Components Required

| Component | Quantity | Purpose |
|-----------|----------|---------|
| [**NodeMCU ESP8266**](https://circuitdigest.com/microcontroller-projects/esp8266-nodemcu-with-atmega16-avr-microcontroller-to-send-an-email) | 1 | Main microcontroller with WiFi capability |
| Soil Moisture Sensor Module | 1 | Measures soil moisture percentage |
| Water Pump Module | 1 | Pumps water for irrigation |
| Relay Module | 1 | Controls pump operation safely |
| DHT11 Sensor | 1 | Measures temperature and humidity |
| Breadboard | 1 | For prototyping connections |
| Connecting Wires | Several | For circuit connections |
| Power Supply (5V) | 1 | Powers sensors and pump |

## Circuit Diagram

The circuit connects:
- **Soil Moisture Sensor**: Analog output to A0 pin of NodeMCU
- **DHT11 Sensor**: Data pin to D3 of NodeMCU
- **Relay Module**: Control pin to D0 of NodeMCU
- **Water Pump**: Connected through relay for safe switching
- **Power Supply**: 5V for sensors and pump, NodeMCU powered via USB

## Pin Configuration

```
NodeMCU ESP8266 Pin Connections:
├── A0  ← Soil Moisture Sensor (Analog Output)
├── D0  → Relay Module (Control Pin)
├── D3  ← DHT11 Sensor (Data Pin)
├── 3.3V → DHT11 VCC
├── GND → Common Ground
└── VIN → 5V Power Supply
```

## Software Requirements

### Libraries Required
- `DHT.h` - For DHT11 sensor operations
- `ESP8266WiFi.h` - For WiFi connectivity

### ThingSpeak Setup
1. Create a ThingSpeak account at [thingspeak.com](https://thingspeak.com)
2. Create a new channel with 3 fields:
   - Field 1: Soil Moisture (%)
   - Field 2: Temperature (°C)
   - Field 3: Humidity (%)
3. Get your Write API Key from the channel settings

## Installation and Setup

### 1. Hardware Assembly
1. Connect all components according to the circuit diagram
2. Ensure proper power connections (5V for sensors, 3.3V for NodeMCU logic)
3. Double-check all connections before powering on

### 2. Software Configuration
1. Install required libraries in Arduino IDE
2. Update the following in the code:
   ```cpp
   String apiKey = "YOUR_THINGSPEAK_API_KEY";
   const char *ssid = "YOUR_WIFI_SSID";
   const char *pass = "YOUR_WIFI_PASSWORD";
   ```

### 3. Upload Code
1. Select NodeMCU 1.0 (ESP-12E Module) in Arduino IDE
2. Set the correct COM port
3. Upload the provided code to NodeMCU

## How It Works

### Operational Logic
1. **Sensor Reading**: System continuously reads soil moisture, temperature, and humidity
2. **Moisture Control**: 
   - If moisture < 50%: Turn ON water pump
   - If moisture between 50-55%: Keep pump ON
   - If moisture > 56%: Turn OFF water pump
3. **Data Transmission**: Every 10 seconds, sensor data is sent to ThingSpeak
4. **Remote Monitoring**: Data can be viewed on ThingSpeak dashboard from anywhere

### Key Functions
- `setup()`: Initializes sensors, WiFi connection, and pin configurations
- `loop()`: Main control loop for sensor reading and pump control
- `sendThingspeak()`: Sends sensor data to cloud platform

## Code Structure

```cpp
// Main sections of the code:
├── Library Includes & Variable Declarations
├── WiFi & ThingSpeak Configuration
├── Pin Definitions & Setup
├── Main Loop (Sensor Reading & Control)
├── Pump Control Logic
└── ThingSpeak Data Transmission
```

## Monitoring and Control

### ThingSpeak Dashboard Features
- Real-time graphs for moisture, temperature, and humidity
- Historical data analysis
- Remote monitoring from any internet-connected device
- Data export capabilities for further analysis

### System Alerts
The system provides:
- Serial monitor output for local debugging
- Cloud-based data logging for trend analysis
- Automatic pump status indication

## Troubleshooting

### Common Issues
1. **WiFi Connection Failed**: Check SSID and password
2. **Sensor Reading Errors**: Verify sensor connections and power supply
3. **Pump Not Working**: Check relay connections and power ratings
4. **ThingSpeak Upload Failed**: Verify API key and internet connection

### Debug Tips
- Use Serial Monitor (115200 baud) for real-time debugging
- Check all connections if sensors return NaN values
- Ensure stable power supply for consistent operation

## Applications

### Suitable For
- **Home Gardens**: Automated plant care for households
- **Greenhouse Farming**: Controlled environment agriculture
- **Small Scale Farming**: Efficient water management
- **Research Projects**: IoT and agriculture studies
- **Educational Purposes**: Learning IoT and sensor integration

### Crop Compatibility
The current configuration works best for crops requiring:
- Soil moisture: 50-55%
- Moderate temperature and humidity conditions

## Future Enhancements

### Possible Improvements
- Multiple sensor zones for larger areas
- Mobile app integration for smartphone control
- Weather forecast integration
- Different moisture thresholds for various crops
- Solar power integration for remote locations
- Water level monitoring in reservoir
- pH and nutrient monitoring capabilities

## Technical Specifications

### Operating Conditions
- **Input Voltage**: 5V DC
- **Operating Temperature**: 0°C to 50°C
- **Humidity Range**: 0% to 95% (non-condensing)
- **WiFi Standards**: 802.11 b/g/n
- **Data Update Interval**: 10 seconds
- **Moisture Threshold**: 50-56% (configurable)

## Safety Considerations

### Important Notes
- Use proper relay ratings for pump current
- Ensure waterproof connections for outdoor use
- Implement proper grounding for electrical safety
- Use GFCI protection in wet environments
- Regular maintenance of sensors and connections

## License

This project is based on the tutorial from Circuit Digest. Please refer to their website for licensing information and additional resources.

## Contributing

Contributions to improve this project are welcome. Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed description

## Support

For technical support and questions:
- Visit the [Circuit Digest Forums](https://circuitdigest.com/forums)
- Check the original tutorial for detailed explanations
- Review the troubleshooting section above

## Acknowledgments

- **Circuit Digest**: For the original tutorial and comprehensive guide
- **ESP8266 Community**: For extensive library support
- **ThingSpeak**: For IoT cloud platform services

---

**Project Complexity**: Intermediate  
**Estimated Build Time**: 2-3 hours  
**Skill Level Required**: Basic electronics and programming knowledge
