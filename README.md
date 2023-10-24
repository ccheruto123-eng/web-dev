#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 6, 2);

int sensor1 = A0; // Smoke sensor in room 1
int sensor2 = A1; // Smoke sensor in room 2
int sensor3 = A2; // Smoke sensor in room 3
int buzzer = 7; // Buzzer connected to digital pin 8

// 555 timer circuit
int timerIn = 8; // Timer input connected to digital pin 9

void setup() {
 lcd.begin(16, 2);
 pinMode(buzzer, OUTPUT);
 pinMode(timerIn, INPUT);
}

void loop() {


 int smoke1 = analogRead(sensor1); // Read the sensor in room 1
 int smoke2 = analogRead(sensor2); // Read the sensor in room 2
int smoke3 = analogRead(sensor3); // Read the sensor in room 3
 lcd.clear();

if (smoke1 > 500) {
   lcd.setCursor(0, 0);
   lcd.print("Room 1: Fire!");
   digitalWrite(buzzer, HIGH); // Activate the buzzer
   delay(1000); // Wait for 1 second
 }
 else if (smoke2 > 500) {
   lcd.setCursor(0, 0);
   lcd.print("Room 2: Fire!");
   digitalWrite(buzzer, HIGH); // Activate the buzzer
   delay(1000); // Wait for 1 secondelse if (smoke3 > 500) {
   lcd.setCursor(0, 0);
   lcd.print("Room 3: Fire!");
   digitalWrite(buzzer, HIGH); // Activate the buzzer
   delay(1000); // Wait for 1 second
 }
 else {
   lcd.setCursor(0, 0);
   lcd.print("All rooms clear");
   digitalWrite(buzzer, LOW); // Deactivate the buzzer
 }// Activate the buzzer for 5 seconds if the timer input is HIGH
 if (digitalRead(timerIn) == HIGH) {
   digitalWrite(buzzer, HIGH);
   delay(5000); // Wait for 5 seconds
   digitalWrite(buzzer, LOW);
    lcd.setCursor(0, 0);
   lcd.print("Room on Fire!");
 }
}
