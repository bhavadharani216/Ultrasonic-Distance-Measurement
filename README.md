# Ultrasonic-Distance-Measurement
task 2 code:

#include <Servo.h>  // Include the Servo library

// Pin Definitions
const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 6;

// Create a Servo object
Servo myServo;

// Variables for distance measurement
long duration;
int distance;

void setup() {
  // Initialize serial communication
  Serial.begin(9600);
  
  // Set up the pins
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  
  // Attach the servo to the pin
  myServo.attach(servoPin);
}

void loop() {
  // Clear the trigger pin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  // Set the trigger pin HIGH for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the echo pin
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance in cm
  distance = duration * 0.0344 / 2;
  
  // Print the distance
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  // Map distance to servo angle (0 to 180 degrees)
  int servoAngle = map(distance, 0, 100, 0, 180);  // Adjust 100 based on your max distance
  
  // Limit servo angle to 0-180 degrees
  servoAngle = constrain(servoAngle, 0, 180);
  
  // Move the servo
  myServo.write(servoAngle);
  
  // Wait for a bit before next measurement
  delay(500);
}
