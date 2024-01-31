#include <Adafruit_ADS1015.h>
#include "HX711.h"

Adafruit_ADS1115 ads1(0x49);
String adcString[8];
HX711 scale;

const int LOADCELL_DOUT_PIN = 33;
const int LOADCELL_SCK_PIN = 32;

void setup() {
  Serial.begin(115200);

  Serial.println("HX711 Demo");
  Serial.println("Initializing the scale");

  // Initialize library with data output pin, clock input pin, and gain factor.
  scale.begin(LOADCELL_DOUT_PIN, LOADCELL_SCK_PIN);
  pinMode(36, INPUT);    // Analog input-battery voltage monitor
  
  Serial.println("Before setting up the scale:");
  Serial.print("read: \t\t");
  Serial.println(scale.read());  // print a raw reading from the ADC

  // Additional setup for analog inputs
  Wire.begin(16, 17);
  ads1.begin();
  ads1.setGain(GAIN_ONE);
  Serial.println("The device is powered up");
  Serial.println("Initialized analog inputs");
}

void loop() {
  Serial.print("one reading:\t");
  Serial.print(scale.get_units(), 1);
  Serial.print("\t| average:\t");
  Serial.println(scale.get_units(10), 1);

  scale.power_down();  // put the ADC in sleep mode

  delay(800);

  scale.power_up();

  // Additional code for analog inputs
  Serial.print("I1: ");
  Serial.println(digitalRead(35));
  Serial.print("I2: ");
  Serial.println(digitalRead(34));
  Serial.print("Battery Voltage: ");
  Serial.println(readBattery());
  delay(800);
  printanalog();
  delay(800);
}

int readBattery() {
  unsigned int analog_value;
  analog_value = analogRead(36);
  return analog_value;
}

void printanalog() {
  for (int i = 0; i < 4; i++) {
    adcString[i] = String(ads1.readADC_SingleEnded(i));
    adcString[i] = String(ads1.readADC_SingleEnded(i));
    delay(10);
    Serial.print("A" + String(i + 1) + ": ");
    Serial.print(adcString[i]);
    Serial.print("  ");
  }

  Serial.println("____________________________________");
}
