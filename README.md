# Gas_leakage_detection

Code for gas leakage detection

#include <LiquidCrystal.h>
LiquidCrystal lcd(5,6,8,9,10,11);


//pin variables
int redled = 3;
int greenled = 2;
int buzzer = 4;
int sensor = A0;
int sensorThresh = 344;


 void setup()
 {
   pinMode(redled,OUTPUT);
   pinMode(greenled,OUTPUT);
   pinMode(buzzer,OUTPUT);
   pinMode(sensor,INPUT);
   Serial.begin(9600);
   lcd.begin(16,2);
 }


void loop()
{
 int analogValue = analogRead(sensor);
  
  Serial.print("GAS VALUE :");
  Serial.println(analogRead(sensor));
  
  //gas concenteration condition
  if(analogValue>sensorThresh)
  {
    digitalWrite(redled,HIGH);
    digitalWrite(greenled,LOW);
    tone(buzzer,1000,10000);
    lcd.clear();
    
    //to print on LCD
    lcd.setCursor(0,1);
    lcd.print("ALERT");
    delay(1000);
    lcd.clear();
    lcd.setCursor(0,1);
    lcd.print("GAS DETECTED");
    delay(1000);
  }
  else
  {
    digitalWrite(greenled,HIGH);
    digitalWrite(redled,LOW);
    noTone(buzzer);
    lcd.clear();
    lcd.setCursor(0,1);
    lcd.print("ALL CLEAR");
    delay(1000);
  }
}