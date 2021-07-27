# Ultrasonic sensor to control LCD and robot arm
Using ultrasonic sensor to detect any moving object in the range of 100 cm to feel if there are people in front of the robot if there are, the LCD will turn on and the robot arm will move.

 ## Components
 - 1 Ultrasonic distance sensor
 - 1 Potentiometer
 - 1 Arduino Uno R3
 - Breadbaourd
 - 4 servo motors
 - 1 LCD 2x16
 
 ## C++ Code 
  the code that used in the circuit is:
  ```javascript
// C++ code
//
#include <LiquidCrystal.h>
#include <Servo.h>
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);
Servo myservo;
Servo myservo1;
Servo myservo2;
Servo myservo3;

int dist = 0;



long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);
  lcd.begin(16, 2);
  lcd.print("Distance:");
  lcd.setCursor(0,1);
  lcd.print(" Hello ");
  

}

void loop()
{
  dist = 0.01723 * readUltrasonicDistance(10, 9);
  Serial.println(dist);
  if (dist < 100)
 {
  lcd.setCursor(11, 0);
  lcd.print(int(dist));
  digitalWrite(13, HIGH);
    
  myservo.attach(11);
  myservo.write(180);
    
  myservo1.attach(12);
  myservo1.write(180); 
  
  myservo2.attach(13);
  myservo2.write(180);
    
  myservo3.attach(A0);
  myservo3.write(180);
  delay(10); // Delay a little bit to improve simulation performance
}
  else
  {
  lcd.setCursor(11, 0);
  lcd.print("0");

  myservo.attach(11);
  myservo.write(0);
    
  myservo1.attach(12);
  myservo1.write(0); 
  
  myservo2.attach(13);
  myservo2.write(0);
    
  myservo3.attach(A0);
  myservo3.write(0);
  }

}

```
## Program
The program that used to do the circuit and the code is TINKERCAD.

## Tinkercad program link.
https://www.tinkercad.com/things/74vAfrKpCeT-copy-of-lcd-ultrasonic-sensor/editel
