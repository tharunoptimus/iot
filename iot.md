# IOT Experiments

## LED

```cpp
int LED = 5; // Assign LED pin i.e: D1 on NodeMCU
void setup() {
    // initialize GPIO 5 as an output
    pinMode(LED, OUTPUT);
}
// the loop function runs over and over again forever
void loop() {
    digitalWrite(LED, HIGH); // turn the LED on
    delay(1000); // wait for a second
    digitalWrite(LED, LOW); // turn the LED off
    delay(1000); // wait for a second
}
```


## LM35
```cpp
// initializes or defines the output pin of the LM35 temperature sensor
int outputpin= A0;
//this sets the ground pin to LOW and the input voltage pin to high
void setup() {
    Serial.begin(9600);
}
void loop() //main loop
{
    int analogValue = analogRead(outputpin);
    float millivolts = (analogValue/1024.0) * 3300; //3300 is the voltage provided by NodeMCU
    float celsius = millivolts/10;
    Serial.print("in DegreeC= ");
    Serial.println(celsius);
    //----------Calculation for Fahrenheit ----------//
    float fahrenheit = ((celsius * 9)/5 + 32);
    Serial.print(" in Farenheit= ");
    Serial.println(fahrenheit);
    delay(1000);
}
```

## IR
```cpp
int ledPin = 12; // choose pin for the LED
int inputPin = 13; // choose input pin (for Infrared sensor) 
int val = 0; // variable for reading the pin status
void setup() { 
    pinMode(ledPin, OUTPUT); // declare LED as output 
    pinMode(inputPin, INPUT); // declare Infrared sensor as input
}
void loop()
{ 
    val = digitalRead(inputPin); // read input value 
    if (val == HIGH){ // check if the input is HIGH
        digitalWrite(ledPin, LOW); // turn LED OFF 
    }  else { 
        digitalWrite(ledPin, HIGH); // turn LED ON 
    } 
}
```

## LDR
```cpp
void setup() {
    Serial.begin(9600); // initialize serial communication at 9600 BPS
}
void loop() {
    int sensorValue = analogRead(A0); // read the input on analog pin 0
    float voltage = sensorValue * (5.0 / 1023.0); // Convert the analog reading (which 
    goes from 0 - 1023) to a voltage (0 - 5V)
    Serial.println(voltage); // print out the value you read
}
```

## Proximeter
```cpp
void setup() {
    // ultrosonic HCSR -04 - proximity detection
    pinMode(D6,OUTPUT); //trigger pin
    pinMode(D7,INPUT);//Echopin //rcr
}
void loop() {
    // put your main code here, to run repeatedly:
    //trigger sonic waves 
    digitalWrite(D6,LOW);
    delayMicroseconds(2);
    digitalWrite(D6,HIGH);
    delayMicroseconds(10);
    // receive ECHO and find DISTANCE
    long duration= pulseIn(D7,HIGH);
    float dist= duration * 0.034/2;
    Serial.println("Distance is...");
    Serial.println(dist);
    delay(2000);
}
```

## Servo Motor
```cpp
#include <Servo.h>
Servo newservo1;//define a name for servo
void setup() {
    // put your setup code here, to run once:
    newservo1.attach(D6);
}
void loop() {
    // put your main code here, to run repeatedly:
    newservo1.write(180);
    delay(1000);
    newservo1.write(0);
    delay(1000);
}
```

## Servo with POT
```cpp
# include<Servo.h>
Servo mew 1;
void setup () {
    New1.attach(D6);
    Serial.begin(9600);
    pinMode(A0, INPUT);
}
void loop() {
    float x=analogRead(A0);
    x=map(x,0,1023,0,180);
    new1.write (x);
    delay(15);
}
```