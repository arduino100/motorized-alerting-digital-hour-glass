//motorized-alerting-digital-hour-glass

const int switchPin = 8;

unsigned previousTime = 0;
int switchState = 0;
int prevSwitchState = 0;
int sensorValue;
int sensorHigh = 441;
int sensorLow = 682;

//341;682 for hour glass
//0;1023 for stopwatch, multipy number of units times 6     stopwatch for 1 minute

int led = 2;
long interval = 1000;
//1000 equals 1 second


void setup() {
  // put your setup code here, to run once:
  for(int x = 2;x<8;x++){
    pinMode(x, OUTPUT) ;
  
  pinMode(switchPin, INPUT);
}

}
void loop() {
  // put your main code here, to run repeatedly:
  unsigned long currentTime = millis();

  if(currentTime - previousTime > interval) {
    previousTime = currentTime;
    digitalWrite(led, HIGH);
    led++;

    if(led == 8){
      delay(interval);
      int sound = 
      map(sensorValue, sensorLow, sensorHigh, 50, 1000);
      //50, 4000
      pinMode ( 9, OUTPUT);
      tone(9, sound ,100);
      Serial.begin(9600);
      Serial.println("one unit");
     
      pinMode ( 10, OUTPUT);
      digitalWrite(10, HIGH);
      delay(500);
      digitalWrite(10, LOW);
      delay(500);
      digitalWrite(10, HIGH);
      delay(500);
      digitalWrite(10, LOW);
      delay(500);
      digitalWrite(10, HIGH);
      delay(500);
      digitalWrite(10, LOW);
      delay(500);
      digitalWrite(10, HIGH);
      delay(500);
      digitalWrite(10, LOW);
      delay(500);
    }
   
  }
 

  
   switchState = digitalRead (switchPin);

  if(switchState != prevSwitchState){
    for(int x = 2;x<8;x++){
       digitalWrite(x, LOW); 
    }
  
  //goes here

 
    led = 2;
    previousTime = currentTime;
  }

      prevSwitchState = switchState;
}





