#include <IRremote.h>

int RECV_PIN = 11;
IRrecv irrecv(RECV_PIN);
decode_results results;

#define BUTON1 0xFF6897
#define BUTON2 0xFF9867
#define BUTON3 0xFF7A85
#define BUTON4 0xFF10EF
#define BUTON5 0xFF22DD
#define BUTON6 0xFF5AA5
#define BUTON7 0xFF42BD
#define BUTON8 0xFF4AB5
#define BUTON9 0xFFC23D
int role1 = 6;
int role2 = 7;

void setup()
{
  pinMode(role1, OUTPUT);
  pinMode(role2, OUTPUT);

  Serial.begin(9600);
  irrecv.enableIRIn();
}
void loop() {

  if (irrecv.decode(&results))
  {
    if (results.value == BUTON1)
    {
      digitalWrite(role1, !digitalRead(role1));
      if (digitalRead(role1) == HIGH)
      {
        Serial.println("LED 1 yandi");
      }
      else
      {
        Serial.println("LED 1 sondu");
      }
    }
    if (results.value == BUTON2)
    {
      digitalWrite(role2, !digitalRead(role2));
      if (digitalRead(role2) == HIGH)
      {
        Serial.println("ROLE 2 yandi");
      }
      else
      {
        Serial.println("ROLE 2 sondu");
      }
    }
    
  
    if (results.value == BUTON9)
    {
      digitalWrite(role1, LOW);
      digitalWrite(role2, LOW);
      
      Serial.println("Tum LED'ler sondu");
    }
    if (results.value == BUTON5)
    {
      digitalWrite(role1, HIGH);
      digitalWrite(role2, HIGH);
     
      Serial.println("Tum LED'ler yandi");
    }
    irrecv.resume();
  }
} 
