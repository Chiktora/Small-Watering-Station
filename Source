#include <LiquidCrystal.h>
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

int soil_moisture = 0;
int air_temperature = 0;

void setup()
{
  lcd.begin(16, 2);
  lcd.print("STARTING");
  delay(1000);
  lcd.clear();
  pinMode(A0,INPUT);
  Serial.begin(9600);
  pinMode(8,OUTPUT);
}
void loop()
{
  soil_moisture = map(analogRead(A0),876,0,100,0);
  int reading = analogRead(A2);
  float voltage = reading * 4.68;
  voltage /= 1024.0;
  air_temperature = (voltage - 0.5) * 100;

  Serial.println(soil_moisture);
  Serial.println(air_temperature);
  if(air_temperature < 0)
  {
    lcd.setCursor(0,0);
    lcd.write("Plant forzen ");
  }
  else if (air_temperature > 100)
  {
    lcd.setCursor(0,0);
    lcd.write("Plant burned  ");
  }
  else if(soil_moisture < 60 && air_temperature < 24)
  {
    digitalWrite(8,HIGH);
    lcd.setCursor(0,0);
    lcd.write("Watering    ");
  }
  else
  {
    lcd.setCursor(0,0);
    lcd.write("Monitoring  ");
    digitalWrite(8,LOW);
  }
  lcd.setCursor(0,1);
  lcd.print(air_temperature);
  lcd.print("C");
  lcd.setCursor(6,1);
  lcd.print(soil_moisture);
  lcd.print("%");
    
  delay(10);
}
