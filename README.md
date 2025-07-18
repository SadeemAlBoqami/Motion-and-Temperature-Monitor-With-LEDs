# Motion-and-Temperature-Monitor-With-LEDs
To create a simple system that detects both motion and temperature using two sensors, and provides visual feedback via two LEDs.

## Project Description:
This Arduino project combines a digital motion sensor (PIR) and an analog temperature sensor (LM35) to control two LEDs:
- LED1 lights up when motion is detected.
- LED2 lights up when temperature exceeds a threshold (e.g., 30°C).
- Data is printed to the Serial Monitor for real-time feedback.

  ## Components Used:

 | Component                   | Quantity  |
| --------------------------- | --------- |
| Arduino Uno                 | 1         |
| PIR Motion Sensor           | 1         |
| LM35 Temperature Sensor     | 1         |
| LED (Red for temperature)   | 1         |
| LED (Green for motion)      | 1         |
| 220Ω Resistor               | 2         |
| Breadboard                  | 1         |
| Jumper Wires                | As needed |


## Wiring Instructions:
1. PIR Motion Sensor:
* VCC → 5V
* GND → GND
* OUT → D2

2. LM35 Temperature Sensor:
* VCC → 5V
* GND → GND
* OUT → A0

3- LED1 (Temperature LED):
* Anode (+) → D12
* Cathode (–) → 220Ω → GND

4- LED2 (Motion LED):
* Anode (+) → D13
* Cathode (–) → 220Ω → GND

## Arduino Code:
```cpp
int pirPin = 2;           // PIR motion sensor connected to digital pin 2
int tempPin = A0;         // LM35 temperature sensor connected to analog pin A0
int ledTemp = 12;       // LED1 for temperature warning connected to digital pin 12
int ledMotion = 13;         // LED2 for motion indicator connected to digital pin 13

void setup() {
  pinMode(pirPin, INPUT);         // Set PIR pin as input
  pinMode(ledMotion, OUTPUT);     // Set motion LED as output
  pinMode(ledTemp, OUTPUT);       // Set temperature LED as output
  Serial.begin(9600);             // Initialize serial communication
}

void loop() {
  // Read motion sensor
  int motion = digitalRead(pirPin);

  // Read temperature sensor (LM35)
  int value = analogRead(tempPin);
  float voltage = value * (5.0 / 1023.0);     // Convert analog value to voltage
  float temperature = voltage * 100;          // Convert voltage to °C

  // Display temperature
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  // Motion detection
  if (motion == HIGH) {
    digitalWrite(ledMotion, HIGH);           // Turn ON motion LED
    Serial.println("Motion Detected!");
  } else {
    digitalWrite(ledMotion, LOW);            // Turn OFF motion LED
  }

  // Temperature threshold check
  if (temperature >= 30.0) {
    digitalWrite(ledTemp, HIGH);             // Turn ON temperature LED
  } else {
    digitalWrite(ledTemp, LOW);              // Turn OFF temperature LED
  }

  delay(1000);  // Wait for 1 second
}
```
You can tinker this from here: https://www.tinkercad.com/things/lto5iY1Jdk9-motion-and-temperature-monitor-with-leds/editel?returnTo=%2Fdashboard%2Fdesigns%2Fcircuits&sharecode=IZxFwKLmfBxaA56MuB3s8wc4B8i6f3r7cA8Y-AsD6SI

