#include <Servo.h>
#define SERVO_PIN 9
#define GROUND_JOY_PIN A5
#define VOUT_JOY_PIN A4
#define XJOY_PIN A3
#define YJOY_PIN A2
#define SJOY_PIN A1
int servo_val;
Servo myservo ;
void setup()
{
 Serial.begin(9600);
 pinMode(VOUT_JOY_PIN, OUTPUT) ;    //pin A4 shall be used as output
 pinMode(GROUND_JOY_PIN, OUTPUT) ;  //pin A5 shall be used as output
 digitalWrite(VOUT_JOY_PIN, HIGH) ; //set pin A4 to high (+5V)
 digitalWrite(GROUND_JOY_PIN,LOW) ; //set pin A5 to low (ground)
 myservo.attach(9);
}
void loop()
{
 delay(200);
 int joystickXVal = analogRead(XJOY_PIN) ;
 servo_val=map(joystickXVal, 4, 1017, 10, 175);
 Serial.print(joystickXVal);
 Serial.println(" = input from joystick");
 Serial.print(servo_val);
 Serial.println(" = output to servo");
 Serial.println() ;
 myservo.write(servo_val);
}
