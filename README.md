# Warning READ BELOW

## This project is currently being reworked and built entirely from scratch to utilize Raspberry Pi 5 and advanced AI Models. Check out the development [**here**](https://github.com/m4xy07/CropSense-Pi)



## Aim and Objective of the Arduino Based Crop and Weather Suitability Station

This project aims to create a comprehensive weather station that monitors various environmental parameters and analyzes their suitability for crop growth. 
Here's a breakdown of the objectives:

* **Environmental Data Collection:** 
    * Measures temperature, humidity, atmospheric pressure, altitude, air quality, soil moisture, and rainfall.
    * Employs sensors like DHT22, BME280, rain sensor, soil moisture sensor and a MQ-135 for air quality.
* **Data Processing and Analysis:**
    * Calculates heat index based on temperature and humidity.
    * Accesses a JSON database containing crop-specific requirements for temperature, humidity, and soil moisture.
    * Analyzes the collected data against the crop database to determine suitable crops for the current conditions.
* **Data Display and Storage:**
    * Presents the collected sensor data on an OLED display.
    * Logs the data to an SD card for later analysis which also serves as a data backup in case WiFi is not available or we lose connection to the server.
* **Web Connectivity and Data Transmission:**
    * Connects to a Wi-Fi network.
    * Transmits the collected weather data along with crop suitability information to a web server at regular intervals.

The Data transmision and processing (storage of data recieved in a MongoDB on a server) is done via the [Arduino Server Manager](https://github.com/m4xy07/arduino-server-manager)

## Working of the Arduino Code

The code can be segmented into several key functionalities:

1. **Initialization:**
    * Sets up communication with various sensors like DHT22, BME280, rain sensor, and analog air quality sensor.
    * Connects to the specified Wi-Fi network and synchronizes time with an NTP server.
    * Initializes the OLED display and SD card for data visualization and storage.

2. **Sensor Data Acquisition:**
    * Reads sensor values for temperature, humidity, pressure, altitude, air quality, soil moisture, and rainfall.
    * Calculates heat index based on temperature and humidity.

3. **Crop Suitability Analysis:**
    * Accesses a JSON database containing information on various crops and their specific requirements for temperature, humidity, and soil moisture.
    * Compares the collected sensor data with the crop requirements in the database.
    * Identifies crops that fall within the suitable range for the current conditions.

4. **Data Display and Storage:**
    * Presents the collected sensor data, heat index, and identified suitable crops on the OLED display.
    * Logs the sensor data, timestamp, crop suitability information, and Wi-Fi signal strength to an SD card file.

5. **Web Connectivity and Data Transmission:**
    * Connects to a specified web server over Wi-Fi.
    * Converts the collected weather data and crop suitability information into a JSON format.
    * Sends the JSON data to the web server at regular intervals.

This continuous cycle of data acquisition, analysis, display, storage, and transmission allows the Arduino station to function as a comprehensive weather monitoring and crop suitability assessment tool.


## Database Template
```
{
      "name": "Potato",
      "temperature": {
        "min": 15,
        "max": 25
      },
      "humidity": {
        "min": 60,
        "max": 80
      },
      "soil_moisture": {
        "min": 60,
        "max": 80
      },
      "retail_price": {
        "January": 4000,
        "February": 4000,
        "March": 4000,
        "April": 3000,
        "May": 3167,
        "June": 3000,
        "July": 3000,
        "August": 3000,
        "September": 3000,
        "October": 3000,
        "November": 3000,
        "December": 3000
      },
      "wholesale_price": {
        "January": 1675,
        "February": 1198,
        "March": 994,
        "April": 1225,
        "May": 1533,
        "June": 1542,
        "July": 1579,
        "August": 1600,
        "September": 1459,
        "October": 1558,
        "November": 1524,
        "December": 1497
      },
      "months_supported": [
        "November",
        "December",
        "January",
        "February",
      ]
    }
```
