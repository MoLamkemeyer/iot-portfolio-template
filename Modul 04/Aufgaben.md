## Reflection 2
[Reflection 2](/Reflections/ref02.md)



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


**Aufgabe 2: Division durch Null (Division by Zero):**

Im Gegensatz zu klassischen Desktop-Prozessoren (x86/x64), bei denen eine Integer-Division durch Null (1000 / 0) sofort eine unüberwindbare Hardware-Exception auslöst, verhält sich der ESP8266-Chip je nach Datentyp und Compiler-Optimierung manchmal überraschend:
•	Fließkommazahlen (float / double): Der Prozessor stürzt in der Regel nicht ab, sondern gibt laut IEEE-754-Standard den Wert inf (Unendlich) oder nan (Not a Number) aus.
•	Ganzzahlen (int / long): Hier führt die Division durch Null auf der Bare-Metal-Ebene des ESP8266 zu einem kritischen Rechenfehler, der den Prozessor blockiert. Der interne Hardware-Wachhund (Watchdog Timer / WDT) merkt, dass der Hauptprozess einfriert, und startet den Controller radikal neu.



**Aufgabe 3: Zu wenig Speicher (Out of Memory):**

Durch das übermäßige Erzeugen von globalen Objekten oder massiver Nutzung der String-Klasse fragmentiert der Arbeitsspeicher (RAM). Das führt dazu, dass Funktionen wie malloc() fehlschlagen und der Controller unkontrolliert mitten im Betrieb rebootet.
Ein Mikrocontroller wie der ESP8266 besitzt mit ca. 80 KB verfügbarem RAM einen sehr begrenzten Arbeitsspeicher. Dieser Speicher teilt sich im Wesentlichen in zwei Bereiche:

1.	Der Stack (Stapelspeicher): Hier liegen lokale Variablen, die nach dem Verlassen einer Funktion automatisch gelöscht werden.
2.	Der Heap (Dynamischer Speicher): Hier wird Speicher zur Laufzeit manuell mit dem Befehl new oder malloc() angefordert.
   
Das Problem (Memory Leak): Speicher, der auf dem Heap mit new reserviert wird, bleibt dort so lange blockiert, bis er im Programmcode explizit mit delete wieder freigegeben wird. Ruft man eine Funktion, die new nutzt, immer wieder auf, ohne den Speicher zu löschen, läuft der Heap unaufhaltsam voll, bis kein einziges Byte mehr frei ist.
Zusätzlich sorgt die wiederholte Verkettung von Objekten der Klasse String für eine starke Speicherfragmentierung, da im Hintergrund ständig neue, größere Speicherblöcke angefordert und alte Blöcke als unbrauchbare „Löcher“ hinterlassen werden.



**Teamarbeit**
## Task 1

serial output:

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

Fehlerhafter Code-Ausschnitt:

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

korrigierter code:

char* in ein char array ändern

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

## Task 2

Serial output:

Publish message: hello world #2
166
Message arrived [inTopic] 1
200
Message arrived [inTopic] 0
Publish message: hello world #3
250
Message arrived [inTopic] 1
Publish message: hello world #4
333
Message arrived [inTopic] 1
500
Message arrived [inTopic] 0
Publish message: hello world #5
1000
Message arrived [inTopic] 1

--------------- CUT HERE FOR EXCEPTION DECODER ---------------

Exception (6):
epc1=0x40201067 epc2=0x00000000 epc3=0x00000000 excvaddr=0x00000000 depc=0x00000000

>>>stack>>>

ctx: cont
sp: 3ffffdf0 end: 3fffffd0 offset: 0150
3fffff40:  00000000 3ffee698 3ffee698 00000001  
3fffff50:  00000001 00003703 3ffee698 40202b1c  
3fffff60:  00000001 3ffef4ef 3ffef4e7 402020ba  
3fffff70:  00000000 000030d1 fcac0801 003872cc  
3fffff80:  00000003 00000007 0000000c 00000004  
3fffff90:  3ffef4e4 3ffee698 3ffee698 3ffee7e8  
3fffffa0:  3fffdad0 00000000 3ffee698 40201317  
3fffffb0:  3fffdad0 00000000 3ffee7bc 4020422c  
3fffffc0:  feefeffe feefeffe 3fffdab0 40100d95  
<<<stack<<<

--------------- CUT HERE FOR EXCEPTION DECODER ---------------

 ets Jan  8 2013,rst cause:2, boot mode:(3,6)

load 0x4010f000, len 3424, room 16 
tail 0
chksum 0x2e
load 0x3fff20b8, len 40, room 8 
tail 0
chksum 0x2b
csum 0x2b
v00045a00
~ld
����g�{��g|�d�l`c��|{�l�g��o�□l`��{�l�d��
Connecting to MCU_ProgrammingFBML
.

broken code:

char super_message[100];
int cnt = 10;

void callback(char* topic, byte* payload, unsigned int length) {
  
  super_message[0] = 'A';
  cnt--;
  int value = 1000 / cnt;
  Serial.println(value);

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

fixed code:

char super_message[100];
int cnt = 10;

void callback(char* topic, byte* payload, unsigned int length) {
  
  super_message[0] = 'A';
  cnt--;
  if (cnt != 0){
    int value = 1000 / cnt;
    Serial.println(value);
  }
  else {
    Serial.println("Can not divide by zero");
  }

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


## Task 3

fehlerhafter code:

void memoryfunc() {
  char* msg = new char[512];
  sprintf(msg, "hello");
  Serial.println(msg);
}

gefixter code:

void memoryfunc() {
  char msg[512];
  sprintf(msg, "hello");
  Serial.println(msg);
}

Kommentar: msg is now stack-allocated (Stack-Speicher)
automatically freed when function ends
deterministic memory lifetime

## Task 4

fehlerhafter code:


void  ICACHE_RAM_ATTR buttonISR() {
  Serial.println("Test?");
  while (true){

  }
  buttonPressed = true;
}

void setup() {
  pinMode(BUILTIN_LED, OUTPUT);     // Initialize the BUILTIN_LED pin as an output
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
  pinMode(5, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(5), buttonISR, FALLING);
}

korrigierter code:

void  ICACHE_RAM_ATTR buttonISR() {
  Serial.println("Test?");
  buttonPressed = true;
}

void setup() {
  pinMode(BUILTIN_LED, OUTPUT);     // Initialize the BUILTIN_LED pin as an output
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
  pinMode(5, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(5), buttonISR, FALLING);
}

kommentar: keine while-schleife/zu langer delay
Fehler kommt daher, dass man innerhalb eines interrupts keine:
delay()
delayMicroseconds() (long durations)
yield()
while(...) loops that wait for conditions


these depend on buffers, interrupts, or OS scheduling.
Serial.print() / Serial.println()
WiFi operations
MQTT publish / subscribe
HTTP requests
SPI / I2C transactions (in most cases)

Memory allocation
Complex computation
floating-point math (on ESP8266 especially expensive)
large loops
recursion
string parsing
JSON handling

Anything not explicitly ISR-safe

## Task 5

Platformio.ini:

[env:wemos_usb]
platform = espressif8266
board = d1_mini
framework = arduino
upload_speed = 115200
monitor_speed = 115200

upload_protocol = espota
upload_port = ota-test
upload_flags = --auth=iotempower

main.cpp:

#include <ESP8266WiFi.h>
#include <ESP8266mDNS.h>
#include <WiFiUdp.h>
#include <ArduinoOTA.h>

#ifndef STASSID
#define STASSID "MCU_ProgrammingFBML"
#define STAPSK "HSBI2105"
#endif

const char* ssid = STASSID;
const char* password = STAPSK;

void setup() {
  Serial.begin(115200);
  Serial.println("Booting");
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.waitForConnectResult() != WL_CONNECTED) {
    Serial.println("Connection Failed! Rebooting...");
    delay(5000);
    ESP.restart();
  }

  // Port defaults to 8266
  // ArduinoOTA.setPort(8266);

  // Hostname defaults to esp8266-[ChipID]
  WiFi.setHostname("myesp8266");
  ArduinoOTA.setHostname("myesp8266");

  // No authentication by default
  // ArduinoOTA.setPassword("admin");

  // Password can be set with it's md5 value as well
  // MD5(admin) = 21232f297a57a5a743894a0e4a801fc3
  // ArduinoOTA.setPasswordHash("21232f297a57a5a743894a0e4a801fc3");

  ArduinoOTA.onStart([]() {
    String type;
    if (ArduinoOTA.getCommand() == U_FLASH) {
      type = "sketch";
    } else {  // U_FS
      type = "filesystem";
    }

    // NOTE: if updating FS this would be the place to unmount FS using FS.end()
    Serial.println("Start updating " + type);
  });
  ArduinoOTA.onEnd([]() {
    Serial.println("\nEnd");
  });
  ArduinoOTA.onProgress([](unsigned int progress, unsigned int total) {
    Serial.printf("Progress: %u%%\r", (progress / (total / 100)));
  });
  ArduinoOTA.onError([](ota_error_t error) {
    Serial.printf("Error[%u]: ", error);
    if (error == OTA_AUTH_ERROR) {
      Serial.println("Auth Failed");
    } else if (error == OTA_BEGIN_ERROR) {
      Serial.println("Begin Failed");
    } else if (error == OTA_CONNECT_ERROR) {
      Serial.println("Connect Failed");
    } else if (error == OTA_RECEIVE_ERROR) {
      Serial.println("Receive Failed");
    } else if (error == OTA_END_ERROR) {
      Serial.println("End Failed");
    }
  });
  ArduinoOTA.begin();
  Serial.println("Ready");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  ArduinoOTA.handle();
}

Bild von OTA upload

<img width="972" height="707" alt="image" src="https://github.com/user-attachments/assets/85c0f4ff-7012-46cc-9cf4-b74c4e4a4111" />

## Task 6

#include <ESP8266WiFi.h>
#include <ESP8266mDNS.h>
#include <WiFiUdp.h>
#include <ArduinoOTA.h>
#include <PubSubClient.h>

#ifndef STASSID
#define STASSID "MCU_ProgrammingFBML"
#define STAPSK "HSBI2105"
#endif

const char* ssid = STASSID;
const char* password = STAPSK;
const char* mqtt_server = "192.168.1.1";
const int ledPin = 12;

WiFiClient espClient;
PubSubClient client(espClient);

bool alarmActive = false;
unsigned long alarmStartTime = 0;
const unsigned long alarmDuration = 30000; // 30 Sekunden Obergrenze für den Alarm


void callback(char* topic, byte* payload, unsigned int length) {
  String message = "";
  for (unsigned int i = 0; i < length; i++) {
    message += (char)payload[i];
  }
  
  Serial.printf("MQTT-Signal empfangen [%s]: %s\n", topic, message.c_str());

  if (message == "on" || message == "ON") {
    if (!alarmActive) {
      alarmActive = true;
      alarmStartTime = millis(); // Zeitstempel für die 30-Sekunden-Begrenzung speichern
      Serial.println("!!! ALARM AKTIVIERT !!! Sanftes Blinken gestartet.");
    }
  } 
  else if (message == "off" || message == "OFF") {
    alarmActive = false;
    analogWrite(ledPin, 0); // LED sofort komplett ausschalten
    Serial.println("Alarm deaktiviert. LED ausgeschaltet.");
  }
}

void reconnect() {
  while (!client.connected()) {
    Serial.print("Verbinde mit MQTT-Broker...");
    String clientId = "AlarmNode-" + String(random(0xffff), HEX);
    if (client.connect(clientId.c_str())) {
      Serial.println("erfolgreich!");
      client.subscribe("hsbi/alarm"); // Das Alarm-Topic abonnieren
    } else {
      Serial.printf("Fehler, rc=%d. Neuer Versuch in 5s...\n", client.state());
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  Serial.println("Booting");
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.waitForConnectResult() != WL_CONNECTED) {
    Serial.println("Connection Failed! Rebooting...");
    delay(5000);
    ESP.restart();
  }

  // Port defaults to 8266
  // ArduinoOTA.setPort(8266);

  // Hostname defaults to esp8266-[ChipID]
  WiFi.setHostname("myesp8266");
  ArduinoOTA.setHostname("myesp8266");

  // No authentication by default
  // ArduinoOTA.setPassword("admin");

  // Password can be set with it's md5 value as well
  // MD5(admin) = 21232f297a57a5a743894a0e4a801fc3
  // ArduinoOTA.setPasswordHash("21232f297a57a5a743894a0e4a801fc3");

  ArduinoOTA.onStart([]() {
    String type;
    if (ArduinoOTA.getCommand() == U_FLASH) {
      type = "sketch";
    } else {  // U_FS
      type = "filesystem";
    }

    // NOTE: if updating FS this would be the place to unmount FS using FS.end()
    Serial.println("Start updating " + type);
  });
  ArduinoOTA.onEnd([]() {
    Serial.println("\nEnd");
  });
  ArduinoOTA.onProgress([](unsigned int progress, unsigned int total) {
    Serial.printf("Progress: %u%%\r", (progress / (total / 100)));
  });
  ArduinoOTA.onError([](ota_error_t error) {
    Serial.printf("Error[%u]: ", error);
    if (error == OTA_AUTH_ERROR) {
      Serial.println("Auth Failed");
    } else if (error == OTA_BEGIN_ERROR) {
      Serial.println("Begin Failed");
    } else if (error == OTA_CONNECT_ERROR) {
      Serial.println("Connect Failed");
    } else if (error == OTA_RECEIVE_ERROR) {
      Serial.println("Receive Failed");
    } else if (error == OTA_END_ERROR) {
      Serial.println("End Failed");
    }
  });
  ArduinoOTA.begin();
  Serial.println("Ready");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());

  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop() {
  ArduinoOTA.handle();

  if (!client.connected()) {
    reconnect();
  }
  client.loop(); //

  // --- NICHT-BLOCKIERENDE ALARM-LOGIK (PWM) ---
  if (alarmActive) {
    unsigned long currentMillis = millis();

    // 1. Prüfen, ob die 30 Sekunden Obergrenze abgelaufen ist
    if (currentMillis - alarmStartTime >= alarmDuration) {
      alarmActive = false;
      analogWrite(ledPin, 0); // LED ausschalten
      Serial.println("Alarm-Timeout: 30 Sekunden abgelaufen. Automatisch deaktiviert.");
    } 
    else {
      // 2. Mathematische Berechnung des sanften Blinkens (Fading via Sinuswelle)
      // Periode beträgt hier ca. 2000ms für ein volles Auf- und Abblenden
      float angle = (float)(currentMillis % 2000) / 2000.0 * 2.0 * PI;
      
      // Sinus liefert Werte von -1 bis +1. Skalierung auf den PWM-Bereich (0 bis 1023)
      int brightness = (sin(angle) + 1.0) * 511.5; 
      
      analogWrite(ledPin, brightness); // PWM-Wert an den Pin ausgeben
    }
  }
}

Bilder:

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/a0a7c47b-fa3b-4635-bbce-4e20ae2d1ca2" />

<img width="1148" height="2040" alt="image" src="https://github.com/user-attachments/assets/0f701945-531e-4283-b627-3b9bb4f12984" />

<img width="1148" height="2040" alt="image" src="https://github.com/user-attachments/assets/3d6693b3-f8d4-4d92-b438-3a9a2a9648bf" />

## Task 7

Teil 1 - Recherche

1. Verfügbare serielle Hardware-Schnittstellen (UART)
Ein UART (Universal Asynchronous Receiver-Transmitter) ist die im Chip verbaute Hardware-Einheit für die asynchrone serielle Kommunikation.
ESP8266 / Wemos D1 Mini
Der ESP8266 besitzt 2 serielle Hardware-Schnittstellen (UART0 und UART1). Allerdings ist ihre Nutzung stark eingeschränkt:
•	Serial (UART0):
o	Pins: TX (GPIO1) und RX (GPIO3).
o	Verwendung: Dies ist die primäre Schnittstelle. Sie ist intern direkt mit dem USB-zu-Seriell-Wandlerchip (z. B. CH340) auf dem Board verbunden. Sie wird standardmäßig für das Flashen des Programms und für die Debug-Ausgaben im Seriellen Monitor der Arduino IDE genutzt.
•	Serial1 (UART1):
o	Pins: TXD1 (GPIO2 / entspricht dem Pin D4 auf dem Wemos). Der zugehörige Empfangspin RXD1 (GPIO8) ist intern durch das Flash-Interfaze des Chips belegt und nicht herausgeführt.
o	Verwendung: Serial1 kann beim ESP8266 nur Daten senden (Tx), aber keine Daten empfangen (Rx). Sie wird in der Praxis oft genutzt, um reine Log-Daten an ein separates Terminal zu senden.
ESP32 / MH-ET LIVE ESP32 MiniKit
Der ESP32 ist deutlich leistungsstärker und besitzt 3 vollwertige serielle Hardware-Schnittstellen (UART0, UART1 und UART2). Eine Besonderheit des ESP32 ist die Pin-Matrix, über die fast jeder UART-Kanal auf beliebige GPIO-Pins umgeroutet werden kann. Standardmäßig sind sie wie folgt belegt:
•	Serial (UART0):
o	Pins: TX (GPIO1) und RX (GPIO3).
o	Verwendung: Genau wie beim ESP8266 fest für den USB-Upload und den seriellen Monitor reserviert.
•	Serial1 (UART1):
o	Pins: Typischerweise TX (GPIO10) und RX (GPIO9).
o	Verwendung: Da diese Pins bei den meisten Entwicklungsboards intern für den SPI-Flashspeicher genutzt werden, ist Serial1 ohne manuelles Umkonfigurieren der Pins im Code (Serial1.begin(Baud, SERIAL_8N1, RX_Pin, TX_Pin)) nicht direkt nutzbar.
•	Serial2 (UART2):
o	Pins: TX (GPIO17) und RX (GPIO16).
o	Verwendung: Dies ist die ideale Hardware-Schnittstelle für Zusatzkomponenten. Sie ist komplett frei, vollduplex-fähig und führt auf dem MH-ET LIVE MiniKit zu keinen Konflikten mit der Onboard-Infrastruktur.
2. Hardware- vs. Software-Serielle Kommunikation
Serielle Hardware-Kommunikation
Hierbei übernimmt eine dedizierte, fest in Silizium gegossene Elektronikeinheit (der UART-Controller) die Arbeit.
•	Stabilität: Extrem stabil. Der Hauptprozessor (CPU) wird kaum belastet. Der UART-Controller besitzt eigene Zwischenspeicher (Hardware-FIFO-Buffer). Wenn Daten reinkommen, sortiert die Hardware die Bits autonom ein und informiert die CPU erst, wenn ein Byte komplett ist. Das funktioniert auch bei sehr hohen Geschwindigkeiten (z. B. 115200 Baud oder höher) fehlerfrei.
Serielle Software-Kommunikation
Hierbei existiert kein physikalischer UART-Controller für die gewählten Pins. Die gesamte Kommunikation wird rein über Programmcode nachgebaut („Bit-Banging“).
•	Funktionsweise: Die CPU muss einen normalen GPIO-Pin permanent im Miksekundentakt überwachen, das Timing genau abzählen und die Flankenwechsel händisch interpretieren.
•	Stabilität: Deutlich instabiler. Da die CPU die Bits manuell zählen muss, führen zeitkritische Hintergrundprozesse (wie die Aufrechterhaltung des WLAN-Stacks beim ESP8266) schnell dazu, dass die CPU ein Bit verpasst. Das führt zu Datenmüll (Garbage Characters). Höhere Baudraten als 9600 oder 19200 Baud sind im Software-Modus oft fehleranfällig.
Wann ist serielle Softwarekommunikation erforderlich?
Sie ist genau dann zwingend erforderlich, wenn:
1.	Die vorhandenen Hardware-UARTs bereits vollständig belegt sind (z. B. UART0 für den PC-Monitor und UART2 für ein GPS-Modul).
2.	Man zusätzliche serielle Geräte an beliebigen Pins anschließen möchte, die keine native Hardware-Unterstützung für UART besitzen (wie es beim ESP8266 für den Empfang nötig ist, da UART1 dort kein Rx besitzt).
3. Die Bibliothek EspSoftwareSerial
Da der ESP8266 und ESP32 eine andere Prozessorarchitektur als klassische AVR-Arduinos besitzen, greift man im ESP-Core auf die spezialisierte Bibliothek EspSoftwareSerial zurück.
Verwendung auf den ESP-Boards:
Die Bibliothek erlaubt es, zwei völlig freie digitale Pins (z. B. D5 und D6 auf dem Wemos) als virtuellen seriellen Port zu deklarieren. Sie nutzt intern präzise Hardware-Timer und Interrupts, um das Bit-Banging so stabil wie möglich zu halten.
Minimales Code-Konstrukt für PlatformIO: Um die Bibliothek zu nutzen, binde sie über den Header ein und deklariere das Objekt:
C++
#include <SoftwareSerial.h>

// Definiere die virtuellen Pins (Beispiel für Wemos D1 Mini)
#define MY_RX_PIN D5
#define MY_TX_PIN D6

// Objekt erstellen
SoftwareSerial softSerial;

void setup() {
  Serial.begin(115200); // Hardware-Schnittstelle zum PC
  
  // Software-Schnittstelle mit materialschonenden 9600 Baud initialisieren
  softSerial.begin(9600, SWSERIAL_8N1, MY_RX_PIN, MY_TX_PIN, false);
  
  softSerial.println("Verbindung zum inneren Wachtposten steht!");
}

void loop() {
  if (softSerial.available()) {
    char inChar = (char)softSerial.read();
    Serial.print("Signal aus der Festung erhalten: ");
    Serial.println(inChar);
  }
}

Teil 2 - Praxis

Monitor:

<img width="264" height="163" alt="image" src="https://github.com/user-attachments/assets/853a44de-ff34-4498-857d-257edabbd689" />

Für die ini:
; [env:node_a]
; platform = espressif8266
; board = d1_mini
; framework = arduino
; lib_deps =
;     knolleary/PubSubClient
;     plerup/EspSoftwareSerial

; Knoten B  
[env:node_b]
platform = espressif8266
board = d1_mini
framework = arduino
lib_deps =
    plerup/EspSoftwareSerial

    
Code Knoten A:
#include <ESP8266WiFi.h>
#include <ESP8266mDNS.h>
#include <WiFiUdp.h>
#include <ArduinoOTA.h>
#include <PubSubClient.h>
#include <SoftwareSerial.h> 

#ifndef STASSID
#define STASSID "MCU_ProgrammingFBML"
#define STAPSK "HSBI2105"
#endif

const char* ssid = STASSID;
const char* password = STAPSK;
const char* mqtt_server = "192.168.1.1";

// ── SoftwareSerial Konfiguration ───────────────────────────────────
// (D6/GPIO12 = TX zu Knoten B, D5/GPIO14 = RX von Knoten B)
SoftwareSerial nodeSerial(D5, D6);  // (RX, TX)

WiFiClient espClient;
PubSubClient client(espClient);

// ── Kombinierte Callback-Funktion ───────────────────────────────────
void callback(char* topic, byte* payload, unsigned int length) {
  String message = "";
  for (unsigned int i = 0; i < length; i++) {
    message += (char)payload[i];
  }
  
  Serial.printf("MQTT-Signal empfangen [%s]: %s\n", topic, message.c_str());
  
  // 1. Logik für das originale Alarm-Topic (Jetzt nur noch Konsolen-Log)
  if (String(topic) == "hsbi/alarm") {
    if (message == "on" || message == "ON") {
      Serial.println("!!! ALARM TRIGGERED !!! (LED-Funktion deaktiviert)");
    } 
    else if (message == "off" || message == "OFF") {
      Serial.println("Alarm zurückgesetzt.");
    }
  }
  
  // 2. Logik für das prison/security Topic
  else if (String(topic) == "prison/security") {
    if (message == "all_clear" || message == "possible_threat" || message == "lockdown") {
      nodeSerial.println(message);  // An Knoten B per SoftwareSerial senden
      Serial.println("→ An Knoten B weitergeleitet");
    } else {
      Serial.println("⚠ Unbekannte Nachricht – ignoriert");
    }
  }
}

// ── Reconnect-Funktion mit beiden Topics ───────────────────────────
void reconnect() {
  while (!client.connected()) {
    Serial.print("Verbinde mit MQTT-Broker...");
    String clientId = "AlarmNode-" + String(random(0xffff), HEX);
    if (client.connect(clientId.c_str())) {
      Serial.println("erfolgreich!");
      
      // Beide Topics abonnieren
      client.subscribe("hsbi/alarm"); 
      client.subscribe("prison/security"); 
      Serial.println("Topics abonniert: hsbi/alarm & prison/security");
    } else {
      Serial.printf("Fehler, rc=%d. Neuer Versuch in 5s...\n", client.state());
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  nodeSerial.begin(9600);  // SoftwareSerial für Knoten B starten
  
  Serial.println("Booting");
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.waitForConnectResult() != WL_CONNECTED) {
    Serial.println("Connection Failed! Rebooting...");
    delay(5000);
    ESP.restart();
  }

  WiFi.setHostname("myesp8266");
  ArduinoOTA.setHostname("myesp8266");

  ArduinoOTA.onStart([]() {
    String type;
    if (ArduinoOTA.getCommand() == U_FLASH) {
      type = "sketch";
    } else {  
      type = "filesystem";
    }
    Serial.println("Start updating " + type);
  });
  ArduinoOTA.onEnd([]() {
    Serial.println("\nEnd");
  });
  ArduinoOTA.onProgress([](unsigned int progress, unsigned int total) {
    Serial.printf("Progress: %u%%\r", (progress / (total / 100)));
  });
  ArduinoOTA.onError([](ota_error_t error) {
    Serial.printf("Error[%u]: ", error);
    if (error == OTA_AUTH_ERROR) Serial.println("Auth Failed");
    else if (error == OTA_BEGIN_ERROR) Serial.println("Begin Failed");
    else if (error == OTA_CONNECT_ERROR) Serial.println("Connect Failed");
    else if (error == OTA_RECEIVE_ERROR) Serial.println("Receive Failed");
    else if (error == OTA_END_ERROR) Serial.println("End Failed");
  });
  
  ArduinoOTA.begin();
  Serial.println("Ready");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());

  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop() {
  ArduinoOTA.handle();
  
  if (!client.connected()) {
    reconnect();
  }
  client.loop();
}

Code Knoten B:
// Knoten B – Innen (Seriell empfangen → Konsole ausgeben)
#include <Arduino.h>
#include <SoftwareSerial.h>

// ── SoftwareSerial: RX=D5, TX=D6 ──────────────────────
// Gespiegelt zu Knoten A: TX von A → RX von B
SoftwareSerial nodeSerial(D5, D6);  // (RX, TX)

void setup() {
    Serial.begin(115200);     // USB-Monitor (Wachmann-Konsole)
    nodeSerial.begin(9600);   // Von Knoten A

    Serial.println("=== Knoten B – Wachstation ===");
    Serial.println("Warte auf Sicherheitsmeldungen...");
    Serial.println("──────────────────────────────");
}

void loop() {
    // Prüfen ob Daten von Knoten A ankommen
    if (nodeSerial.available()) {
        String received = nodeSerial.readStringUntil('\n');
        received.trim();  // Leerzeichen/Zeilenumbrüche entfernen

        if (received.length() > 0) {
            // Ausgabe für den Wachmann
            Serial.print("Security status: ");
            Serial.println(received);

            // Optional: Visuelle Unterscheidung nach Status
            if (received == "lockdown") {
                Serial.println("!!! ACHTUNG: LOCKDOWN AKTIV !!!");
            } else if (received == "possible_threat") {
                Serial.println(">> Mögliche Bedrohung erkannt!");
            } else if (received == "all_clear") {
                Serial.println(">> Lage ist ruhig.");
            }
            Serial.println("──────────────────────────────");
        }
    }
}

## Task 8

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/7d102fbf-53e2-4710-ba0a-b1c326d3ed50" />

ini:

[env:wemos_usb]
platform = espressif8266
board = d1_mini
framework = arduino
monitor_speed = 115200

lib_deps =
    knolleary/PubSubClient
    olikraus/U8g2

main.cpp:

#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <Wire.h>
#include <U8g2lib.h>

// --- EINSTELLUNGEN ---
const char* ssid        = "MCU_ProgrammingFBML";
const char* password    = "HSBI2105";
const char* mqtt_server = "192.168.1.1";
const char* topic_sub   = "task";


// --- DISPLAY-INITIALISIERUNG ---
// KORREKTUR: Verwendung des funktionierenden FULL-BUFFER-Konstruktors (F)
U8G2_SSD1306_64X48_ER_F_HW_I2C u8g2(U8G2_R0, /* reset=*/ U8X8_PIN_NONE);

WiFiClient espClient;
PubSubClient client(espClient);

// --- KORREKTUR: DIE OPTIMIERTE ANZEIGE-FUNKTION ---
void updateDisplay(String text) {
  u8g2.clearBuffer();					// 1. Internen Speicher leeren
  
  // KORREKTUR: Verwendung einer extra kleinen, standardisierten Schriftart
  u8g2.setFont(u8g2_font_5x7_tr);	
  
  // KORREKTUR: Sichere Y-Koordinaten, damit der Text nicht aus dem Bildschirm rutscht
  u8g2.drawStr(0, 12, "MQTT LIVE:"); 
  
  // Die Nachricht wird mittig platziert und zur Sicherheit auf 10 Zeichen begrenzt
  String gekuerzterText = text.substring(0, 10);
  u8g2.drawStr(0, 34, gekuerzterText.c_str()); 
  
  u8g2.sendBuffer();					// 2. Daten an das physikalische Display senden
}

// --- MQTT CALLBACK (EINGANGSVERARBEITUNG) ---
void callback(char* topic, byte* payload, unsigned int length) {
  String message = "";
  for (unsigned int i = 0; i < length; i++) {
    message += (char)payload[i];
  }
  
  Serial.print("Nachricht im Seriellen Monitor angekommen: ");
  Serial.println(message);
  
  // Display mit der frisch empfangenen Nachricht beschreiben
  updateDisplay(message);
}

void setup_wifi() {
  delay(10);
  Serial.begin(115200);
  Serial.println("\n--- Starte WLAN-Verbindung ---");
  
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWLAN erfolgreich verbunden!");
  Serial.print("IP-Adresse des Boards: ");
  Serial.println(WiFi.localIP());
}

void reconnect() {
  while (!client.connected()) {
    Serial.print("Versuche MQTT-Verbindung...");
    String clientId = "ESP32-OLED-Node-" + String(random(0xffff), HEX);
    
    if (client.connect(clientId.c_str())) {
      Serial.println("erfolgreich!");
      client.subscribe(topic_sub); // Topic abonnieren
    } else {
      Serial.printf("Fehler, rc=%d. Neuer Versuch in 5 Sekunden...\n", client.state());
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  
  // 1. I2C-Bus explizit auf den Standard-Pins des ESP32 starten
  Wire.begin(); // SDA an GPIO21, SCL an GPIO22
  
  // 2. Display initialisieren und Kontrast erzwingen
  u8g2.begin();
  u8g2.setContrast(255); // Volle Helligkeit einschalten
  
  // Erste Testanzeige auf dem Schirm erzeugen, BEVOR das WLAN rumsucht
  updateDisplay("STARTING"); 
  delay(1000);

  // 3. Netzwerk & MQTT-Verbindung starten
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
  
  // Visuelles Feedback: Verbindung steht, wir warten auf MQTT-Pakete
  updateDisplay("WIFI OK");
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop(); // Verarbeitet die eingehenden MQTT-Pakete im Hintergrund
}

## Task 9

