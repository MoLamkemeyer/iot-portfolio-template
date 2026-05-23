Wichtigste Erkenntnisse & Lessons Learned
- Das IoTempower-Ökosystem: Spannende und mächtige Erfahrung zu sehen, wie MQTT und Node-RED als universelle Dolmetscher fungieren. Es war faszinierend zu beobachten, wie Nachrichten plattformübergreifend zwischen den Node-RED-Flows und MQTT-Brokern verschiedener Kommilitonen hin- und herwanderten.

- Echte Aha-Erlebnisse bei den Crashtests: Das gezielte Absperren und Überlasten des Boards (durch die Nullzeiger, Division durch Null, den vollgelaufenen Speicher und die blockierten Interrupts) war extrem lehrreich. Es war krass zu sehen, wie gnadenlos die Hardware reagiert: Wenn man im Code unsauber arbeitet, fängt sich der Prozessor nicht einfach fiktiv, sondern stürzt sofort hart ab und startet über den Watchdog (soft wdt reset / rst cause:4) komplett neu.

- Mein Rat an Nachfolgende: Schreibt ausnahmslos nicht-blockierenden Code (Verzicht auf delay(), Nutzung von millis()). Nur so bleibt das System reaktiv genug, um zeitkritische Hintergrundprozesse wie den Wi-Fi-Stack, MQTT-Abfragen und drahtlose OTA-Updates parallel und stabil zu verarbeiten.
Die Funktion millis() ist eines der wichtigsten Werkzeuge in der Arduino-Programmierung. Kurz gesagt: millis() ist die Stoppuhr des Mikrocontrollers.
Sobald der Wemos D1 Mini oder ESP32 Strom bekommt und hochfährt, startet im Hintergrund ein interner Zähler. millis() gibt dir die Millisekunden zurück, die seit diesem Start vergangen sind.


Was war gut? (Erfolge und Aha-Erlebnisse)

- Die visuelle Erfolgskontrolle: Es war extrem motivierend zu sehen, wie die gesamte Kette aus Taster, Node-RED-Logik, der Alarm-Warnung, dem OLED-Display am ESP32 und dem pulsierenden 12V-RGB-LED-Streifen auf der Steckplatine in Echtzeit ineinandergriff. Zu sehen, dass das, was man baut und programmiert, real funktioniert, war ein echtes Highlight.

- Dashboard-Flexibilität: Die parallele Darstellung der Telemetriedaten (wie der Dallas-Temperaturwerte) sowohl als Roh-MQTT-Nachricht als auch visuell auf dem Node-RED Dashboard lief hervorragend.


Was war schwierig und wo gab es Hürden?

- Der Node-RED Einstieg: Zu Beginn war die Konfiguration und Logik von Node-RED langwierig und kompliziert. Erst durch intensive Recherche und den gegenseitigen Support unter uns Kommilitonen kam der entscheidende Durchbruch, ab dem es deutlich schneller lief.

- Erneuter Pin-Konflikt (Hardware-Tücke): Bei der Anbindung des Dallas-Temperatursensors stießen wir auf massive Probleme, als wir den Pin D8 am Wemos nutzen wollten, der Sensor war dort schlicht nicht funktionsfähig. Erst der Wechsel auf den Pin D5 (GPIO14) brachte die Schaltung zum Laufen.

Interaktion, Feedback & kollaborative Hürden

- Teamübergreifender Support: Die Zusammenarbeit war unverzichtbar, besonders beim Lösen der anfänglichen Node-RED-Hürden und beim Verstehen der komplexeren Erweiterungs-Nodes. Die Zusammenarebit mit Frederik und Emil lief aber sehr gut.. Emil konnte die Installation von Node-Red gut erklären. Allerdings waren wir nach langen warten und installieren a, Ende dennoch überfragt, sodass ich durch eine Recherche den letzten Stück der Installation und Aufruf hinbekommen habe, sodass man das bei Frederik dann auch übertragen konnte und wir als team starten konnten. 


Transfer & Zukunftsgedanken (Kritischer Ausblick)

Obwohl die praktischen Versuche im Kleinen perfekt funktionierten, bleibt bei mir als Elektroniker eine zentrale Frage offen: Wie skaliert man das für die Praxis? * Beruflicher Bezug: Wie lässt sich diese IoT-Technik robust und wirtschaftlich in der Haustechnik (Gebäudeautomation) einsetzen?

- Wunsch an die Dozenten: Um zu verstehen, was im großen Stil nötig ist und welche realen Kosten damit verbunden sind, wäre es großartig, gemeinsam mit den Dozenten ein reales Großprojekt zu analysieren. Ein umfassenderer Gesamtplan an einem echten Industrie- oder Praxisbeispiel würde uns helfen, die gelernten Module noch gezielter auf die realen Arbeitssektoren zu übertragen.
