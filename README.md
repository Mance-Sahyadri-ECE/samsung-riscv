#include <Arduino.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET    -1
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// Sensor Pin Definitions
#define TEMP_SENSOR_PIN A0  // LM35 Temperature Sensor
#define LDR_SENSOR_PIN A1   // Light Sensor (LDR)

// Calibration Factors
#define TEMP_SENSOR_VOLTAGE 3.3
#define ADC_RESOLUTION 1024.0

void setup() {
    Serial.begin(9600);  // Start Serial communication

    // Initialize OLED Display
    if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
        Serial.println("SSD1306 OLED display failed to initialize!");
        for (;;);
    }
    
    display.clearDisplay();
    display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(10, 10);
    display.println("Temperature & Light Monitoring");
    display.display();
    delay(2000);
}

void loop() {
    // Read Temperature Sensor (LM35)
    int tempValue = analogRead(TEMP_SENSOR_PIN);
    float temperature = (tempValue * TEMP_SENSOR_VOLTAGE / ADC_RESOLUTION) * 100;  // Convert to °C

    // Read Light Sensor (LDR)
    int lightValue = analogRead(LDR_SENSOR_PIN);
    float lightPercentage = (lightValue / ADC_RESOLUTION) * 100.0;  // Convert to percentage

    // Display values on Serial Monitor
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.print(" °C | Light Level: ");
    Serial.print(lightPercentage);
    Serial.println(" %");

    // Display values on OLED
    display.clearDisplay();
    display.setTextSize(2);
    display.setCursor(0, 0);
    display.print("Temp: ");
    display.print(temperature);
    display.println("C");

    display.setCursor(0, 30);
    display.print("Light: ");
    display.print(lightPercentage);
    display.println("%");

    display.display();

    delay(1000);  // Update every second
}
