#include <Wire.h>
#include <Adafruit_INA219.h>

Adafruit_INA219 ina219;

float voltage = 0.0;
float current_mA = 0.0;
float power_mW = 0.0;
float capacity_Ah = 0.0;

unsigned long lastTime = 0;

void setup() {
  Serial.begin(9600);

  if (!ina219.begin()) {
    Serial.println("INA219 не е открит!");
    while (1);
  }

  lastTime = millis();
}

void loop() {
  unsigned long now = millis();
  float hours = (now - lastTime) / 3600000.0;
  lastTime = now;

  voltage = ina219.getBusVoltage_V();
  current_mA = ina219.getCurrent_mA();
  power_mW = ina219.getPower_mW();

  capacity_Ah += (current_mA / 1000.0) * hours;

  Serial.println("----- Battery Monitor -----");
  Serial.print("Voltage: ");
  Serial.print(voltage);
  Serial.println(" V");

  Serial.print("Current: ");
  Serial.print(current_mA);
  Serial.println(" mA");

  Serial.print("Power: ");
  Serial.print(power_mW);
  Serial.println(" mW");

  Serial.print("Used capacity: ");
  Serial.print(capacity_Ah, 4);
  Serial.println(" Ah");

  delay(1000);
}
