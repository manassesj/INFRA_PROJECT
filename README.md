# INFRA_PROJECT

#include <Arduino.h>
#include <jLed.h>
#define BLYNK_PRINT Serial


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "YourAuthToken";

char ssid[] = "YourNetworkName";
char pass[] = "YourPassword";

auto led = JLed(LED_BUILTIN);

BLYNK_WRITE(V1){
  led.Blink(900,100).Forever();
}
BLYNK_WRITE(V2){
  led.Blink(500,500).Forever();
}
BLYNK_WRITE(V3){
  led.Breathe(2000).DelayAfter(1000).Forever();
}
BLYNK_WRITE(V4){
  int slider = param.asInt();
  led.Off();
  analogWrite(LED_BUILTIN,slider);
}
void setup()
{
  Serial.begin(9600);
  Blynk.begin(auth, ssid, pass);

}

void loop()
{
  Blynk.run();
  led.Update();

}

