Für Phase 1:

1. OpenWrt erforschen
Was ist OpenWrt? OpenWrt ist ein Linux-basiertes Open-Source-Betriebssystem, das speziell für eingebettete Geräte wie Router, Access Points und IoT-Gateways entwickelt wurde. Anstatt der oft stark eingeschränkten und unsicheren Standard-Firmware der Hersteller bietet OpenWrt die vollständige Kontrolle über das Gerät.
Warum ist OpenWrt im IoT-Bereich so wichtig?
•	Paketverwaltung (opkg): Ähnlich wie bei Ubuntu (apt) können zusätzliche Softwarepakete direkt auf dem Router installiert werden. Dadurch lässt sich der Router in einen MQTT-Broker (Mosquitto), einen Webserver oder eine Integrationsplattform verwandeln.
•	Erweiterte Netzwerkkontrolle: Es ermöglicht komplexe Routing-Konfigurationen, das Erstellen isolierter VLANs (z. B. um unsichere Smart-Home-Geräte vom restlichen Netzwerk zu trennen) und detaillierte Firewall-Regeln.
•	Ressourceneffizienz: Es ist extrem schlank programmiert und läuft stabil auf minimaler Hardware (wie unserem Mango-Router).
Die Benutzeroberfläche: LuCI
LuCI ist die standardmäßige, webbasierte grafische Benutzeroberfläche (Web-GUI) für OpenWrt. Sie ermöglicht es, alle grundlegenden und fortgeschrittenen Konfigurationen komfortabel im Browser vorzunehmen, ohne zwingend die Linux-Kommandozeile (CLI) über SSH nutzen zu müssen.

2. LAN vs. WAN-Vergleich
Jeder IoT-Router besitzt physisch und logisch getrennte Schnittstellen, um den Datenverkehr zu ordnen und das lokale Netzwerk abzusichern.

LAN (Local Area Network)
Das lokale Netzwerk verbindet alle Geräte innerhalb eines begrenzten Bereichs (z. B. dein Team-Arbeitsplatz im HSBI-Labor oder deine Wohnung) untereinander.
•	Schnittstelle am Router: Gekennzeichnet als LAN-Port (und das lokale Wi-Fi).
•	Geräte: Dein Programmier-Laptop, deine Wemos-Knoten, dein Smartphone.
•	Sicherheit: Standardmäßig vertrauenswürdig. Geräte im LAN können ohne Einschränkungen direkt miteinander kommunizieren (z. B. dein Laptop mit dem MQTT-Broker auf dem Wemos).
•	IP-Bereich im Kurs: 192.168.14.xxx

WAN (Wide Area Network)
Das Weitverkehrsnetzwerk verbindet dein lokales LAN mit der Außenwelt oder einem übergeordneten Netzwerk (z. B. dem Campus-Netzwerk der HSBI oder dem weltweiten Internet).
•	Schnittstelle am Router: Gekennzeichnet als WAN-Port (oft gelb oder separat beschriftet).
•	Verbindung: Hier kommt das Netzwerkkabel hinein, das zur Ethernet-Dose im Raum führt.
•	Sicherheit: Nicht vertrauenswürdig. Die integrierte Firewall von OpenWrt blockiert standardmäßig jeglichen eingehenden Datenverkehr vom WAN-Port in das LAN, um deine IoT-Geräte vor Angriffen von außen zu schützen.

3. DHCP und DNS erforschen
Damit Geräte im Netzwerk ohne manuellen Konfigurationsaufwand sofort miteinander kommunizieren können, nutzt OpenWrt den kombinierten Hintergrunddienst dnsmasq, welcher DHCP und DNS bereitstellt.

DHCP (Dynamic Host Configuration Protocol)
DHCP ist dafür zuständig, Geräten beim Beitritt in ein Netzwerk vollautomatisch alle notwendigen Netzwerkeinstellungen zuzuweisen.
•	Wie es funktioniert: Sobald du deinen Laptop per Kabel oder WLAN mit dem Router verbindest, sendet dieser einen Ruf in das Netzwerk (DHCP Discover). Der Router antwortet und teilt dem Laptop automatisch folgende Daten mit:
1.	Eine freie, einzigartige IP-Adresse (z. B. 192.168.14.120).
2.	Die Subnetzmaske (standardmäßig 255.255.255.0), um zu wissen, wer sich im selben Netz befindet.
3.	Die Gateway-IP (192.168.14.1), also die Adresse des Routers selbst, über den alle Daten ins Internet geschickt werden müssen.
4.	Die DNS-Server-IP.

DNS (Domain Name System)
Das DNS ist das „Telefonbuch“ des Netzwerks. Da Computer intern nur mit IP-Adressen (wie 192.168.14.1) arbeiten, Menschen sich Namen aber besser merken können, übersetzt DNS lesbare Domainnamen in die zugehörigen IP-Adressen.
•	Bedeutung für unser IoT-Projekt: Wenn dein Wemos-Mikrocontroller Daten an dein Node-RED-Dashboard schicken soll, musst du im Code nicht zwingend die IP-Adresse fest eintragen. Du kannst stattdessen den in Phase 1 vergebenen Hostnamen deines Laptops oder Routers verwenden (z. B. http://team5-gateway.local). Der DNS-Dienst des Routers löst diesen Namen dann intern sekundenschnell in die IP 192.168.14.1 auf.


Phase 2: WLAN-Zugangspunkt (Access Point) einrichten

Regulierung & Kanalauswahl (ETSI / Deutschland-Anpassung)
•	Kanäle in Deutschland: Im 2,4-GHz-Band stehen in Deutschland (nach ETSI-Standard) die Kanäle 1 bis 13 zur Verfügung (im Gegensatz zu den USA, wo Kanal 12 und 13 illegal sind).
•	Auswahl des Kanals im Kursraum: Da viele Teams gleichzeitig ein Netz aufbauen, müssen wir uns koordinieren. Die Kanäle 1, 6 und 11 sind die einzigen drei Kanäle im 2,4-GHz-Spektrum, die sich frequenztechnisch nicht überlappen.


MQTT: 

netstat -a:

 Proto  Local Address          Foreign Address        State
 
  TCP    0.0.0.0:80             MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:135            MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:445            MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:5040           MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:8016           MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:9593           MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:9594           MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:9595           MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:33354          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:33370          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:33888          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:48898          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49664          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49665          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49666          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49668          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49669          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49670          MoritzLa-NB01:0           LISTENING
  
  TCP    0.0.0.0:49814          MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:8884         MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:49910       TIME_WAIT
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:59072       TIME_WAIT
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:59410       ESTABLISHED
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:61176       TIME_WAIT
  
  TCP    127.0.0.1:9592         MoritzLa-NB01:61671       TIME_WAIT
  
  TCP    127.0.0.1:19294        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:21584        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:49273        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:49672        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:49673        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:49699        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:55185        MoritzLa-NB01:0           LISTENING
  
  TCP    127.0.0.1:59410        MoritzLa-NB01:9592        ESTABLISHED
  
  TCP    127.0.0.1:62522        MoritzLa-NB01:0           LISTENING
  
  TCP    192.168.1.145:139      MoritzLa-NB01:0           LISTENING
  
  TCP    192.168.1.145:49409    172.211.123.250:https  ESTABLISHED
  
  TCP    192.168.1.145:49410    172.211.123.248:https  ESTABLISHED
  
  TCP    192.168.1.145:49909    150.171.28.11:https    ESTABLISHED
  
  TCP    192.168.1.145:50517    52.111.243.2:https     ESTABLISHED
  
  TCP    192.168.1.145:50831    52.123.135.184:https   ESTABLISHED
  
  TCP    192.168.1.145:51098    lb-140-82-121-6-fra:https  ESTABLISHED
  
  TCP    192.168.1.145:52435    lb-140-82-113-26-iad:https  ESTABLISHED
  
  TCP    192.168.1.145:54030    20.150.179.224:8883    ESTABLISHED
  
  TCP    192.168.1.145:59409    lb-140-82-113-21-iad:https  ESTABLISHED
  
  TCP    192.168.1.145:59411    sslvpn:https           SYN_SENT
  
  TCP    192.168.1.145:60769    52.111.243.2:https     ESTABLISHED
  
  TCP    192.168.1.145:61437    lcfrai-in-f188:5228    ESTABLISHED
  
  TCP    192.168.1.145:61673    52.111.227.13:https    TIME_WAIT
  
  TCP    192.168.1.145:61926    40.79.150.123:https    ESTABLISHED
  
  TCP    192.168.1.145:63100    52.112.120.223:https   ESTABLISHED
  
  TCP    192.168.1.145:63604    ec2-18-158-187-80:https  ESTABLISHED
  
  TCP    192.168.1.145:64228    199.232.214.172:http   ESTABLISHED
  
  TCP    [::]:80                MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:135               MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:445               MoritzLa-NB01:0           LISTENING
  
  
  TCP    [::]:8016              MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:9593              MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:9594              MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:9595              MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:33370             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:48898             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49664             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49665             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49666             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49668             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49669             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49670             MoritzLa-NB01:0           LISTENING
  
  TCP    [::]:49814             MoritzLa-NB01:0           LISTENING
  
  TCP    [::1]:42050            MoritzLa-NB01:0           LISTENING
  
  TCP    [::1]:49273            MoritzLa-NB01:0           LISTENING
  
  TCP    [::1]:49273            MoritzLa-NB01:49274       ESTABLISHED
  
  TCP    [::1]:49274            MoritzLa-NB01:49273       ESTABLISHED
  
  TCP    [::1]:49671            MoritzLa-NB01:0           LISTENING
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:49275  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:49667  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:49674  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:51698  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:51712  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:52366  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:52542  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:52702  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:52898  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:53139  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:53317  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:54090  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:54121  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:54785  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:55114  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:55668  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:55769  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:56408  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:56429  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:56920  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:57687  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:58195  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:58447  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:58891  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:58958  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:60831  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:60986  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:61488  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:61639  OpenWrt:domain         TIME_WAIT
  
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:61840  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:62202  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:62506  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:63799  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:63997  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:64590  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:64778  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:64834  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:65152  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:65500  OpenWrt:domain         TIME_WAIT
  
  TCP    [fd74:3356:188c:0:f453:c605:9876:a2fa]:65532  OpenWrt:domain         TIME_WAIT
  
  UDP    0.0.0.0:123            :
  
  UDP    0.0.0.0:5050           :
  
  UDP    0.0.0.0:5353           :
  
  UDP    0.0.0.0:5353           :
  
  UDP    0.0.0.0:5353           :
  
  UDP    0.0.0.0:5355           :
  
  UDP    0.0.0.0:9595           :
  
  UDP    0.0.0.0:33354          :
  
  UDP    0.0.0.0:33355          :
  
  UDP    0.0.0.0:33371          :
  
  UDP    0.0.0.0:33999          :
  
  UDP    0.0.0.0:48899          :
  
  UDP    0.0.0.0:49346          :
  
  UDP    0.0.0.0:49665          :
  
  UDP    0.0.0.0:49666          :
  
  UDP    0.0.0.0:49667          :
  
  UDP    0.0.0.0:49668          :
  
  UDP    0.0.0.0:49670          :
  
  UDP    0.0.0.0:49675          108.177.15.101:443
  
  UDP    0.0.0.0:50082          :
  
  UDP    0.0.0.0:51261          142.251.157.119:443
  
  UDP    0.0.0.0:53536          :
  
  UDP    0.0.0.0:59848          :
  
  UDP    0.0.0.0:60012          142.251.127.93:443
  
  UDP    0.0.0.0:61647          142.251.110.93:443
  
  UDP    0.0.0.0:64549          142.250.154.139:443
  
  UDP    127.0.0.1:49664        127.0.0.1:49664
  
  UDP    127.0.0.1:49671        :
  
  UDP    127.0.0.1:49672        :
  
  UDP    127.0.0.1:49674        :
  
  UDP    127.0.0.1:49676        127.0.0.1:49676
  
  UDP    192.168.1.145:137      :
  
  UDP    192.168.1.145:138      :
  
  UDP    192.168.1.145:55486    :
  
  UDP    192.168.1.145:55487    :
  
  UDP    192.168.1.145:59679    :
  
  UDP    [::]:123               :
  
  UDP    [::]:5353              :
  
  UDP    [::]:5353              :
  
  UDP    [::]:5355              :
  
  UDP    [::]:9595              :
  
  UDP    [::]:33371             :
  
  UDP    [::]:48899             :
  
  UDP    [::]:49346             :
  
  UDP    [::]:49669             :
  
  UDP    [::]:50082             :
  
  UDP    [::]:53536             :
  
  UDP    [::]:59848             :
  
  UDP    [::1]:49673            :
  
  UDP    [fd74:3356:188c:0:6c33:f3f6:3354:daf7]:51408  :
  
 
netsh wlan show interfaces:
There is 1 interface on the system:
 
    Name                   : Wi-Fi
    Description            : Intel(R) Wi-Fi 6E AX211 160MHz
    GUID                   : 463086fd-a786-4485-9294-72e2a5819ecb
    Physical address       : 30:05:05:68:9a:4d
    Interface type         : Primary
    State                  : connected
    SSID                   : MCU_ProgrammingFBML
    AP BSSID               : 94:83:c4:06:d0:36
    Band                   : 5 GHz
    Channel                : 36
    Connected Akm-cipher   : [ akm = 00-0f-ac:08, cipher =  00-0f-ac:04 ]
    Network type           : Infrastructure
    Radio type             : 802.11ac
    Authentication         : WPA3-Personal  (H2E)
    Cipher                 : CCMP
    Connection mode        : Profile
    Receive rate (Mbps)    : 433.3
    Transmit rate (Mbps)   : 433.3
    Signal                 : 92%
    Rssi                   : -39
    Profile                : MCU_ProgrammingFBML
    QoS MSCS Configured         : 0
    QoS Map Configured          : 0
    QoS Map Allowed by Policy   : 0


Bilder einfügen: 

https://github.com/MoLamkemeyer/iot-portfolio-template/tree/main/Modul%2003/Bilder 

Alle Dateien finden Sie auch bei meinem Partner: 
<Frederik Bröckling>, [Frederik Bröckling](https://github.com/fbroeckling/Portfolio-of-Frederik-Br-ckling/tree/main/Module03)
































