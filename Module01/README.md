

## Task Inspirations

- Inspiration 1: Der smarte WG-Heizwächter (Klima- & Energiemanagement) Ein ESP32-basiertes System für schlecht isolierte Studentenfehnhäuser oder WGs. Ein Kontaktsensor am Fenster erkennt, wenn gelüftet wird, und ein kleiner Servomotor dreht das Heizungsventil automatisch zu, um Energieverschwendung zu vermeiden. Wenn das Fenster im Winter zu lange offen bleibt, erinnert ein akustischer Signalgeber an das Schließen. 

- Inspiration 2: Der smarte Postkasten (Sensorik & Benachrichtigung): Ein batteriebetriebener ESP32 im Briefkasten. Sobald die Klappe geöffnet wird (Lichtsensor oder Kontaktsensor), wacht der Controller auf, verbindet sich kurz mit dem WLAN und schickt dir eine Nachricht aufs Handy („Du hast Post!“). Danach geht er wieder in den Tiefschlaf (Deep Sleep), um Batterie zu sparen.


## Task Personal Profile

Programmiererfarung:
TwinCat 3 Structured Text (ST) ist realtiv gut, da man viel in der Firma damit arbeitet.
C   - Nur Grundkenntnisse durch das Studium im ersten Semester erlangt.
C++ - Nur Grundkenntnisse durch das Studium im zweiten Semester erlangt.
Im bereich Microcontroller gibt es keien Vorkenntnisse. 

•	Bisheriges Mikrocontroller-Wissen: Meine Erfahrung mit MCUs ist noch am Anfang. Ich weiß, was ein Arduino oder ein Raspberry Pi ist, habe aber noch keine tiefergehenden, eigenständigen Projekte mit dem ESP32 oder nackter Hardware umgesetzt. Das Zusammenspiel von Registern, GPIO-Pins und elektronischen Bauteilen (Sensoren/Aktoren) möchte ich in diesem Kurs praktisch erlernen. 

Kreative Fähigkeiten (Creative Qualities)
Mir macht es großen Spaß, völlig neue Sachen zu erfinden, reale Probleme systematisch zu analysieren und innovative Produktlösungen zu entwickeln. In den vergangenen Semestern konnte ich diese Stärke bereits erfolgreich in interdisziplinären Modulen einbringen, bei denen wir marktfähige Produkte von Grund auf konzipieren und vor einer Jury bestmöglich pitchen mussten.

Dazu gehörten zwei High-Tech-Konzepte aus dem Handwerks- und Industriebausektor:

Der autonome Unterputz-Roboter: Ein mobiles System, das schwere, gesundheitsgefährdende Unterputzarbeiten automatisch übernimmt. Durch das Hochladen eines digitalen Bauplans führt er seine Aufgaben zentimetergenau und selbstständig aus.

Der intelligente AR/VR-Bauhelm: Ein vernetzter Helm, der Baupläne direkt als digitales Overlay in das Sichtfeld des Arbeiters projiziert und über integrierte Umgebungssensoren Sicherheits- und Gefahrenzonen während des Arbeitens visuell überwacht.

Erwartungen: 

Generell macht es mir Spaß neue Ideen auszudenken und diese durchzugehen bis zum Endprodukt. Mit den neuen Erkenttnissen aus dem Kurs möchte ich mein Wissen ausbreiten und vertiefen und diese in meinen Lieblinsgsektoren wie Fussball und SPort sowie der Immobiliensektor erweitern. 

Meine Erwartungen an diesen Kurs konzentrieren sich auf das Zusammenspiel von kreativer Produktentwicklung und technischer Umsetzung:
Ich erwarte einen steilen, aber extrem spannenden Lernprozess in diesem kompakten Blockkurs. Ich möchte lernen, wie man eingebettete Systeme stabil programmiert, wie die drahtlose Kommunikation (WLAN/MQTT) funktioniert und wie man aus einzelnen elektronischen Komponenten ein funktionierendes Gesamtsystem baut.

Prototyping für eigene Innovationen: 
Mein Ziel ist es, das gelernte Wissen über autarke Ad-hoc-Netzwerke (wie mit dem Router) zu nutzen, um meine kreativen Produktideen aus den Vorsemestern, wie autonome Robotiksysteme für das Handwerk oder vernetzte Gadgets für den Sport- und Immobiliensektor, als funktionstüchtige IoT-Prototypen realisieren zu können.

## Task What is IoT

Domains and included areas:

- Smart Home (Hausautomatisierung): Die Vernetzung von Haushaltsgeräten, Beleuchtung, Heizung und Sicherheitssystemen. Ziel ist die Steigerung des Wohnkomforts, die Erhöhung der Sicherheit und die effiziente Energienutzung (z. B. automatisches Herunterregeln der Heizung beim Öffnen eines Fensters).

- Industrial IoT (IIoT) / Industrie 4.0: Der Einsatz von IoT-Technologien in der Fertigungsindustrie und Logistik. Maschinen, Transportbänder und Lagerbestände kommunizieren selbstständig miteinander, um Produktionsprozesse zu optimieren, Lieferketten lückenlos zu überwachen und vorausschauende Wartung (Predictive Maintenance) zu ermöglichen.

- Smart Cities (Intelligente Städte): Die Digitalisierung städtischer Infrastrukturen. Sensoren erfassen Verkehrsströme zur intelligenten Ampelsteuerung, überwachen den Füllstand von Mülltonnen für optimierte Entsorgungsrouten oder messen die Luftqualität in Echtzeit.

Weitere Domäne:
1.	Smart Agriculture (Intelligente Landwirtschaft): Vernetzte Bodensensoren messen Feuchtigkeit und Nährstoffe, um automatisierte Bewässerungs- und Düngeanlagen präzise zu steuern.
2.	Connected Mobility / Automotive: Vernetzte Fahrzeuge, die Echtzeit-Verkehrsdaten austauschen, Software-Updates über die Luft (Over-the-Air) erhalten und mit der Straßeninfrastruktur kommunizieren.
3.	Digital Health / E-Health: Medizinische Wearables, die Vitalwerte von Patienten rund um die Uhr überwachen und bei Unregelmäßigkeiten automatisch den Arzt benachrichtigen.


Commonly used (data) protocols:

- MQTT (Message Queuing Telemetry Transport): Ein extrem leichtgewichtiges, auf dem Publish/Subscribe-Modell basierendes Protokoll. Es wurde speziell für energiesparende Geräte und Netzwerke mit geringer Bandbreite oder hoher Latenz entwickelt. Perfekt für die Übertragung von Sensordaten an einen zentralen Broker.

- CoAP (Constrained Application Protocol): Ein spezialisiertes Web-Übertragungsprotokoll für ressourcenbeschränkte Geräte (wenig Speicher, schwache CPU). Es basiert auf UDP (statt TCP), lehnt sich eng an das bekannte HTTP-Modell (REST-Architektur mit GET, POST, PUT, DELETE) an und spart durch komprimierte Header massiv Datenvolumen.


Typical devices (appliance or micro controller):

- ESP32 (Mikrocontroller): Ein extrem leistungsfähiger, kostengünstiger und stromsparender Mikrocontroller-Chip mit integriertem WLAN und Dual-Mode-Bluetooth. Er bildet das Herzstück vieler DIY- und kommerzieller IoT-Projekte, da er direkt Sensoren auslesen und Daten ins Internet funken kann.

- Smarte Steckdose (Smart Plug / Haushaltsgerät): Ein Zwischenstecker, der herkömmliche elektronische Geräte ins IoT einbindet. Er verfügt über ein eingebautes WLAN-/Zigbee-Modul und ein Relais. Dadurch lässt er sich per App oder Sprachbefehl aus der Ferne ein- und ausschalten und misst oft zusätzlich den Stromverbrauch des angeschlossenen Geräts.

Weitere Geräte:
1.	Smarter Rasenmäher- / Saugroboter: Autonome Haushaltshelfer, die per App gesteuert werden, Wetterdaten einbeziehen und Karten ihrer Umgebung in der Cloud speichern.
2.	Intelligenter Kühlschrank: Ein Kühlgerät mit Innenkameras und Display, das den Haltbarkeitsstatus von Lebensmitteln überwacht, Rezepte vorschlägt und Einkaufslisten digital synchronisiert.
3.	Vernetzter Fitness-Tracker / Smartwatch: Wearables mit Herzfrequenz-, GPS- und Beschleunigungssensoren, die Aktivitätsdaten verarbeiten und an Cloud-Plattformen senden.


Challenges:

- Datenschutz und IT-Sicherheit: Da Milliarden von Geräten sensible Daten erfassen und übertragen, steigen die Angriffsflächen für Hacker. Viele IoT-Geräte besitzen kaum Sicherheitsmechanismen, was sie anfällig für Botnetze macht.

- Interoperabilität und Fragmentierung: Es gibt keinen universellen Standard. Viele Hersteller kochen ihr eigenes Süppchen (proprietäre Ökosysteme), weshalb Geräte unterschiedlicher Marken oft nicht ohne tiefes technisches Vorwissen miteinander kommunizieren können.

- Hoher Energiebedarf der Infrastruktur: Die Verarbeitung und Speicherung der gigantischen Datenmengen in globalen Rechenzentren (Cloud) verbraucht enorm viel Strom.

- Lebenszyklus und Elektroschrott: Viele IoT-Geräte werfen Fragen zur Nachhaltigkeit auf, wenn der Software-Support nach wenigen Jahren eingestellt wird und funktionierende Hardware unbrauchbar wird.

- Netzwerk-Infrastruktur und Bandbreite: In ländlichen Gebieten oder Entwicklungsländern limitiert eine unzureichende Netzabdeckung (WLAN, Mobilfunk) den verlässlichen Einsatz von IoT-Systemen im großen Stil.



## Reflection 1
[Reflection 1](/Reflections/ref01.md)
