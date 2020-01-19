//ARDUNİO NANO 
//OLedAdafruitDisplay_Scl-A5_Sda-A4_5V
//MP6050_Scl-A5_Sda-A4_5V
 
#include<Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
Adafruit_SSD1306 display;  

const int MPU_addr=0x68; 
int16_t AcX,AcY,AcZ,Tmp,GyX,GyY,GyZ;

int minVal=265; 
int maxVal=402;

double x; 
double y; 
double z;

void setup()
{ 

display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
display.clearDisplay();
Wire.begin(); 
Wire.beginTransmission(MPU_addr);
Wire.write(0x6B); 
Wire.write(0); 
Wire.endTransmission(true); 
Serial.begin(9600); 

} 

void loop()
{

// DISPLAY 

  display.drawLine(0,32,128,32,WHITE);
  display.drawLine(0,40,128,40,WHITE);
  display.drawLine(0,32,0,40,WHITE);
  display.drawLine(127,32,127,40,WHITE);
  

  display.setTextColor(WHITE);
  display.setTextSize(1);
  display.setCursor(21,20);
  display.println("Egim Gostergesi");


  display.setTextColor(WHITE);
  display.setTextSize(1);
  display.setCursor(0,43);
  display.println("Sol");

  display.setTextColor(WHITE);
  display.setTextSize(1);
  display.setCursor(110,43);
  display.println("Sag");


//MAIN CODE

 int dikcizgi = map(y,0,360,0,256);
 display.drawLine(dikcizgi,32,dikcizgi,40,WHITE);
 display.display();
 display.clearDisplay();
 
//MP6050 CODE


  Wire.beginTransmission(MPU_addr); 
  Wire.write(0x3B); 
  Wire.endTransmission(false); 
  Wire.requestFrom(MPU_addr,14,true); 
  AcX=Wire.read()<<8|Wire.read(); 
  AcY=Wire.read()<<8|Wire.read(); 
  AcZ=Wire.read()<<8|Wire.read(); 
  
  int xAng = map(AcX,minVal,maxVal,-90,90); 
  int yAng = map(AcY,minVal,maxVal,-90,90); 
  int zAng = map(AcZ,minVal,maxVal,-90,90);

x= RAD_TO_DEG * (atan2(-yAng, -zAng)+PI); 
y= RAD_TO_DEG * (atan2(-xAng, -zAng)+PI); 
z= RAD_TO_DEG * (atan2(-yAng, -xAng)+PI);


Serial.print("AngleY= "); 
Serial.println(y);
Serial.println(dikcizgi);
Serial.println("--------------------"); 

}
