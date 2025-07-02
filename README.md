# V2V-communication-transmitter-
#include <SoftwareSerial.h>

SoftwareSerial hc12(10, 11); // RX, TX

int speedPin = A0;
int speedValue = 0;
int prevSpeed = 0;
bool isBraking = false;

void setup() {
  Serial.begin(9600);
  hc12.begin(9600);
}

void loop() {
  speedValue = analogRead(speedPin) / 4; // Map to 0-255

  if (speedValue < prevSpeed - 10) {
    isBraking = true;
  } else {
    isBraking = false;
  }

  String data = String(speedValue) + "," + String(isBraking);
  hc12.println(data);
  Serial.println("Sent: " + data);

  prevSpeed = speedValue;
  delay(500);
}
