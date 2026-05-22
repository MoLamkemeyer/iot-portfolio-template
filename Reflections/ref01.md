# Reflection 1 in Module 1

- What is your take-away, what do you want to remember, what would be your advice?
  Take-away can be small summary, but better outstanding points.
- What was good?
- What was difficult, where did you struggle?
- Was there any good/fun “struggling”/exploration?
  Any show stoppers – anything where you should reach out to peers or instructors? 
- How was your interaction with peers/instructors?
- Help and extra work
  - Who helped you, gave feedback, was it valuable?
  - Who did you help, gave feedback to?
  - Did you present, implement, made a PR, or fix something that was crucial for the class in itself?

1. Wichtigste Erkenntnisse und Ratschläge (Lessons Learned)
Hardware-Spezifikationen kritisch prüfen: Meine wichtigste Erkenntnis aus den ersten Laborphasen ist, dass man Entwicklungsboards trotz identischer Prozessorbasis (ESP8266) niemals blind verdrahten darf. Das platinenspezifische Layout und die internen Vorbeschaltungen der Hersteller unterscheiden sich in feinen, aber kritischen Details.

Protokolleffizienz schlägt Overhead: Das Kennenlernen des MQTT-Protokolls im Vergleich zu klassischen HTTP-Strukturen war ein echter Augenöffner. 

Mein Rat an zukünftige Studierende: Vertraut nicht blind darauf, dass ein Pin, der auf dem Wemos D1 Mini funktioniert, eins zu eins auf die NodeMCU übertragen werden kann. Schaut vor jedem Schaltungsaufbau zwingend in das exakte Pin-Mapping-Datenblatt des jeweiligen Board-Herstellers und messt Spannungsreihen im Zweifel lieber einmal zu viel nach.

2. Was ist gut gelaufen? (Erfolge und Stärken)
Besonders positiv war der schnelle Erfolg bei der vertikalen Systemintegration in Phase 4. Es war extrem motivierend zu sehen, wie ein selbst aufgebautes, vom Campus-Netzwerk völlig entkoppeltes Ad-hoc-Intranet über den OpenWrt-basierten Router stabil funktionierte. Die Steuerung einer externen LED und das synchrone Abgreifen eines Taster-Status in Echtzeit über den MQTT Explorer zu beobachten, hat die Brücke zwischen grauer Netzwerktheorie und physischer Hardware perfekt geschlagen. Auch das Schreiben von sauberem, minimalistischem C++ Code hat sehr gut funktioniert mit der Hilfe meines Teampartners. Da hab eich nochmal Unterschiede gemerkt, dass er stärker in der Programmiersprach ist, was mir aber wiederum gut tut, da er mir sehr viel beibringen kann und ich aktiv mit ihm zusammen das Programm noch besser erlerne und vertiefe.

3. Was war schwierig und wo gab es Hürden?
Die größte technische Hürde trat bei Aufgabe 6 (Tastersteuerung im Pull-Up-Modus) auf dem NodeMCU-Board auf. Wir stießen auf ein massives Problem, als wir versuchten, den digitalen Eingang über den Pin D2 (GPIO4) einzulesen. Der Pin lieferte trotz korrekter Software-Konfiguration mit INPUT_PULLUP nur instabile, „schwebende“ Werte , und angeschlossene LEDs glimmten ungewollt.

Nach systematischer Fehlersuche stellte sich heraus, dass bei der NodeMCU-Architektur der Pin D2 intern mit einer werkseitigen Beschaltung oder LED gekoppelt ist, was zu einem logischen Pegelkonflikt im Stromkreis führt.

Die Lösung: Wir mussten die Schaltung modifizieren und auf den Pin D4 (GPIO2) ausweichen. Dies war eine wertvolle, wenn auch anfangs frustrierende Herausforderung, die uns die realen Tücken des Embedded-Bereichs aufgezeigt hat.

4. Interaktion, Hilfe und zusätzliche Arbeit (Kollaboration & Peer-Feedback)
- Interaktion im Team: Die Zusammenarbeit im Labor war extrem agil und produktiv. Wir haben uns gegenseitig perfekt ergänzt. durch starke Recherche und gutes Herausfiltern der Vorinformation meinerseits und die gute C++-Programmierkenntnisse meines Partners ist ein super Teamgefüge entstanden, welche wir ab Aufgabe 7 des Modul 2 sehr gut umgesetzt haben. Vorher haben wir uns selber immer wieder unterstützt , aber recht eigenständig gearbeitet, was ein guter Einstieg war, um sich mit dem Modul vertraut zu machen.

- Geben und Nehmen von Feedback: Ich konnt andere Teams durch leine Fragen gezielt weiter Helfen und habe ebenso on weiteren Kommilitonen profitiert. Man merkt, dass einige Studenten deutlic stärker in der Materie sind. Das ist gut, da man von diesen Studenten ihre Sichtweisen und Arbeitsweisen verinnerlichen kann und man so weiter im Mpodul von weiteren Studenten lernt.

- Eigene Beiträge zum Kurs: Neben dem erfolgreichen Lösen und Dokumentieren des NodeMCU-Pin-Konflikts habe ich mich aktiv mit Fragen beteiligt, um so weitere Erkenntnisse zu sammeln. Ich war mir nicht zu Schade nach längeren Eigenständigen Arbeiten meine Mitstudierenden und Teampartner sowie die beidne Dozenten zu fragen, um Lösungen zu vergleichen, Probleme zu lösen und Hilfestellungen anzunehmen. Zudem stellte ich einige Fragen meine Dozenten, um weitere Erkenntnisse zu sammeln und auch mal spannende Wege herausz zulocken, wie man die Aufgaben lösen kann.   



Reflexion an den Dozenten:

- Der gesamte Input ist etwas viel aufeinmal und bei der langen Unterrichtszeit ist es schwer sich lange gut zu konzentrieren, sodass man irgendwann dazu neigt, dass man hauptsache schnell fertig werden möchte.
- Es wäre gut, wenn man mehr zusammen als Klasse die Aufgaben durch geht und Erklärungen dazu auf deutsch bekommt während der Vorlesung, da man beim selbstständigen Arbeiten nicht immer weiß, ob man wirklich alles richtig gemacht und verstanden hat und es ist deutlisch schwerer den Unterricht auf Englisch zu verfolgen.
- Meiner Meinung nach ist es manchmal besser weniger vom Inhalt zu machen, aber dafür der Input intensiv, sicher und klar von der Arbeitsweise ist, wie man arbeitet. Es nterscheiden sich viele Studenten von den Wissensstand, was es für Sie etwas schwerer macht, aber gearde die Leute die damit noch nicht so sicher sind wie andere hängen oftmals hinterher und werden etwas vernachlässigt, weil man sich eher den guten Studenten anpasst. 



