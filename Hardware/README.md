# Hardware

This is the hardware, I/we took out.
- Arduino Kit
- Wemos D1 mini
- USB-Kabel

## year-month-day

- Dupont cables 20 socket to socket (watch https://youtu.be/yXirMBP3x4U for documentation)
- 1x large breadboard, 1x medium size breadboard (watch https://youtu.be/yXirMBP3x4U for documentation)
-  ...

![A picture showing all parts taken out this day.](/images/img01.jpg "A picture showing all parts taken out this day.]")

## Connectivity Classification Table

TODO: here will be a table showing different connection options like serial (uart/rs232), i2c, onewire, pwm, ... 
and corresponding wiring documentation (update table when you get new and/or interesting parts)

Bus-Systeme & Peripheriekommunikation (Kurzübersicht für Ihr Portfolio) • GPIO / PWM: Allgemeine digitale Ein-/Ausgangspins für einfache Schaltsignale (Taster, Relais) oder zeitkritische Pulsmodulationen (Dimmen, Servos).

• I2C (Inter-Integrated Circuit): Ein Synchroner, Halbduplexer 2-Draht-Bus (SDA für Daten, SCL für den Takt). Er ist Master-Slave-basiert und erlaubt es, mehrere Sensoren (z. B. Displays, Barometer) parallel über dieselben zwei Leitungen anzusprechen.

• SPI (Serial Peripheral Interface): Ein sehr schneller, synchronisierter 4-Draht-Bus (MOSI, MISO, SCK, CS). Ideal für datenintensive Anwendungen wie SD-Kartenleser oder TFT-Displays.

• UART (Universal Asynchronous Receiver-Transmitter): Eine asynchrone Punkt-zu-Punkt-Verbindung über zwei Leitungen (TX und RX). Wird standardmäßig für die serielle Kommunikation mit dem PC (USB-Schnittstelle) genutzt. RS232/RS485 sind industrielle Pegel-Erweiterungen davon.

• OneWire (Eindraht-Bus): Ein von Dallas Semiconductor entwickelter Bus, der neben Masse nur eine einzige Datenleitung benötigt (z. B. für den Temperatursensor DS18B20).

Achtung (Das Spiegelbild): Achten Sie beim Stecken der Komponenten auf dem Breadboard immer darauf, ob Sie die Pins von oben (Top View) oder von unten (Bottom View auf die Lötpunkte) betrachtet haben. Verwechselt man die Seiten, spiegelt man versehentlich die Spannungsversorgung (VCC und GND) wider, was die Bauteile sofort zerstören kann!

UART siehe Aufgabe 7 GPIO / PWM siehe Aufgabe 5 und 8
