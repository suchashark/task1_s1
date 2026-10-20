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

- **Anforderung**: Aufnehmen eines Schatzes - Das Aufnehmen eines Schatzes muss durchgeführt werden, wenn Spielfigur das Spielfeld mit einem Schatze der Karte betritt
- **Bezugsquelle**: Spielidee, **Das Aufnehmen eines Schatzes und die Übernahme der Burg erfolgen automatisch durch den Server, sobald eine Spielfigur das jeweilige Spielfeld der Karte betritt.  **

**Anforderung 3**

- **Anforderung**: Warte auf Aktionen - Der Client muss nicht eine Aktion einfügen, wenn Reihe nicht leer ist.
- **Bezugsquelle**: Spielidee, **Eine KI darf aber keine Aktion setzen solange die andere KI an der Reihe ist**

### Typ der Anforderung: nicht funktional

**Anforderung 4**

- **Anforderung**: Antwortzeit per Spielaktion - Sobald der Client an der Reihe ist, muss der Client in hoechsents 5 Senkunden ANtwort am Server schicken
- **Bezugsquelle**: Spielidee, **Für jede dieser rundenbasierten Spielaktion hat die KI maximal 5 Sekunden Bedenkzeit... Sollten diese Bedingungen nicht erfüllt werden, verliert die KI, welche gerade an der Reihe ist, das Spiel automatisch und der zugehörige menschliche Spieler bekommt dies vom Client mitgeteilt.**

**Anforderung 5**

- **Anforderung**: [Name plus Anforderung]
- **Bezugsquelle**: [Spielidee, **Zitat**]

**Anforderung 6**

- **Anforderung**: [Name plus Anforderung]
- **Bezugsquelle**: [Spielidee, **Zitat**]

### Typ der Anforderung: Designbedingung

**Anforderung 7**

- **Anforderung**: - Benutzeroberflaeche - Waehrend des Spiels muss der Client alle Ausgaben fuer den ANwender ausschliesslich ueber ein Command-Line-Interface darstellen
- **Bezugsquelle**: Spielidee, **Während des Spiels müssen die Karte und deren bekannten Eigenschaften und wichtige Spielzustände von den Clients mittels command-line interface (CLI) für Anwender nachvollziehbar visualisiert werden.**

