# -#include <Wire.h>
#include <Adafruit_INA219.h>

Adafruit_INA219 ina219;

// Променливи
float busVoltage = 0.0;
float current_mA = 0.0;
float power_mW = 0.0;

float capacity_Ah = 0.0;
unsigned long lastTime = 0;

void setup() {
  Serial.begin(9600);
  while (!Serial) { delay(1); }

  if (!ina219.begin()) {
    Serial.println("ГРЕШКА: INA219 не е открит!");
    while (1);
  }

  Serial.println("Система за следене на батерия стартирана");
  lastTime = millis();
}

void loop() {
  unsigned long currentTime = millis();
  float deltaTime = (currentTime - lastTime) / 3600000.0; // време в часове
  lastTime = currentTime;

  // Четене от INA219
  busVoltage = ina219.getBusVoltage_V();
  current_mA = ina219.getCurrent_mA();
  power_mW = ina219.getPower_mW();

  // Изчисляване на консумация (Ah)
  capacity_Ah += (current_mA / 1000.0) * deltaTime;

  // Извеждане в Serial Monitor
  Serial.println("----------------------------");
  Serial.print("Напрежение: ");
  Serial.print(busVoltage);
  Serial.println(" V");

  Serial.print("Ток: ");
  Serial.print(current_mA);
  Serial.println(" mA");

  Serial.print("Мощност: ");
  Serial.print(power_mW);
  Serial.println(" mW");

  Serial.print("Консумация: ");
  Serial.print(capacity_Ah, 4);
  Serial.println(" Ah");

  delay(1000);
}
