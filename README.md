# Ultrasonic-Distance-Measurement

const int trigPin = 9;    
const int echoPin = 10;   

void setup() {
  Serial.begin(9600);      
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  long duration;
  float measuredDistance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  
  duration = pulseIn(echoPin, HIGH, 30000);  

  measuredDistance = (duration * 0.034) / 2;

  float distances[] = {50, 100, 150, 200, 250, 300, 350, 400};

  for (int i = 0; i < sizeof(distances) / sizeof(distances[0]); i++) {
    if (distances[i] < 200) {
      Serial.println("Object founded");
    } else if (distances[i] < 300) {
      Serial.println("Object may be founded");
    } else {
      Serial.println("No object founded");
    }
  }

  delay(5000);
}
