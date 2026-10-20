# Software Engineering I - Teilaufgabe 1 (Anforderungsanalyse und Planungsphase)

## Abgabedokument - Teilaufgabe 1 (Anforderungsanalyse und Planungsphase)

- Kariavkina Elizaveta
- 12450960


## Aufgabe 1: Anforderungsanalyse

### Quellen dokumentieren - Aufgabe 1: Anforderungsanalyse

Die Anforderungen 1-7 wurden aus Spielidee[https://moodle.univie.ac.at/mod/book/view.php?id=19904280] abgeleitet

### Typ der Anforderung: funktional

**Anforderung 1**

- **Anforderung**: Regisrtrierung am Server - Nach Start MUSS der Client beim Server registrieren
- **Bezugsquelle**: Spielidee, **Initial gilt es am Server ein neues Spiel anzufordern. Dieser erste Schritt wird noch von einem Menschen durchgeführt, alles danach erfolgt immer vollautomatisch durch eine Client/KI-Implementierung. Nach Start des Clients registrieren sich die KIs für das Spiel am Server..**

**Anforderung 2**

- **Anforderung**: Bewegung zum Schatz - Der Client muss seine Spielfigur zum Schatz bewegen, sobald KI das gefunden hat.
- **Bezugsquelle**: Spielidee, **Sobald eine KI "ihren" Schatz gefunden bzw. aufgedeckt hat, muss sie ihre Spielfigur zu diesem bewegen, um ihn aufnehmen zu können.  **

**Anforderung 3**

- **Anforderung**: Warte auf Aktionen - Der Client darf nicht eine Aktion einfügen, wenn anderer Spieler in der Reihe ist.
- **Bezugsquelle**: Spielidee, **Eine KI darf aber keine Aktion setzen solange die andere KI an der Reihe ist**

### Typ der Anforderung: nicht funktional

**Anforderung 4**

- **Anforderung**: Antwortzeit per Spielaktion - Sobald der Client an der Reihe ist, muss der Client in hoechsents 5 Senkunden ANtwort am Server schicken
- **Bezugsquelle**: Spielidee, **Für jede dieser rundenbasierten Spielaktion hat die KI maximal 5 Sekunden Bedenkzeit... Sollten diese Bedingungen nicht erfüllt werden, verliert die KI, welche gerade an der Reihe ist, das Spiel automatisch und der zugehörige menschliche Spieler bekommt dies vom Client mitgeteilt.**

**Anforderung 5**

- **Anforderung**: Spieldauer - Während eines Spiels muss der Client seine Spielaktionen so schnell senden, dass das gesamte Spielzeit dauert maximal 10 minuten
- **Bezugsquelle**: Spielidee, **Insgesamt dauert ein Spiel maximal 10 Minuten.**

**Anforderung 6**

- **Anforderung**: Rundenbegrenzung. Ab den Kartenaustausch muss der Client gegnerische Berg mit ihrem Schatz erreichen, bevor Spiel 320 Runde hat.
- **Bezugsquelle**: Spielidee, **Um die Spiele für die Zuschauer spannend zu gestalten, wurde festgelegt, dass ein Spiel insgesamt nicht länger als 320 Spielaktionen (und damit 320 Runden) dauern darf**

### Typ der Anforderung: Designbedingung

**Anforderung 7**

- **Anforderung**: - Benutzeroberflaeche - Waehrend des Spiels muss der Client alle Ausgaben fuer den ANwender ausschliesslich ueber ein Command-Line-Interface darstellen
- **Bezugsquelle**: Spielidee, **Während des Spiels müssen die Karte und deren bekannten Eigenschaften und wichtige Spielzustände von den Clients mittels command-line interface (CLI) für Anwender nachvollziehbar visualisiert werden.**

- **Anforderung**: - Client/Server Arckitektur - Der Client muss ein Teil des Client/Server Arckitektur sein, und muss nur durch Server Spieldaten austausschen (Karte, Spielstatus, AKtionen)
- **Bezugsquelle**: Spielidee, **Dabei werden die KIs von einem Server unterstützt der beide Clients koordiniert, Datenaustausch ermöglich, als Schiedsrichter auftritt und für Clients Daten speichert, aktualisiert und auswertet. Die Grobarchitektur ist damit als klassische Client/Server Architektur vorgegeben. **


