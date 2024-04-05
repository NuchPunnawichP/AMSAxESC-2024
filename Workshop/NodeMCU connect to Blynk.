// Blynk setting
#define BLYNK_TEMPLATE_ID "TMPL6vbh9Q5gv"
#define BLYNK_TEMPLATE_NAME "SmartPatientSystem"
#define BLYNK_AUTH_TOKEN "GM61QhAFk6lNLMSi1L3PMXWknMJwV-Vx"

// Set password to "" for open networks.
char ssid[] = "AMSAxESC";
char pass[] = "55555555";

// ESP Module
#include <ESP8266WiFi.h>
#include <SoftwareSerial.h>
#include <BlynkSimpleEsp8266.h>

SoftwareSerial NodeMCU(D2, D3); // RX | TX

int ch = 1;

void setup()
{
  //Connect to Blynk
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  Blynk.virtualWrite(V3, HIGH);
  Blynk.setProperty(V3, "color", "#90EE90");

  pinMode(D2, INPUT);
  pinMode(D3, OUTPUT);
  Serial.begin(9600);
  NodeMCU.begin(9600);
}

void loop()
{
  Blynk.run();

  float temp = NodeMCU.parseFloat();
  //Serial.print("Temp: ");
  //Serial.println(temp);

  int bpm = NodeMCU.parseInt();
  //Serial.print("bpm: ");
  //Serial.print(bpm);

  int ox = NodeMCU.parseInt();
  //Serial.print(" / OX: ");
  //Serial.println(ox);

  Blynk.virtualWrite(V0, bpm); //send the heart rate value to Blynk
  Blynk.virtualWrite(V1, ox); //send the heart rate value to Blynk
  Blynk.virtualWrite(V2, temp); //send temperature value to Blynk

  // Check if patient is going to die
  if(bpm > 150 or ox < 90 or temp > 40 and ch)
  {
    //#D3435C - Blynk RED 
    Blynk.setProperty(V3, "color", "#D3435C");
    ch = 0;
  }
  else if(!ch)
  {
    //#D3435C - Blynk GREEN 
    Blynk.setProperty(V3, "color", "#90EE90");
    ch = 1;
  }
 
  delay(3000);
}
