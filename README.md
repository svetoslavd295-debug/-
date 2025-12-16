<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  
</head>
<body>

<header>
  <h1>🔋 Battery Monitoring System</h1>
  <p>Battery monitoring using ammeter (INA219)</p>
</header>

<section>
  <h2>📌 Project Description</h2>
  <p>
    This project is a battery monitoring system that measures voltage,
    current, and power using an INA219 ammeter and an Arduino-compatible
    microcontroller.
  </p>

  <h2>⚙️ Hardware Used</h2>
  <ul>
    <li>Arduino Uno / Nano</li>
    <li>INA219 Ammeter</li>
    <li>Battery (Li-ion / 12V)</li>
    <li>Jumper wires</li>
  </ul>

  <h2>🔌 Wiring</h2>
  <table>
    <tr>
      <th>INA219</th>
      <th>Arduino</th>
    </tr>
    <tr>
      <td>VCC</td>
      <td>5V</td>
    </tr>
    <tr>
      <td>GND</td>
      <td>GND</td>
    </tr>
    <tr>
      <td>SDA</td>
      <td>A4</td>
    </tr>
    <tr>
      <td>SCL</td>
      <td>A5</td>
    </tr>
  </table>

  <h2>💻 Example Arduino Code</h2>
  <pre><code>
#include &lt;Wire.h&gt;
#include &lt;Adafruit_INA219.h&gt;

Adafruit_INA219 ina219;

float capacity_Ah = 0.0;
unsigned long lastTime = 0;

void setup() {
  Serial.begin(9600);
  ina219.begin();
  lastTime = millis();
}

void loop() {
  unsigned long now = millis();
  float hours = (now - lastTime) / 3600000.0;
  lastTime = now;

  float voltage = ina219.getBusVoltage_V();
  float current = ina219.getCurrent_mA();

  capacity_Ah += (current / 1000.0) * hours;

  Serial.print("Voltage: ");
  Serial.print(voltage);
  Serial.println(" V");

  Serial.print("Current: ");
  Serial.print(current);
  Serial.println(" mA");

  Serial.print("Capacity: ");
  Serial.print(capacity_Ah);
  Serial.println(" Ah");

  delay(1000);
}
  </code></pre>

  <h2>🚀 Future Improvements</h2>
  <ul>
    <li>OLED display</li>
    <li>Web dashboard</li>
    <li>Data logging</li>
    <li>Low battery alert</li>
  </ul>
</section>

<footer>
  <p>MIT License | Created for GitHub</p>
</footer>

</body>
</html>
