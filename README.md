#include <Servo.h>
Servo servo1; // servo pin for horizontal movement
Servo servo2; // servo pin for vertical movement
Servo servo3; // servo pin claw

int x_key = A1; // assign "X" axis of joystick to pin A0                                               
int y_key = A0; // assign "Y" axis of joystick to pin A1                                                
int x_pos; // variable to read x position from joystick
int y_pos; // variable to read y position from joystick
int button_pin = 12; // assign button pin 12


const int servo2_pin = 9; // vertical servo connected to pin 9
const int servo1_pin = 8; // horizontal servo connected to pin 8
const int servo3_pin = 7; // button servo connected to pin 7
int initial_position = 90; // variable for servo movement
int initial_position1 = 90; // variable for servo movement
int buttonState = 0; // variable to hold button on/off





void setup ( ) {
Serial.begin (9600) ;
servo1.attach (servo1_pin ) ; 
servo2.attach (servo2_pin ) ;
servo3.attach (servo3_pin); // button servo
servo1.write (initial_position);
servo2.write (initial_position1);
pinMode (x_key, INPUT) ;                     
pinMode (y_key, INPUT) ;

// Set up the pushbutton pins to be an input:
pinMode(button_pin, INPUT_PULLUP);
}

void loop ( ) {
// local variable to hold the pushbutton states  
//read the digital state of buttonPin with digitalRead() function and store the 
//value in buttonState variable
  buttonState = digitalRead(button_pin);  
  
x_pos = analogRead (x_key) ;  
y_pos = analogRead (y_key) ;                      

if (x_pos < 300){
  if (initial_position < 10) { } else{ initial_position = initial_position - 20; 
  servo1.write ( initial_position ) ;
  delay (100) ;
  }
}

if (x_pos > 700){
  if (initial_position > 180)
  {  
  }  
  else{
  initial_position = initial_position + 20;
  servo1.write ( initial_position ) ;
  delay (100) ;
  }
}

if (y_pos < 300){
  if (initial_position1 < 10) { } else{ initial_position1 = initial_position1 - 20;
  servo2.write ( initial_position1 );
  delay (100);
}
}

if (y_pos > 700){
if (initial_position1 > 180)
{  
}
else{
initial_position1 = initial_position1 + 20;
servo2.write ( initial_position1 ) ;
delay (100) ;
}
}

//if the button is pressed increment counter and wait a tiny bit to give us some time to release the button
  if (buttonState == LOW) // light the LED
  {
    servo3.write (180);
  }
  if (buttonState == HIGH) 
  {
    servo3.write (0);
  }
  
  
}

