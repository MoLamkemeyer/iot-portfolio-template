## Abschlussprojekt Reflexion X

## PORTFOLIO-MASTER: Modul 7 – Abschlussprojekt

**Projektname:** Intelligentes Schulwetter- und Sicherheitssystem (Smart School Weather & Safety System)

**Gruppenmitglieder:** Emil, Frederik, Jonathan, Kilian, Minguel, Moritz

**Eigener Name:** Kilian Ridder

**Eigener Schwerpunkt/Knoten:** diverse Sensoren flashen, Animation der LEDs

## 1. Architektur & Technische Umsetzung (Mein Beitrag)

diverse Sensoren flashen, Animation der LEDs


**Mein Programmcode** 
IOTEmpore Befehle:

```
// Name: ledstrip, Anzahl: 10, Typ: GRB, Methode: UART1, Pin: D4
rgb_strip_bus(ledstrip, 8, F_GRB, NeoEsp8266Uart1800KbpsMethod, D4);
```

```
Humidity Sensor Boden
analog(water);
```

## 2. Die geforderte Projekt-Reflexion**

•	**Wichtigste Erkenntnis (Zusammenfassung):** Analoger Eingang ungleich digitaler Eingang. 

•	**Das möchte ich mir merken:** Nicht blind auf die Dokumentation vertrauen, weil manchmal Fehler drin sind.

•	**Mein Rat an zukünftige Studierende:** Nicht blind von der KI kopieren

## Was ist gut gelaufen?

•	Das Arbeiten mit Iotempower wird immer vertrauter

•	Zusammenarbeit in der Gruppe

## Was war schwierig & wo gab es Hürden?
 
•	**Technische Probleme:** die passenden Befehle finden, um die gesamten LEDs anzusteuern. 

•	**Positive/Unterhaltsame Herausforderungen:** Bodensensor-Einrichten mit Werten aus dem Wasserglas oder dem Boden des Gleis 13 an der IMA.


•	**Kommunikation im Team:** Kommunikation im Team: Durch die klare Verteilung der 8 ESP-Boards konnte jeder isoliert arbeiten, während die gemeinsame Logik-Zusammenführung am Hauptbildschirm der zentralen Steuerung stattfand. Fragen wurden immer offen und gemeinsam geklärt.

## 3. Hilfe und zusätzliche Arbeit

**Erhaltene Hilfe & Feedback**

•	**Wer hat geholfen:** Moritz

•	**Nutzen des Feedbacks:** Einrichten des Bodensensors 

**Geleistete Hilfe & Feedback**

•	**Wem habe ich geholfen:** Jonathan

•	**Welches Feedback habe ich gegeben:** Dashboard Vorbereitung zum Einrichten



## 4. Visueller Labor-Nachweis (Anhänge)

<img width="2048" height="1536" alt="d820eb95-7b62-4b53-82e9-8c0cb9814279" src="https://github.com/user-attachments/assets/e27e210d-3bd4-47a1-a08f-59d78b3b9ed5" />

<img width="2048" height="1536" alt="71e7d675-e69e-466c-9438-260849687aa3" src="https://github.com/user-attachments/assets/c09fb229-5dc0-4518-bf63-5c1a150fdb4c" />

<img width="2048" height="1536" alt="c5ef6eab-b237-4888-987a-392c956605bb" src="https://github.com/user-attachments/assets/a7658cfa-35d1-41a0-8961-e0f785266207" />


