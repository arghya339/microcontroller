```ino
#include <Wire.h>
#include <MPU6050.h>  // INSTALL MPU6050 by Electronic Cats Library from Arduino IDE

MPU6050 mpu;

void setup() {
  Serial.begin(115200);
  Wire.begin(13, 14);  // SDA=GPIO13, SCL=GPIO14, GND=GND, VCC=3V3
  
  Serial.println("Initializing MPU-6050...");
  mpu.initialize();
  
  if (mpu.testConnection()) {
    Serial.println("MPU-6050 connection successful!");
  } else {
    Serial.println("MPU-6050 connection failed!");
    while(1);
  }
}

void loop() {
  int16_t ax, ay, az, gx, gy, gz;
  float temperature;  // Variable for temperature
  
  // Get motion data
  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
  
  // Get temperature (in Celsius)
  temperature = mpu.getTemperature();
  
  // Print all data
  Serial.print("Temp: ");
  Serial.print(temperature);
  Serial.print(" °C | ");
  Serial.print("a: ");
  Serial.print(ax); Serial.print(", ");
  Serial.print(ay); Serial.print(", ");
  Serial.print(az); Serial.print(" | ");
  Serial.print("g: ");
  Serial.print(gx); Serial.print(", ");
  Serial.print(gy); Serial.print(", ");
  Serial.println(gz);
  
  delay(100);
}
```