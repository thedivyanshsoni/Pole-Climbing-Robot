#include <SoftwareSerial.h>
// Double Motor Side (Output A on L298N)
// Connect the two motors wired in parallel here
const int MOTOR_PAIR_IN1 = 8;
const int MOTOR_PAIR_IN2 = 9;

// Single Motor Side (Output B on L298N)
// Connect the third, single motor here
const int MOTOR_SINGLE_IN3 = 10;
const int MOTOR_SINGLE_IN4 = 11;

// Bluetooth Pins 
// TX of HC-05 goes to Pin 2
// RX of HC-05 goes to Pin 3
const int BT_RX = 2;
const int BT_TX = 3;

SoftwareSerial BTSerial(BT_RX, BT_TX); 

char command; 

void setup() {
  Serial.begin(9600);
  BTSerial.begin(9600); 
  
  pinMode(MOTOR_PAIR_IN1, OUTPUT);
  pinMode(MOTOR_PAIR_IN2, OUTPUT);
  pinMode(MOTOR_SINGLE_IN3, OUTPUT);
  pinMode(MOTOR_SINGLE_IN4, OUTPUT);

  stopRobot();
  
  Serial.println("System Ready. 2+1 Motor Config initialized.");
}

void loop() {
  if (BTSerial.available() > 0) {
    command = BTSerial.read();
    Serial.print("Command: ");
    Serial.println(command); 
    
    
    if (command == 'F') {
      climbUp();
    }
    else if (command == 'B') {
      climbDown();
    }
    else if (command == 'S') {
      stopRobot();
    }
  }
}

void climbUp() {
  // Turn pair of motors Forward
  digitalWrite(MOTOR_PAIR_IN1, HIGH);
  digitalWrite(MOTOR_PAIR_IN2, LOW);
  
  // Turn single motor Forward
  digitalWrite(MOTOR_SINGLE_IN3, HIGH);
  digitalWrite(MOTOR_SINGLE_IN4, LOW);
}

void climbDown() {
  // Turn pair of motors Backward
  digitalWrite(MOTOR_PAIR_IN1, LOW);
  digitalWrite(MOTOR_PAIR_IN2, HIGH);
  
  // Turn single motor Backward
  digitalWrite(MOTOR_SINGLE_IN3, LOW);
  digitalWrite(MOTOR_SINGLE_IN4, HIGH);
}

void stopRobot() {
  digitalWrite(MOTOR_PAIR_IN1, LOW);
  digitalWrite(MOTOR_PAIR_IN2, LOW);
  digitalWrite(MOTOR_SINGLE_IN3, LOW);
  digitalWrite(MOTOR_SINGLE_IN4, LOW);
}
