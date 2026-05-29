## Reflexion 3
 
 ## Portfolio-Reflexion: Module 5 & 6 
 
**1. Was war gut? (Einstieg & Hardware-Erkenntnisse aus Modul 5)**

•	Lernkurve: Die praktischen Aufgaben in Modul 5 waren anfangs sehr anspruchsvoll, aber man ist mit der Zeit immer besser reingekommen.

•	Erfolgserlebnis: Es war richtig cool zu sehen, wie die ganze Kette der Zutrittskontrolle am Ende funktionierte, sowohl auf dem Board mit den LEDs und den klickenden Relais beim scannen des RFID als auch in Node-RED und über MQTT.

•	Systematik: Die Aufgaben haben logisch aufeinander aufgebaut, sodass man das System Schritt für Schritt mit weiteren Sensoren erweitern und gezielt verfeinern konnte.

•	Positive Erkundung: Das spielerische und das direkte visuelle/akustische Feedback der Hardware haben die abstrakte Logik der Datenströme sofort greifbar gemacht.

**2. Was war schwierig & wo gab es Hürden? (Modul 6)**

•	Infrastruktur-Frust: Ab Modul 6 ging der Frust mit der Einrichtung der IoTempower-Umgebung los.

•	Installations-Stopp: Trotz Stunden intensiven Ausprobierens und Herumdiktierens war die Installation auf drei von vier Laptops in der Gruppe unmöglich.

•	Engpass: Der gesamte Gateway-Stack lief letztlich nur auf einem einzigen Laptop vom Teampartner, was die parallele Arbeit massiv blockierte.

•	Hardware-Restriktion: Bei der RFID-Implementierung stießen wir auf die harten Grenzen des Wemos D1 Mini: Wegen der SPI-Bus-Kommunikation mussten die Pins D5, D6 und D7 zwingend belegt werden, wodurch D2 für die I2C-Leitung des Displays blockiert war.

**3. Wichtigste Erkenntnisse, Merkzettel & Rat für die Zukunft**

•	Wichtigste Erkenntnis: Pins bei komplexer SPI-Sensorik niemals nach Bauchgefühl belegen, sondern exakt nach den Boot-Vorgaben des ESP8266. Wählt man für den Reset fälschlicherweise D3 oder D4, sorgt der interne Pull-Up beim Starten für eine permanente Boot-Schleife.

•	Was ich mir merken möchte: Frameworks wie IoTempower bieten theoretisch enorme Skalierungsvorteile, erfordern in der Praxis aber eine extrem fehlerfreie, standardisierte Basis-Infrastruktur auf Betriebssystemebene.

•	Mein Rat an andere: Prüft das Pinout-Diagramm des spezifischen Boards vor dem Verkabeln. 

**4. Didaktisches Fazit, Interaktion & Lerneffekt**

•	Lerneffekt-Verlust: Durch den ganzen Stress bei der Software-Installation hat der eigentliche Lerneffekt in dieser Phase leider echt gelitten.

•	Fokus-Verschiebung: Statt logisch über die Systemarchitektur nachzudenken, war man am Ende mehr überfragt und hat ständig nur in der Konsole nach Linux- und Python-Fehlern gesucht.

•	Kompensation: Das führte dazu, dass man irgendwann nur noch stumpf per Copy and Paste Code-Schnipsel eingefügt hat, um den Labor-Prototypen irgendwie ans Laufen zu kriegen, ohne wirklich tief nachzudenken.

•	Interaktion im Labor: Beim Quatschen mit den anderen Gruppen kam heraus, dass fast alle vor demselben Problem standen. 

**5. Hilfe und zusätzliche Arbeit**

•	Erhaltene Hilfe: Der Support innerhalb der eigenen Gruppe war entscheidend, ohne den funktionierenden Laptop des Teampartners hätten wir den IoTempower-Workflow nicht live testen können, sowie die weiteren zwei Laptops nicht mehr einbinden können. Bei mir musste ich z.B. wsl und Ubuntu komplett deinstallieren und zurücksetzen und eine komplette Neuinstallation durhführen, was man wieder zusammen mit Frederik und Emil gemacht hat, um schneller zu sein. 

•	Geleistete Hilfe: Wir haben uns eng mit Nachbargruppen ausgetauscht, Fehlerprotokolle verglichen und Tipps zur Behebung Fehlern weitergegeben. Anschließend haben wir uns zusammen getan als etwas größere Gruppe. Vorab haben wir alles zu zwiet gemacht für Modul 5 und ab Modul 6 dann mit der Gruppe von Emil und Minguel zusammen getan, da man schon viel zusammen gearbeitet hat.

•	Eigene Beiträge: Wir haben die lückenhafte Dokumentation bezüglich der veralteten Gateway-Adressen (gw.iotempower.net vs. localhost:40080) intern für die Folgemodule dokumentiert und im Team-Review als Feedback festgehalten.


