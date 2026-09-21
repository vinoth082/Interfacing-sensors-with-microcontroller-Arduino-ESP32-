# Interfacing-sensors-with-microcontroller-Arduino-ESP32
**Exp 1: Interfacing Temperature and Humidity Sensor with ESP32 Using Wokwi**
Aim
To interface a DHT22 temperature and humidity sensor with an ESP32 microcontroller using the Wokwi online simulator, measure the temperature and relative humidity, and display the measured values on the Serial Monitor.
Apparatus / Software Required
Software / Online Tools
•	Wokwi Online Simulator 
•	Web browser 
•	ESP32 simulation board 
•	Arduino C/C++ program 
•	DHT22 sensor model 
Simulated Components
•	ESP32 DevKit
•	DHT22
•	Jumper wires
•	Serial Monitor


Circuit Diagram: 
Students shall design and simulate the circuit using the Wokwi online simulator. Take a clear screenshot of the completed circuit showing all the components and their connections, and include it in this section. The component names, pin connections, and ESP32 GPIO connections should be clearly visible in the screenshot.

<img width="829" height="529" alt="image" src="https://github.com/user-attachments/assets/d389fa05-d41f-4091-bc28-6ebce37a64d0" />


Procedure:
Step-by-step operation
•	ESP32 is powered. 
•	ESP32 initializes the DHT22 sensor. 
•	The DHT22 measures temperature and relative humidity. 
•	The sensor sends digital data to ESP32. 
•	ESP32 reads the data through GPIO 4. 
•	The Arduino program converts the received data into temperature and humidity values. 
•	The values are sent through UART/USB serial communication and appear on the Wokwi Serial Monitor.

Simulation Procedure
Step 1 : Install Wokwi online simulator and Open 
Step 2 : Create a new ESP32 project.
Step 3 : Add ESP32 DevKit, DHT22
Step 5 : Connect the sensor: VCC  → 3.3 V; DATA → GPIO 4; GND  → GND
Step 6 : Open the program editor.
Step 7 :Enter the Arduino C/C++ program.
Step 8 : Make sure the DHT22 library is available in the Wokwi project.
Step 9 : Start Simulation
Step 10 : Open the Serial Monitor and Observe the temperature and humidity values.

Program:
```
/************************************************ 
TITLE: Temperature Monitoring System using ESP32 Microcontroller
SUBMITTED BY: YUVARAJ M
SUBMITTED TO: PROF. ANISH KUMAR, HEMA
*************************************************/

#include <DHT.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define DHTPIN 4
#define DHTTYPE DHT22

#define LED1 2
#define LED2 5
#define LED3 18
#define LED4 19
#define BUZZER 15

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 4);

void setup() {
  lcd.init();         // initialize the LCD
  lcd.backlight();     // turn on backlight
  dht.begin();         // initialize DHT22 sensor
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(LED4, OUTPUT);
  pinMode(BUZZER, OUTPUT);
}

void loop() {
  float temp = dht.readTemperature(); // read temperature data from DHT22
  float hum = dht.readHumidity();     // read humidity data from DHT22

  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temp);
  lcd.print(" C");

  if (temp < 28.0) {
    digitalWrite(LED1, HIGH);
    digitalWrite(LED2, HIGH);
    digitalWrite(LED3, LOW);
    digitalWrite(LED4, LOW);
    tone(BUZZER, 1000); // Start the buzzer at 1 kHz
  } 
  else {
    digitalWrite(LED1, LOW);
    digitalWrite(LED2, LOW);
    digitalWrite(LED3, HIGH);
    digitalWrite(LED4, HIGH);
    noTone(BUZZER); // Stop the buzzer
  }

  lcd.setCursor(0, 1);
  lcd.print("Humidity: ");
  lcd.print(hum);
  lcd.print(" %");
  lcd.setCursor(0, 2);
  lcd.print("Created By:");
  lcd.setCursor(0, 3);
  lcd.print("YUVARAJ M");
}
```
Output:
<img width="1903" height="832" alt="image" src="https://github.com/user-attachments/assets/a91d8a5b-7172-4974-8485-c1bf302ebfc7" />

<img width="1918" height="879" alt="image" src="https://github.com/user-attachments/assets/5b2ce277-48e1-437e-bbd8-db73793685db" />


Result:
Thus, the DHT22 temperature and humidity sensor was successfully interfaced with the ESP32 microcontroller using the Wokwi online simulation platform. 
