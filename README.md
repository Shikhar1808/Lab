# EDP LAB
### Blinking of LEDs
```
const int ledPins[] = {3, 4, 5}; // Define LED pins
const int numLeds = 3; // Number of LEDs

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(ledPins[i], HIGH);
    delay(500);
    digitalWrite(ledPins[i], LOW);
    delay(500);
  }
}

```

### WAP to design an odd-even pattern and then perform the reverse operation also. For example- Sequence = 1 3 5 2 4 --- 4 2 5 3 1
```
const int numElements = 5;
int sequence[numElements];  // Array to store pattern

void setup() {
  Serial.begin(9600);
  
  // Step 1: Generate Odd-Even Pattern
  int oddIndex = 0, evenIndex = (numElements + 1) / 2;
  
  for (int i = 1, index = 0; i <= numElements; i++) {
    if (i % 2 != 0) {
      sequence[oddIndex++] = i; // Store odd numbers first
    } else {
      sequence[evenIndex++] = i; // Store even numbers next
    }
  }

  // Step 2: Print Original Sequence
  Serial.print("Original Sequence: ");
  printArray(sequence, numElements);

  // Step 3: Reverse the Sequence
  reverseArray(sequence, numElements);

  // Step 4: Print Reversed Sequence
  Serial.print("Reversed Sequence: ");
  printArray(sequence, numElements);
}

void loop() {
  // Nothing in loop, runs only once
}

// Function to print array
void printArray(int arr[], int size) {
  for (int i = 0; i < size; i++) {
    Serial.print(arr[i]);
    Serial.print(" ");
  }
  Serial.println();
}

// Function to reverse array
void reverseArray(int arr[], int size) {
  for (int i = 0; i < size / 2; i++) {
    int temp = arr[i];
    arr[i] = arr[size - 1 - i];
    arr[size - 1 - i] = temp;
  }
}
```

### WAP to blink multiple LEDs for exactly 3 times. (Avoid writing the whole code in void  setup). 
```
const int ledPins[] = {3, 4, 5};  // Define LED pins
const int numLeds = sizeof(ledPins) / sizeof(ledPins[0]);
int blinkCount = 0;  // Counter for blinks

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  if (blinkCount < 3) {  // Blink LEDs only 3 times
    for (int i = 0; i < numLeds; i++) {
      digitalWrite(ledPins[i], HIGH);
    }
    delay(500);

    for (int i = 0; i < numLeds; i++) {
      digitalWrite(ledPins[i], LOW);
    }
    delay(500);
    
    blinkCount++;  // Increment blink counter
  } else {
    // Stop blinking after 3 cycles
    while (true);  // Infinite loop to stop further execution
  }
}
```

### 7 WAP to perform dimmer effect for multiple LEDs: 
#### a) Using for loop 
#### b) Using user input 
```
//a
const int ledPins[] = {3, 5, 6};  // PWM pins for LEDs
const int numLeds = sizeof(ledPins) / sizeof(ledPins[0]);

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // Increasing brightness
  for (int brightness = 0; brightness <= 255; brightness += 5) {
    for (int i = 0; i < numLeds; i++) {
      analogWrite(ledPins[i], brightness);
    }
    delay(30);
  }

  // Decreasing brightness
  for (int brightness = 255; brightness >= 0; brightness -= 5) {
    for (int i = 0; i < numLeds; i++) {
      analogWrite(ledPins[i], brightness);
    }
    delay(30);
  }
}

```
```
//b
const int ledPins[] = {3, 5, 6};  // PWM pins for LEDs
const int numLeds = sizeof(ledPins) / sizeof(ledPins[0]);
int brightness = 0;  // Variable for user input

void setup() {
  Serial.begin(9600);
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
  Serial.println("Enter brightness (0-255):");
}

void loop() {
  if (Serial.available() > 0) {
    brightness = Serial.parseInt();  // Read user input
    brightness = constrain(brightness, 0, 255);  // Ensure valid range

    // Set brightness for all LEDs
    for (int i = 0; i < numLeds; i++) {
      analogWrite(ledPins[i], brightness);
    }

    Serial.print("Brightness set to: ");
    Serial.println(brightness);
  }
}

```

### WAP to show dimmer effect where LED 1 should display values between 1-50
#### LED 2 = 51-100
#### LED 3 = 101-150
#### LED 4 = 151-200
#### LED 5 = 201-255
```
const int ledPins[] = {3, 5, 6, 9, 10};  // PWM pins for LEDs
const int brightnessMin[] = {1, 51, 101, 151, 201};  // Minimum brightness for each LED
const int brightnessMax[] = {50, 100, 150, 200, 255}; // Maximum brightness for each LED
const int numLeds = sizeof(ledPins) / sizeof(ledPins[0]);

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // Increasing brightness for each LED
  for (int level = 0; level <= 100; level++) {
    for (int i = 0; i < numLeds; i++) {
      int brightness = map(level, 0, 100, brightnessMin[i], brightnessMax[i]);
      analogWrite(ledPins[i], brightness);
    }
    delay(30);
  }

  // Decreasing brightness for each LED
  for (int level = 100; level >= 0; level--) {
    for (int i = 0; i < numLeds; i++) {
      int brightness = map(level, 0, 100, brightnessMin[i], brightnessMax[i]);
      analogWrite(ledPins[i], brightness);
    }
    delay(30);
  }
}

```

### Buggy Movement
#### Infrared 
```
int r1, r2, r3, r4;
void setup() {
Serial.begin(9600);
pinMode(A1,INPUT);
pinMode(A3,INPUT);

pinMode(5,OUTPUT);
pinMode(6,OUTPUT);
pinMode(7,OUTPUT);
pinMode(8,OUTPUT);
}

void loop() {
r1=analogRead(A1);
r2=analogRead(A3);
r3=digitalRead(A1);
r4=digitalRead(A3);
Serial.println(r1);
Serial.print("\t");
Serial.println(r2);
Serial.print("\t");
Serial.println(r3);
Serial.print("\t");
Serial.println(r4);

   if(r1==LOW&&r2==LOW)
    {
      digitalWrite(5,HIGH);
      digitalWrite(6,LOW);
      digitalWrite(7,LOW);
      digitalWrite(8,HIGH);
      
    }
     if(r1==HIGH&&r2==LOW)
    {
      digitalWrite(5,HIGH);
      digitalWrite(6,LOW);
      digitalWrite(7,HIGH);
      digitalWrite(8,LOW);
      
    }
  if(r1==LOW&&r2==HIGH)
    {
      digitalWrite(5,LOW);
      digitalWrite(6,HIGH);
      digitalWrite(7,LOW);
      digitalWrite(8,HIGH);
     }
     if(r1==HIGH&&r2==HIGH)
    {
      digitalWrite(5,HIGH);
      digitalWrite(6,LOW);
      digitalWrite(7,LOW);
      digitalWrite(8,HIGH);
     }
     digitalWrite(5,LOW);
      digitalWrite(6, LOW);
      digitalWrite(7, LOW);
      digitalWrite(8,LOW);
}
```

#### Ultrasonic
```
const int trigPin = 13;
const int echoPin = 12;
long duration;
int distanceCm, distanceInch;

const int rightForward = 5;
const int rightBackward = 6;
const int leftBackward = 7;
const int leftForward = 8;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
  
  pinMode(rightForward, OUTPUT);
  pinMode(rightBackward, OUTPUT);
  pinMode(leftBackward, OUTPUT);
  pinMode(leftForward, OUTPUT);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  distanceCm = (duration * 0.034) / 2;
  distanceInch = (duration * 0.0133) / 2;
  Serial.println(distanceCm);

  if (distanceCm < 30) { // Object detected within 30 cm
    stopCar();
    delay(500);
    reverseCar();
    delay(500);
    turnLeft(); // Adjust to turn right if needed
    delay(500);
  } else {
    moveForward();
  }
}

void moveForward() {
  digitalWrite(rightForward, HIGH);
  digitalWrite(leftForward, HIGH);
  digitalWrite(rightBackward, LOW);
  digitalWrite(leftBackward, LOW);
}

void stopCar() {
  digitalWrite(rightForward, LOW);
  digitalWrite(leftForward, LOW);
  digitalWrite(rightBackward, LOW);
  digitalWrite(leftBackward, LOW);
}

void reverseCar() {
  digitalWrite(rightForward, LOW);
  digitalWrite(leftForward, LOW);
  digitalWrite(rightBackward, HIGH);
  digitalWrite(leftBackward, HIGH);
}

void turnLeft() {
  digitalWrite(rightForward, HIGH);
  digitalWrite(leftForward, LOW);
  digitalWrite(rightBackward, LOW);
  digitalWrite(leftBackward, HIGH);
}

```

