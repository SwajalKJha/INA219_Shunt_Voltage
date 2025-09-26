#include <Wire.h>
#include <Adafruit_INA219.h>

Adafruit_INA219 ina219;

const float max_shunt_mV = 50.0;  // Max expected shunt voltage (50 mV = 100%)

void setup() {
    Serial.begin(115200);
    while (!Serial);

    if (!ina219.begin()) {
        Serial.println("Failed to find INA219 chip");
        while (1);
    }

    Serial.println("INA219 initialized");
}

void loop() {
    float shuntVoltage = ina219.getShuntVoltage_mV();

    // Take absolute value to handle reverse current direction (e.g., battery input)
    shuntVoltage = abs(shuntVoltage);

    // Use float math for percentage calculation
    float percentage = (shuntVoltage / max_shunt_mV) * 100.0;

    // Limit percentage to avoid 250%+ errors
    percentage = constrain(percentage, 0.0, 99.99);

    Serial.print("Shunt Voltage: ");
    Serial.print(shuntVoltage, 3);
    Serial.println(" mV");

    Serial.print("Mapped Percentage: ");
    Serial.print(percentage, 2);
    Serial.println(" %");

    Serial.println();

    delay(1000);  // 1 second delay
}
