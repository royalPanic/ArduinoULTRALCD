# Arduino LCD and Ultrasonic Sensor
## Connections:
The HC-SR04 Ultrasonic Module has 4 pins, **Ground**, **VCC**, **Trig** and **Echo**. The Ground and the VCC pins of the module needs to be connected to the Ground and the 5 volt pins on the Arduino Board respectively and the trig and echo pins to any Digital I/O pin on the Arduino Board.

* The HC-SR04 sensor attached to the Breadboard
* The Sensor VCC connected to the Arduino Board +5V
* The Sensor GND connected to the Arduino Board GND
* The Sensor Trig connected to the Arduino Board Digital I/O 9
* The Sensor Echo connected to the Arduino Board Digital I/O 10

Watch the basic tutorial about the HC-SR04:
[Youtube](https://youtu.be/vTjJDeDJmsA)

---

## LCD Display Connection:
*Before wiring the LCD screen to your Arduino or Genuino board we suggest to solder a pin header strip to the 14 (or 16) pin count connector of the LCD screen.
To wire your LCD screen to your board, connect the following pins*

* LCD VSS pin to Arduino GND
* LCD VDD pin to Arduino 5V
* LCD VO pin to 10k Potentiometer center pin
* LCD RS pin to digital pin 1
* LCD RW pin to Arduino GND
* LCD Enable pin to digital pin 2
* LCD D4 pin to digital pin 4
* LCD D5 pin to digital pin 5
* LCD D6 pin to digital pin 6
* LCD D7 pin to digital pin 7
* The 10k Potentiometer’s other legs connect to +5V and GND
* For the backlight of the display, pin 15 (A+) and 16 (K-) of the LCD connect to +5V and GND

If you want, can be use a 220 ohm resistor to power the backlight of the display.

Watch the basic tutorial about the LCD Display:
[Youtube](https://youtu.be/cxNBlD5c8zI)

---
```c
#include <LiquidCrystal.h>
LiquidCrystal lcd(1, 2, 4, 5, 6, 7); // Creates an LCD object. Parameters: (rs, enable, d4, d5, d6, d7)
const int trigPin = 9;
const int echoPin = 10;
long duration;
int distanceCm, distanceInch;
void setup() {
    lcd.begin(16,2); // Initializes the interface to the LCD screen, and specifies the dimensions (width and height) of the display
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}
void loop() {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    duration = pulseIn(echoPin, HIGH);
    distanceCm= duration*0.034/2;
    distanceInch = duration*0.0133/2;
    lcd.setCursor(0,0); // Sets the location at which subsequent text written to the LCD will be displayed
    lcd.print("Distance: "); // Prints string "Distance" on the LCD
    lcd.print(distanceCm); // Prints the distance value from the sensor
    lcd.print("  cm");
    delay(10);
    lcd.setCursor(0,1);
    lcd.print("Distance: ");
    lcd.print(distanceInch);
    lcd.print("inch");
    delay(10);
}
```
