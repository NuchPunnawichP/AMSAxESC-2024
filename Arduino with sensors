// Varaible for esp communication
#include <SoftwareSerial.h>
SoftwareSerial Uno(3, 2); // RX | TX
int led = 13;

// Temp variable
int val = 0;
int tempPin = A0;

// Oximeter
#include <Wire.h>
#include "MAX30100_PulseOximeter.h"
 
#define REPORTING_PERIOD_MS     1000
 
PulseOximeter pox;
uint32_t tsLastReport = 0;

// Setting zero
float temp = 0;
int bpm = 0;
int oxi = 0;

void onBeatDetected()
{
    Serial.println("Beat!");
}

// Starting setup
void setup()
{
  pinMode(3, INPUT);
  pinMode(2, OUTPUT);
  pinMode(led, OUTPUT);

  Serial.begin(9600);
  Uno.begin(9600);
/*
  Serial.print("Initializing pulse oximeter..");

  if (!pox.begin())
  {
      Serial.println("FAILED");
      for(;;);
  }
  else
  {
    Serial.println("SUCCESS");
  }
*/
  pox.setIRLedCurrent(MAX30100_LED_CURR_7_6MA);

  pox.setOnBeatDetectedCallback(onBeatDetected);
}

void loop()
{
  pox.update();
  if (millis() - tsLastReport > 3000)
  {
    Uno.println(temp);
    Uno.println(bpm);
    Uno.println(oxi);

    tsLastReport = millis();
  }
  else
  {
    temp = TempCH();
    bpm = heartCH();
    oxi = oxiCH();
  }
}

float TempCH()
{
  val = analogRead(tempPin);
  
  float mv = ( val / 1024.0) * 5000;
  float cel = mv / 10;
  
  return cel;
}

int heartCH()
{
  return pox.getHeartRate();
}

int oxiCH()
{
  return pox.getSpO2();
}
