## Aufgabe 1: HLK-System mit Integration (Orchestrierung) und Simulatoren/Modellen (Tester)

## Aufgabe 1.1: Reiner Softwareintegrator + Mockups

<img width="912" height="803" alt="aufgabe1 1(3)" src="https://github.com/user-attachments/assets/1e359645-a97c-4495-a156-d843ac660c86" />
<img width="1918" height="1020" alt="aufgabe1 1(2)" src="https://github.com/user-attachments/assets/595eb2c3-d507-4409-bdcb-9e7ed0acd638" />
<img width="1918" height="1022" alt="aufgabe1 1" src="https://github.com/user-attachments/assets/07467fb9-8fbf-4d94-ae17-335e293ccb0a" />

**Schritt für Schritt Anleitung für mich**

Schritt 1: Das Dashboard vorbereiten (Der Ablageort)Bevor wir Knoten (Nodes) auf die Arbeitsfläche ziehen, müssen wir einen Platz auf der Benutzeroberfläche schaffen, wo der Schieberegler und die Anzeige später auftauchen.Schau an den ganz rechten Bildschirmrand von Node-RED.Klicke dort auf das Dashboard-Symbol (das sieht aus wie ein kleines Balkendiagramm).Es öffnet sich eine Seitenleiste. Klicke dort oben auf den Reiter Tabs und dann auf den Button + Tab. Ein neuer Tab namens Tab 1 erscheint.Fahre mit der Maus über Tab 1, klicke auf edit und benenne ihn in Klimasteuerung um. Klicke auf Update.Fahre jetzt mit der Maus über deinen neuen Tab Klimasteuerung und klicke auf den Button + Group.Benenne diese Gruppe über den edit-Button in Büro um. Klicke auf Update.

Schritt 2: Flow A – Der Temperatur-Simulator (Der "Sensor")Wir bauen jetzt den Schieberegler, mit dem du die Raumtemperatur manuell verändern kannst, und schicken diesen Wert per MQTT in den Raum.Scrolle in der linken Node-Liste nach unten bis zur Kategorie dashboard.Ziehe den Node slider auf deine leere Arbeitsfläche in der Mitte.Mache einen Doppelklick auf den slider-Node, um ihn einzustellen:Group: Wähle im Dropdown-Menü deine erstellte Gruppe [Klimasteuerung] Büro aus.Label: Trage Raumtemperatur einstellen (°C) ein.Min: 15Max: 30Step: 0.5 (Das erlaubt Schritte wie 21,5 °C).Klicke oben rechts auf Done.Gehe in der linken Leiste hoch zur Kategorie network, greife den Node mqtt out (Ausgang) und ziehe ihn rechts neben deinen Slider.Mache einen Doppelklick auf den mqtt out-Node:Server: Klicke auf das Stift-Symbol. Trage bei Server die IP-Adresse deines Mango-Routers ein (192.168.14.1). Klicke auf Add. (Wenn dort schon ein Broker eingerichtet ist, wähle ihn einfach aus).Topic: Trage das Thema buero/sim/temperatur ein.Klicke auf Done.Verkabeln: Klicke auf den grauen Punkt rechts am slider-Node, halte die Maustaste gedrückt und ziehe die Linie zum linken Punkt des mqtt out-Nodes.

Schritt 3: Flow B – Der Integrator (Das "Gehirn")Dieser Flow liest die simulierte Temperatur ununterbrochen mit und entscheidet anhand der Schwellenwerte, ob die Klimaanlage an- oder ausgeschaltet werden muss.Ziehe einen mqtt in-Node (Eingang aus der Kategorie network) auf die Arbeitsfläche (am besten ein Stück weiter unten, um Ordnung zu halten).Doppelklick auf den mqtt in-Node:Server: Wähle deinen eben eingerichteten Mango-Broker aus.Topic: Trage exakt dasselbe Thema ein: buero/sim/temperatur.Klicke auf Done.Gehe in die Kategorie function (links) und ziehe den Node switch rechts neben den eben erstellten MQTT-Eingang.Doppelklick auf den switch-Node, um die Schwellenwerte einzustellen:Property: Stelle sicher, dass dort msg.payload steht.Schau auf die erste Regelzeile darunter. Ändere das kleine Dropdown-Feld von az (Text) auf num (Zahl).Ändere das logische Dropdown daneben auf > (größer als) und trage rechts daneben 23.0 ein. (Wenn es wärmer als 23 °C wird, soll die Klima kühlen).Klicke ganz unten links im Fenster auf das kleine + add, um eine zweite Regel hinzuzufügen.Stell das Dropdown der zweiten Zeile wieder auf num, wähle das Zeichen < (kleiner als) und trage rechts daneben 21.0 ein. (Ist es kühler als 21 °C, kann die Klima aus).Klicke auf Done. (Dein Switch-Node hat nun rechts zwei Ausgänge).Ziehe jetzt zwei change-Nodes (Kategorie function) auf die Arbeitsfläche (übereinander platziert hinter dem Switch).Doppelklick auf den oberen change-Node:Benenne ihn zur Übersicht oben bei Name in ON um.Bei Rules stellst du ein: Set msg.payload to ON (Achte darauf, dass rechts im Dropdown str für String/Text ausgewählt ist). Klicke auf Done.Doppelklick auf den unteren change-Node:Benenne ihn in OFF um.Bei Rules stellst du ein: Set msg.payload to OFF (Typ: str). Klicke auf Done.Ziehe einen neuen mqtt out-Node ganz rechts daneben.Doppelklick darauf:Topic: Trage das Befehls-Thema buero/sim/ac/set ein.Klicke auf Done.Verkabeln:Verbinde den mqtt in-Node mit dem switch-Node.Verbinde den oberen Ausgang des Switches (Regel > 23) mit dem ON-Change-Node.Verbinde den unteren Ausgang des Switches (Regel < 21) mit dem OFF-Change-Node.Verbinde die Ausgänge beider Change-Nodes mit dem einzelnen Eingang des neuen mqtt out-Nodes.

Schritt 4: Flow C – Der AC-Simulator (Die "Klimaanlage")Dieser Teil lauscht auf den Befehl (ON/OFF), wertet ihn aus und färbt die Schaltfläche auf dem Dashboard passend ein.Ziehe einen neuen mqtt in-Node auf die Arbeitsfläche (wieder ein Stück weiter unten).Doppelklick darauf:Topic: Trage das Befehls-Thema ein: buero/sim/ac/set.Klicke auf Done.Ziehe einen function-Node (Kategorie function) rechts daneben.Doppelklick auf den function-Node. Lösche den Text, der dort standardmäßig drin steht, und kopiere exakt dieses JavaScript-Stück hinein:JavaScriptif (msg.payload === "ON") {
    msg.background = "green";
    msg.color = "white";
    msg.payload = "KLIMAANLAGE: AN";
} else {
    msg.background = "red";
    msg.color = "white";
    msg.payload = "KLIMAANLAGE: AUS";
}
return msg;
Klicke auf Done. (Dieser Node erzeugt dynamisch die Farben für das Dashboard).Scroll nach unten zur Kategorie dashboard und ziehe einen button-Node auf die Arbeitsfläche.Doppelklick auf den button-Node, um ihn mit der Farbfunktion zu verknüpfen:Group: Wähle wieder deine Gruppe [Klimasteuerung] Büro aus.Label: Trage dort exakt {{msg.payload}} ein.Background: Trage exakt {{msg.background}} ein.Text Color: Trage exakt {{msg.color}} ein.(Durch die geschweiften Klammern liest das Dashboard die Farben und den Text direkt aus dem JavaScript-Code aus).Klicke auf Done.Verkabeln: Verbinde den mqtt in-Node mit dem function-Node, und den function-Node mit dem button-Node.

Schritt 5: Speichern und Testen!Klicke ganz oben rechts auf den großen, roten Deploy-Button, um das System live zu schalten. Unter deinen drei lila MQTT-Knoten muss jetzt das Wort "connected" in grün stehen.Öffne dein Dashboard im Browser. Tippe dazu in die Adresszeile deines Browsers: http://localhost:40080/ui/ (bzw. die IP deines Labor-Gateways).Der Test:Schiebe den Temperatur-Regler mit der Maus hoch auf 25 °C.Was passiert im Hintergrund? Der Slider schickt 25 per MQTT $\rightarrow$ der Integrator empfängt es $\rightarrow$ der Switch merkt, dass 25 größer als 23 ist $\rightarrow$ der Change-Node macht daraus ein ON $\rightarrow$ der Befehl geht per MQTT an die virtuelle Klimaanlage $\rightarrow$ die Funktion macht den Button grün und schreibt KLIMAANLAGE: AN.Schiebe den Regler runter auf 20 °C: Der Button springt sofort um auf rot und zeigt KLIMAANLAGE: AUS.

## Aufgabe1.2: Sensor: Knoten mit Temperatursensor

**Alle Aufgaben werden zusammen mit meinem Teampartner <Frederik Bröckling>, [Frederik Bröckling](https://github.com/fbroeckling/Portfolio-of-Frederik-Br-ckling/blob/main/Module05/Tasks.md) zusammen bearbeitet. Es funktioniert nur das Programm auf seinem Laptop und wir haben zusammen nur einen funktionierenden Wemos D1 mini.**

Hintergrund: Warum darf das Shield nicht einfach direkt angeschlossen werden?
Der Dozent warnt im Skript eindringlich davor, Sensoren ohne Plan anzuschließen. Bei der Verwendung des Dallas-Sensor-Shields (DS18B20) zusammen mit dem Wemos D1 Mini hat das zwei handfeste Gründe:

Gefahr von Pin-Konflikten (Boot-Fehler): Das originale Wemos-Dallas-Shield ist auf der Platine fest mit dem Pin D2 verdrahtet. Wenn du in einer späteren Aufgabe (wie der Zutrittskontrolle) dort bereits deinen Taster oder das OLED-Display angeschlossen hast, blockieren sich die Signale gegenseitig. Schlimmer noch: Bestimmte Pins am Wemos (wie D3, D4 oder D8) müssen beim Starten des Boards auf einem exakten elektrischen Pegel liegen. Zieht ein Sensor diesen Pin beim Einschalten fälschlicherweise auf Masse, bleibt der Wemos in einer Boot-Schleife hängen (Boot-Glitches).

Spannungsebenen (3.3V vs. 5V): Der ESP8266-Chip auf dem Wemos arbeitet intern mit 3.3V. Viele Sensoren vertragen keine 5V oder senden 5V-Signale zurück, was den Mikrocontroller irreparabel zerstören kann. Das Dallas-Shield muss zwingend mit der stabilen 3.3V-Schiene versorgt werden.

Deshalb nutzen wir Dupont-Kabel, um den Sensor flexibel auf einen absolut sicheren und freien Pin (hier D5) zu legen!


node-red ist gleich geblieben, es wird nur statt dem Slider der gemessene Temperaturwert genommen:

MQTT Ausgabe:

<img width="102" height="58" alt="image" src="https://github.com/user-attachments/assets/319187fe-50fc-4b62-9931-0f8d8be73b25" />

<img width="108" height="58" alt="image" src="https://github.com/user-attachments/assets/a2313598-105e-4418-91ac-577db9d40e04" />

platformio.ini:
```
[env:d1_mini]
platform  = espressif8266
board     = d1_mini
framework = arduino

lib_deps =
    knolleary/PubSubClient
    milesburton/DallasTemperature
    paulstoffregen/OneWire
```

main.cpp:
```
#include <Arduino.h>
#include <ESP8266WiFi.h>        // ESP8266, nicht ESP32!
#include <PubSubClient.h>
#include <OneWire.h>
#include <DallasTemperature.h>

// ── WiFi ──────────────────────────────────────
const char* WIFI_SSID     = "MCU_ProgrammingFBML";
const char* WIFI_PASSWORD = "HSBI2105";

// ── MQTT ──────────────────────────────────────
const char* MQTT_BROKER   = "192.168.1.1";  // IP deines Brokers
const int   MQTT_PORT     = 1883;
const char* MQTT_TOPIC    = "AC/Soll";
const char* MQTT_CLIENT   = "wemos-sensor";

// ── Sensor ────────────────────────────────────
// Dallas Shield auf Wemos D1 Mini = GPIO 2 = D4
#define ONE_WIRE_PIN D5
OneWire oneWire(ONE_WIRE_PIN);
DallasTemperature sensors(&oneWire);

WiFiClient   espClient;
PubSubClient mqtt(espClient);

void connectWiFi() {
    WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
    Serial.print("WiFi verbinden");
    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println(" OK – IP: " + WiFi.localIP().toString());
}

void connectMQTT() {
    while (!mqtt.connected()) {
        Serial.print("MQTT verbinden...");
        if (mqtt.connect(MQTT_CLIENT)) {
            Serial.println("OK");
        } else {
            Serial.print("Fehler: ");
            Serial.println(mqtt.state());
            delay(2000);
        }
    }
}

void setup() {
    Serial.begin(115200);
    sensors.begin();
    connectWiFi();
    mqtt.setServer(MQTT_BROKER, MQTT_PORT);
}

void loop() {
    if (!mqtt.connected()) connectMQTT();
    mqtt.loop();

    sensors.requestTemperatures();
    float temp = sensors.getTempCByIndex(0);

    if (temp != DEVICE_DISCONNECTED_C) {
        char payload[8];
        dtostrf(temp, 4, 1, payload);       // z.B. "23.5"
        mqtt.publish(MQTT_TOPIC, payload);

        Serial.print("Temp: ");
        Serial.print(temp);
        Serial.println(" °C");
    } else {
        Serial.println("Sensor nicht gefunden – Verkabelung prüfen!");
    }

    delay(5000);
}
```


## Aufgabe 1.3: Akteur: Zweiter Knoten: AC als gleichmäßig blinkende LED

In Node-red wurde nichts angepasst. Der Code wurde erweitert, um eine Funktion, welche das ON/OFF Signal hört und demnach die LED schaltet.

Bild Hardwareaufbau:

<img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/f991b1dd-deab-46a0-ac85-571dc0971d19" />

ini: Hat sich nicht verändert

main.cpp:
```
#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <OneWire.h>
#include <DallasTemperature.h>

// ── WiFi ──────────────────────────────────────
const char* WIFI_SSID     = "MCU_ProgrammingFBML";
const char* WIFI_PASSWORD = "HSBI2105";

// ── MQTT ──────────────────────────────────────
const char* MQTT_BROKER   = "192.168.1.1";
const int   MQTT_PORT     = 1883;
const char* MQTT_TOPIC    = "AC/Soll";
const char* MQTT_CLIENT   = "wemos-sensor";
const char* TOPIC_STATE   = "AC/State";      // NEU

// ── Sensor ────────────────────────────────────
#define ONE_WIRE_PIN D5
OneWire oneWire(ONE_WIRE_PIN);
DallasTemperature sensors(&oneWire);

// ── LED Faden ─────────────────────────────────
#define LED_PIN D2                            // NEU
int  brightness = 0;
int  fadeStep   = 5;
bool ledFading  = false;

WiFiClient   espClient;
PubSubClient mqtt(espClient);

// ── MQTT Callback ─────────────────────────────── NEU
void mqttCallback(char* topic, byte* payload, unsigned int length) {
    String message = "";
    for (unsigned int i = 0; i < length; i++) {
        message += (char)payload[i];
    }
    Serial.print("Topic: ");
    Serial.print(topic);
    Serial.print(" → ");
    Serial.println(message);

    if (String(topic) == TOPIC_STATE) {
        if (message == "ON") {
            ledFading = true;
            Serial.println("LED: faden AN");
        } else if (message == "OFF") {
            ledFading  = false;
            brightness = 0;
            analogWrite(LED_PIN, 0);
            Serial.println("LED: AUS");
        }
    }
}

// ── LED updaten ───────────────────────────────── NEU
void updateFade() {
    if (!ledFading) return;
    brightness += fadeStep;
    if (brightness >= 255) { brightness = 255; fadeStep = -abs(fadeStep); }
    else if (brightness <= 0) { brightness = 0;  fadeStep =  abs(fadeStep); }
    analogWrite(LED_PIN, brightness);
}

void connectWiFi() {
    WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
    Serial.print("WiFi verbinden");
    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println(" OK – IP: " + WiFi.localIP().toString());
}

void connectMQTT() {
    while (!mqtt.connected()) {
        Serial.print("MQTT verbinden...");
        if (mqtt.connect(MQTT_CLIENT)) {
            mqtt.subscribe(TOPIC_STATE);     // NEU – AC/State abonnieren
            Serial.println("OK");
        } else {
            Serial.print("Fehler: ");
            Serial.println(mqtt.state());
            delay(2000);
        }
    }
}

void setup() {
    Serial.begin(115200);
    sensors.begin();
    pinMode(LED_PIN, OUTPUT);                // NEU
    analogWrite(LED_PIN, 0);                 // NEU
    connectWiFi();
    mqtt.setServer(MQTT_BROKER, MQTT_PORT);
    mqtt.setCallback(mqttCallback);          // NEU
}

void loop() {
    if (!mqtt.connected()) connectMQTT();
    mqtt.loop();

    // ── LED Fade (non-blocking) ────────────── NEU
    updateFade();

    // ── Temperatur alle 5 s senden ────────────
    static unsigned long lastMsg = 0;        // NEU – kein blockierendes delay()
    if (millis() - lastMsg >= 5000) {
        lastMsg = millis();

        sensors.requestTemperatures();
        float temp = sensors.getTempCByIndex(0);

        if (temp != DEVICE_DISCONNECTED_C) {
            char payload[8];
            dtostrf(temp, 4, 1, payload);
            mqtt.publish(MQTT_TOPIC, payload);
            Serial.print("Temp: ");
            Serial.print(temp);
            Serial.println(" °C");
        } else {
            Serial.println("Sensor nicht gefunden – Verkabelung prüfen!");
        }
    }

    delay(10);                               // Fade-Takt
}
```



