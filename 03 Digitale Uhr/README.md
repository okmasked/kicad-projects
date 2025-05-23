# Klärung der Spezifikation

- Wird es eine Uhr, eine Stoppuhr oder ein Countdown-Timer (Eier-Uhr)?
	- Uhr; broken clock is right twice a day
- Wie genau soll der Zähler sein?
	- Stunden, Minuten, evtl. Sekunden;
- Wie viele Stellen werden benötigt?
	- 4 bis 6 (2 für stunden, 2 für minuten, 2 für sekunden);
- 7-Segment-Anzeige als LCD oder LED-Anzeige?
	- LED;
- Welche Funktionen sind nötig?
	- reset auf 00:00 nach dem +1 minute auf 23:59 sind;
	- einstellen der zeit mit einem taster (+/- 1 zur minute/sekunde);
- Wie viele Tasten werden für diese Funktionen benötigt?
	- 2 Taster für einstellen der zeit (einmal für +1 und einmal -1);
- Wie wird die Uhr zu beginn eingestellt?
	- bei 00:00;
- Wie wird die Uhr in Etwa Aussehen?
	- 4 dekaden-zähler, die die zeit anzeigen. (6, wenn sekunden dabei sind);
	- für jeden zähler ein dekoderbausten(oder einen mit dekoder Bausetein eingebaut);
	- für jeden dekoderbaustein eine 7-Segment-Anzeige (Led);
- Wie groß wird sie (Abmessungen)?
	- Nach
- Wie erfolgt die Spannungsversorgung?
	- 3 AAA Batterien(Zink-Kohle-Zelle) jeweils 1,5 V, so geschalten das es 4,5 V sind;
-----------------------------------------------
# Blockschaltbild

- Aus welchen funktionellen Blöcken besteht die Uhr?
- Welche Signale bzw. wie viele Signale werden zwischen den Blöcken benötigt?
- Zeichne für jeden Block ein detaillierteres Blockschaltbild.

------------------------------------------------
# Quellen
- bild von quearzoszillator prinzipschaltung: https://elektro.turanis.de/html/prj398/index.html
- bild von enpreller eines Schalters: https://www.ganssle.com/debouncing-pt2.htm
- immense Hilfe: https://jacobsa.github.io/circuits/
------------------------------------------------
# Documentation
07.03.2025
- Dokumentieren das die Schaltung für den oszi schwingt
------------------------------------------------
27.03.2025 (1-stündige Einheit)
- Zählerbaustein cd40110 anschauen
- bcd zu 7-Segment converter suchen (4511)
------------------------------------------------
28.03.2025 (2-stündige Einheit)

- Alle Dateien die wichtig für das projekt sind verloren :(
- Arbeitsverlauf: 
	- Schaltung in multisim neu aufgebaut (vom frequenzteiler)
	- wiedersimulieren von der schaltung
	- Word Dokument neu anlegen und schreiben (1. Taktgeber fertig, 2. Zähler angefangen)
	- Schaltung für den Zähler in Multisim aufbauen (W.I.P.)
------------------------------------------------
03.04.2025 (1-stündige Einheit)

- Über mögliche Störfaktoren in der Schaltung geredet und wie man sie beheben kann.
	- Stützkondensator für die CMOS bausteine
------------------------------------------------
04.04.2025 (2-stündige Einheit)

 - Einbauen der gestern besprochenen behebungen gegen die Störfaktoren
- neuaufbau der zählerschaltung, da zu unübersichtlich zuvor
	Note: Es sind keine Stützkondensatoren, weil keine Vcc und GND Inputs sind an den Bausteinen
- Die Schaltung hat jetzt, anstatt den digital Displays, 4511 (7-Segment Decoder) und normalen 7-Segment Displays
- Schaltung noch nicht operationstüchtig, da ich noch nicht die ganze Logik verbunden habe
- Schaltung braucht noch auf und ab Zähler
------------------------------------------------
24.04.2025 (1-stündige Einheit)

- Besprochen, wie Schalter synchronisiert und entprellt (2 RS FFs) werden
------------------------------------------------
25.04.2025 (2-stündige Einheit)

- Von Common Anode 7-Segment Displays auf Common Cathode wechseln und neu verkabeln
	- Wurden auch von 6 Single 7-Segment Anzeigen auf 3 Dual 7-Segment Anzeigen geändert
- Die Schaltung zu einer Uhr machen indem die Reset-Logik gemacht wird (noch nicht fertig, wird wahrscheinlich zuhause gemacht)
	- Reset-Logik muss noch überarbeitet werden, da eine 6 für eine kurze Zeit gesehen werden kann auf der 7-Segment Anzeige
- Wenn die Reset-Logik fertig ist kann ich mit peripherien wie Power On Rest (POR) und  entprellung & synchronisation von Schaltern arbeiten.\
  Ebenfalls müssen andere Sachen wie, änderung der Zeit berücksichtigt werden
------------------------------------------------
08.05.2025 (1-stündige Einheit)

- Suppliert
------------------------------------------------
09.05.2025 (2-stündige Einheit)
- Bus über 2 seiten verbinde:
	-> Doppel click auf bus leitung\
	-> Leitung benennen\
	-> Seitenübergreifend einfügen und id setzen\
	-> profit
- Reset-Logik funktioniert jetzt.
- Power On Reset ist jetzt dran.\
	Keine ahnung warum, aber der funktioniert bei mir nicht. Werd ich noch investigieren. 
-------------------------------------------------
15.05.2025 (1-stündige Einheit)
- Das meiste was wir gemacht haben betrifft die timer, nicht die Uhr :sob:
-------------------------------------------------
16.05.2025 (2-stündige Einheit)

- Power on Reset funktioniert jetzt
	- Das Problem: ich habe die Reset-Logik falsch verbunden.\
	  Der Power On Reset war einfach nach belieben verbunden mit den MR pins.\
	  Das habe ich lösen können indem ich es einfach mit einem OR-Gate verknüpfe and den MR.
- Jetzt muss ich testen ob die Reset-Logik funktioniert.\
  Der Testmodus muss eingebaut werden.\
  Testen war erfolgreich und ich konnte ein paar fehler entfernen.
- Nächster schritt ist die entprellung der Taster.
-------------------------------------------------
21.05.2025 (1-stündige Einheit)

   - versucht ni-multisim via wine zu installieren\
       nicht erfolgreich, da der package manager die EULA nicht anzeigen kann.\
       vielleicht nochmal testen mit dem offline installer, aber ich habe sonst keine große hoffnung.
-------------------------------------------------
22.05.2025 (2-stündige Einheit)

- betreffemd gestern, man kann multisim nicht mit wine installieren da:
	+ Das NI license Agreement nicht angezeigt werden kann durch den package manager
	+ Ich keine NI driver installiert habe
	+ Kein offizieller arch support existiert (nur windows, suse, redhat und ubuntu)
- Lösungen zu diesem problem wären:
	+ installieren über .rpm (redhat package manager) dateien.
	+ ein PKGBUILD schreiben und dann über pacman installieren
	+ windows vm verwenden oder gar dualbooten
- Ich werde das definitiv später nochmal probieren, da in diesen 2 stunden nicht genug zeit ist\
  um das alles zu recherechieren und dann auch noch meine Arbeit zu machen
	- Nachdem das fertig ist, werde ich mich an den einstell mechanismus für die uhr wenden (sekunden, minuten und stunden auf knopfdruck ändern)
	- mögliche wege:
		+ 3 knöpfe: einer zum setzen in den "set" modus, ein zweiter für das einstellen (+1 pro click) und ein dritter für toggeln zwischen zeiten (stunden minuten sekunden)
		+ für jede 1er stelle der zeit einen eigenen taster, mit noch immer einem "set" modus	
