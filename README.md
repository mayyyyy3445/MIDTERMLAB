# MIDTERMLAB


This circuit connects an Arduino Uno to a photoresistor (LDR) and multiple LEDs, likely for a light-sensitive system.

Components and Connections:
	1.	Arduino Uno – The microcontroller controlling the system.
	2.	LDR (Photoresistor)
	•	Connected to an analog pin (A0 or A1).
	•	One leg connected to 5V.
	•	Other leg connected to GND through a resistor (voltage divider circuit).
	3.	Resistor (near LDR) – Forms a voltage divider to get readable values from the LDR.
	4.	Three LEDs (Red, Yellow, Green):
	•	Each LED is connected to an Arduino digital pin (pins 10, 11, 12).
	•	Resistors in series to limit current.
	5.	Wires
	•	Yellow wires connect LEDs to digital pins.
	•	Green and red wires connect the LDR.

How It Works:
	•	The LDR detects light intensity.
	•	The Arduino reads the LDR’s value from the analog input pin.
	•	Based on the light level, the Arduino controls the LEDs, likely indicating different brightness levels.

Arduino Code Example:

const int ldrPin = A0;  // LDR connected to A0
const int redLED = 12;
const int yellowLED = 11;
const int greenLED = 10;

void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
  Serial.begin(9600);  // Monitor LDR values
}

void loop() {
  int ldrValue = analogRead(ldrPin);  // Read LDR value
  Serial.println(ldrValue);  // Print value to Serial Monitor

  if (ldrValue < 300) {  // Dark environment
    digitalWrite(redLED, HIGH);
    digitalWrite(yellowLED, LOW);
    digitalWrite(greenLED, LOW);
  } else if (ldrValue < 700) {  // Medium light
    digitalWrite(redLED, LOW);
    digitalWrite(yellowLED, HIGH);
    digitalWrite(greenLED, LOW);
  } else {  // Bright light
    digitalWrite(redLED, LOW);
    digitalWrite(yellowLED, LOW);
    digitalWrite(greenLED, HIGH);
  }

  delay(500);  // Small delay for stability
}

