**Aufgabe 1. Fehlersuche und einfaches Debugging (Crash-Labor)**

•	Nullzeiger-Dereferenzierung (Null Pointer Dereference): Wenn im Code versucht wird, auf eine Speicheradresse zuzugreifen, die auf NULL (0) zeigt, stürzt der Prozessor sofort ab. Im seriellen Monitor (auf 115200 Baud gestellt) wird ein sogenannter „Fatal Exception“ (z. B. Cause 28 / LoadProhibited) ausgegeben, gefolgt von einem Stack Dump und einem automatischen Software-Reset. 


- Fehlerhafter code:

char* super_message;

void callback(char* topic, byte* payload, unsigned int length) {
  
  super_message[0] = 'A';

  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  // Switch on the LED if an 1 was received as first character
  if ((char)payload[0] == '1') {
    digitalWrite(BUILTIN_LED, LOW);   // Turn the LED on (Note that LOW is the voltage level
    // but actually the LED is on; this is because
    // it is active low on the ESP-01)
  } else {
    digitalWrite(BUILTIN_LED, HIGH);  // Turn the LED off by making the voltage HIGH
  }

}


- Ausgabe: 

WiFi connected
IP address: 
192.168.1.167
Attempting MQTT connection...connected
Publish message: hello world #1

--------------- CUT HERE FOR EXCEPTION DECODER ---------------

Exception (29):
epc1=0x4020104b epc2=0x00000000 epc3=0x00000000 excvaddr=0x00000000 depc=0x00000000

>>>stack>>>

ctx: cont
sp: 3ffffdf0 end: 3fffffd0 offset: 0150
3fffff40:  00000000 3ffee638 3ffee638 00000001  
3fffff50:  00000001 000011fb 3ffee638 40202af8  
3fffff60:  00000001 3ffef48f 3ffef487 40202096  
3fffff70:  00000000 000011de f9581001 0014a9d0  
3fffff80:  00000003 00000007 0000000c 00000004  
3fffff90:  3ffef484 3ffee638 3ffee638 3ffee788  
3fffffa0:  3fffdad0 00000000 3ffee638 402012f3  
3fffffb0:  3fffdad0 00000000 3ffee75c 402041e4  
3fffffc0:  feefeffe feefeffe 3fffdab0 40100d95  
<<<stack<<<


- Korrigierter Code:

char super_message[100];

void callback(char* topic, byte* payload, unsigned int length) {
  
  super_message[0] = 'A';

  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  // Switch on the LED if an 1 was received as first character
  if ((char)payload[0] == '1') {
    digitalWrite(BUILTIN_LED, LOW);   // Turn the LED on (Note that LOW is the voltage level
    // but actually the LED is on; this is because
    // it is active low on the ESP-01)
  } else {
    digitalWrite(BUILTIN_LED, HIGH);  // Turn the LED off by making the voltage HIGH
  }

}

