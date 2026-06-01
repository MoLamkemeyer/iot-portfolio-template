<img width="1321" height="583" alt="Screenshot 2026-06-01 111559" src="https://github.com/user-attachments/assets/474f5807-24de-4aed-b03f-ab69c9db0026" />
## Abschlussprojekt Reflexion 1

## PORTFOLIO-MASTER: Modul 7 – Abschlussprojekt

**Projektname:** Intelligentes Schulwetter- und Sicherheitssystem (Smart School Weather & Safety System)

**Gruppenmitglieder:** Emil, Frederik, Jonathan, Kilian, Minguel, Moritz

**Eigener Name:** Jonathan Hunold

**Eigener Schwerpunkt/Knoten:** Node-Red Flow & Dashboard 

## 1. Architektur & Technische Umsetzung (Mein Beitrag)

Node-Red Flow & Dashbaord erstellt und die geflashten Wemos sowie die Sensoren in das Flow eingearbeitet, sodass man immer die fertigen Sensoren im Dashboard angezeigt bekommt.

**Mein Programmcode** 
Beispiel:
Node-Red: 

Code für Warte auf RFID Validierung:

```
let startTime = Date.now();
let waitTime = 5000; //5 seconds
let timer = setInterval(()=>
{
    let current = Date.now();
    if(current-startTime > waitTime)
    {
        clearInterval(timer);
        node.send({payload:[false,msg.payload]});
    }

    if(flow.get("rfid") != null && String(flow.get("rfid")) != "")
    {
        node.send({payload:[true,msg.payload]});
        clearInterval(timer);
    }
},500);

```

Code für RFID Validierung 1/2:
```
if(msg.payload == "e6a5dbf9")
{
    return msg;
}
return;

Code für RFID Validierung 2/2
flow.set(msg.topic,msg.payload);
node.send({payload: msg.payload});
setTimeout(()=>
{
    flow.set(msg.topic,null);
    node.send({payload:"NAN"});
},5000);
```

## 2. Die geforderte Projekt-Reflexion**

•	**Wichtigste Erkenntnis (Zusammenfassung):** Das schreiben von Funktion in Node-Red ist sehr mächtig.
Statt einzelne Bausteine einzufügen, ist eine Funktion deutlich sinnvoller.

•	**Das möchte ich mir merken:** Node-Red ist ziemlich super und kann man schnell aufsetzen

•	**Mein Rat an zukünftige Studierende:** Vorher sich intensiv mit Node-Red zu beschäftigen.

## Was ist gut gelaufen?

•	Kommunikation im Team 

•	Aufgabenverteilung

## Was war schwierig & wo gab es Hürden?
 
•	**Technische Probleme:** --Kein Eintrag--

•	**Positive/Unterhaltsame Herausforderungen:** Das Zusammenspiel der verschiedenen Sensoren im Node-Red

•	**Verpasste Chancen (Hürden):** Dashboard schön zu gestalten ist anspruchsvoll.

•	**Kommunikation im Team:** Durch die klare Verteilung der 8 ESP-Boards konnte jeder isoliert arbeiten, während die gemeinsame Logik-Zusammenführung am Hauptbildschirm der zentralen Steuerung stattfand. Fragen wurden immer offen und gemeinsam geklärt.


## 3. Hilfe und zusätzliche Arbeit

**Erhaltene Hilfe & Feedback**

•	**Wer hat geholfen:** Moritz beim Dashboard

•	**Nutzen des Feedbacks:** Gestaltung und Aufbau des Dashboard 

**Geleistete Hilfe & Feedback**

•	**Wem habe ich geholfen:** Kilian 

•	**Welches Feedback habe ich gegeben:** Beraten für die Einstellung der Sensoren


## 4. Visueller Labor-Nachweis (Anhänge)

<img width="1321" height="583" alt="Screenshot 2026-06-01 111559" src="https://github.com/user-attachments/assets/91725e99-d029-4ef8-b1a5-af593dbf293e" />

<img width="1854" height="861" alt="SC2" src="https://github.com/user-attachments/assets/bf89ed32-a4b6-4a1b-a138-8bf2909e56a4" />


