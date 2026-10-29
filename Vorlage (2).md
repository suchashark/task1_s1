## Abgabedokument - Teilaufgabe 1 (Anforderungsanalyse und Planungsphase)

### Persönliche Daten, bitte vollständig ausfüllen:

- Nachname, Vorname: Kariavkina, Elizaveta
- Matrikelnummer: 12450960



## Aufgabe 1: Anforderungsanalyse

### Quellen dokumentieren - Aufgabe 1: Anforderungsanalyse

- **Kurzbeschreibung der übernommenen Teile**: *Die Anforderungen wurden aus Spielidee abgeleitet. Alle Texte sind eigene Formulierungen.*
- **Quellen der übernommenen Teile**: *[Spielidee](https://moodle.univie.ac.at/mod/book/view.php?id=19904280],  [Spielaufzeichnung](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/ExampleGame.mkv),[Block 2](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/Software%20Engineering%20I%20Anforderungsanalyse%20Unterlagen.pdf), Vorlage.md.*

### Typ der Anforderung: funktional

**Anforderung 1**

- **Anforderung**: Regisrtrierung am Server - Nach Start MUSS der Client sich beim Server registrieren
- **Bezugsquelle**: Spielidee, **Initial gilt es am Server ein neues Spiel anzufordern. Dieser erste Schritt wird noch von einem Menschen durchgeführt, alles danach erfolgt immer vollautomatisch durch eine Client/KI-Implementierung. Nach Start des Clients registrieren sich die KIs für das Spiel am Server..**

**Anforderung 2**

- **Anforderung**: Bewegung zum Schatz - Der Client muss seine Spielfigur zum Schatz bewegen, sobald das eigene SChatz gefunden wurde.
- **Bezugsquelle**: [Spielidee, **Sobald eine KI "ihren" Schatz gefunden bzw. aufgedeckt hat, muss sie ihre Spielfigur zu diesem bewegen, um ihn aufnehmen zu können**]

**Anforderung 3**

- **Anforderung**: Warte auf Aktionen - Der Client darf nicht eine Spielaktion an Server senden, wenn anderer Spieler an der Reihe ist.
- **Bezugsquelle**: Spielidee, **Eine KI darf aber keine Aktion setzen solange die andere KI an der Reihe ist**

### Typ der Anforderung: nicht funktional

**Anforderung 4**

- **Anforderung**: Antwortzeit per Spielaktion
- **Bezugsquelle**: Spielidee, **Für jede dieser rundenbasierten Spielaktion hat die KI maximal 5 Sekunden Bedenkzeit... Sollten diese Bedingungen nicht erfüllt werden, verliert die KI, welche gerade an der Reihe ist, das Spiel automatisch und der zugehörige menschliche Spieler bekommt dies vom Client mitgeteilt**

**Anforderung 5**

- **Anforderung**: Spieldauer - Während eines Spiels muss der Client seine Spielaktionen so schnell senden, dass das gesamte Spielzeit dauert maximal 10 minuten
- **Bezugsquelle**: Spielidee, **Insgesamt dauert ein Spiel maximal 10 Minuten.**

**Anforderung 6**

- **Anforderung**: Effizienz der Weg - Ab den Kartenaustausch muss der Client gegnerische Burg mit ihrem Schatz erreichen, bevor Spiel 320 Runde hat
- **Bezugsquelle**: Spielidee, **Um die Spiele für die Zuschauer spannend zu gestalten, wurde festgelegt, dass ein Spiel insgesamt nicht länger als 320 Spielaktionen (und damit 320 Runden) dauern darf**

### Typ der Anforderung: Designbedingung

**Anforderung 7**

- **Anforderung**: Benutzeroberflaeche - Waehrend des Spiels muss der Client alle Ausgaben fuer den Anwender ausschliesslich ueber ein Command-Line-Interface darstellen
- **Bezugsquelle**: Spielidee, **Während des Spiels müssen die Karte und deren bekannten Eigenschaften und wichtige Spielzustände von den Clients mittels command-line interface (CLI) für Anwender nachvollziehbar visualisiert werden**


## Aufgabe 2: Anforderungsdokumentation

### Quellen dokumentieren - Aufgabe 2: Anforderungsdokumentation

- **Kurzbeschreibung der übernommenen Teile**: *Die Business Rules, Szenarien und Zahlenwerte wurden aus Spielidee abgeleitet. Alle Texte sind eigene Formulierungen.*
- **Quellen der übernommenen Teile**: *[Spielidee](https://moodle.univie.ac.at/mod/book/view.php?id=19904280],  [Spielaufzeichnung](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/ExampleGame.mkv), [Block 2](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/Software%20Engineering%20I%20Anforderungsanalyse%20Unterlagen.pdf), [Netzwerkprotokoll](Netzwerkprotokoll), [Beispiel einer Vorlage zur Anforderungsdokumentation der IEEE](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255152/srs_template-ieee.doc?time=1790373138896), Vorlage.md.*

### Anforderungsüberblick

- **Name**: Kartenhälfte erzeugen
- **Beschreibung und Priorität**: [Nach der Registrierung erzeugt der Client eine Kartenhälfte mit 5 x 10 Feldern. Nach der Sendung der Kartenhälfte und wartet auf Überprüfung vom Server. Mit nicht gültige Kartenhälfte ist das Spiel verloren, deshalb ist die Priorität hoch]
- **Relevante Anforderungen**: [Anforderung 1, Anforderung 3, Anforderung 4, Anforderung 7]
- **Relevante Business Rules**: [
- Eine Karte besteht aus 5 x 10 Feldern
- Jedes Feld repräsentiert genau eine von drei möglichen Terrainarten: Wasser, Wiese oder Berg
- Kartenhälften müssen zufällig mit Algorithmen generiert und nicht statisch vorgegeben werden
- Jede Kartenhälfte muss mindestens 10% Bergfelder, 48% Wiesenfelder, 14% Wasserfelder
- Es muss genau eine Burg auf der Kartenhälfte sein
- Jeder potentiell betretbare Felder muss betretbar sein
- Mindestens 51% der Felder jedes Randes der Kartenhälfte müssen betretbar sein
- Der Client verliert das Spiel automatisch, wenn seine Kartenhälfte ungültig ist.     ]

### Impuls/Ergebnis - Typisches Szenario



**Vorbedingungen:**

- Das Client hat sich erfolgreich am Server für ein Spiel registriert.
- Der Client besitzt eindeutige SpielID.
- Es ist nächstes Schritt nach der Registrierung, bei dem Client Kartenhälfte generieren muss.

**Hauptsächlicher Ablauf:**

- **Impuls** Der Client startet den Algorithmus fuer Generierung 5 x 10 Kartenhälfte.
- **Ergebnis** Kartenhälfte wird erstellt, die alle Business Rules erfuellt.

- **Impuls** Der Client sendet die Kartenhälfte zum Server.
- **Ergebnis** Der Server empfaengt die Kartenhälfte. validiert sie fuer Business rules und schickt ResponseEnvelope.

- **Impuls** Der Client bekommt ResponseEnvelope und bearbeitet es.
- **Ergebnis** Der Client stellt fest, dass  Kartenhälfte akzeptiert ist.

**Nachbedingungen:**

- Die Kartenhälfte ist am Server validierd und akzeptiert
- Der Client geht in dem naechsten Spielzustand.
  
### Impuls/Ergebnis - Alternativszenario


**Vorbedingungen:**


- Das Client hat sich erfolgreich am Server für ein Spiel registriert.
- Der Client besitzt eindeutige SpielID.
- Es ist nächstes Schritt nach der Registrierung, bei dem Client Kartenhälfte generieren muss.
- Der Client verfügt über einen Validierungsalgorithmus, um Kartenhälfte zu überprüfen

**Hauptsächlicher Ablauf:**

- **Impuls** Der Client startet den Algorithmus für Generierung 5 x 10 Kartenhälfte und überprüft sie.
- **Ergebnis** Kartenhälfte wird erstellt, die bei Validierungsalgorithmus nicht akzeptiert wurde.

- **Impuls** Der Client bekommt das Ergebnis der Validierung und generiert 5 x 10 Kartenhälfte mit Validierung danach.
- **Ergebnis** Kartenhälfte wird erstellt, die bei Validierungsalgorithmus akzeptiert wurde.

- **Impuls** Der Client sendet die Kartenhälfte zum Server.
- **Ergebnis** Der Server empfaengt die Kartenhälfte. validiert sie fuer Business rules und schickt ResponseEnvelope.

- **Impuls** Der Client bekommt ResponseEnvelope und bearbeitet es.
- **Ergebnis** Der Client stellt fest, dass  Kartenhälfte akzeptiert ist.

**Nachbedingungen:**

- Die Kartenhälfte ist am Server validiert und akzeptiert
- Der Client geht in dem naechsten Spielzustand.
- Obwohl extra Zeit wird gebraucht, um Kartenhälfte selbst zu validieren, das erhöht die Möglichkeit, das Kartenhälfte beim Server akzeptiert wurde

### Impuls/Ergebnis - Fehlerfall



**Vorbedingungen:**

- Das Client hat sich erfolgreich am Server für ein Spiel registriert.
- Der Client besitzt eindeutige SpielID.
- Das Client generiert Kartenhälfte, die gegen ein oder mehrere Business Rules verstößt.
- 
**Hauptsächlicher Ablauf:**

- **Impuls** Der Client startet den Algorithmus fuer Generierung 5 x 10 Kartenhälfte.
- **Ergebnis** Kartenhälfte wird erstellt, die nicht alle Business Rules erfüllt.

- **Impuls** Der Client sendet die Kartenhälfte zum Server.
- **Ergebnis** Der Server empfängt die Kartenhälfte checkt sie für Business Rules und schickt ResponseEnvelope mit Fehler.

- **Impuls** Der Client bekommt ResponseEnvelope und bearbeitet es.
- **Ergebnis** Der Client hat verloren.
  

**Nachbedingungen:**
- Der Client hat automatisch verloren
- Es gibt Visualisierung in CLI
  Der Client sendet keine weiteren Aktionen   
### Benutzergeschichten

- Als Anwender möchte ich visualisiere Kartenhälft im CLI sehen, um Fehler zu erkennen.
- Als KI möchte ich eigene Validierungsalgorithmus haben, um Fehler rechtzeitig zu bemerken.
- 
### Benutzerschnittstelle

- .  - Wasser
- + - Berg
- _ - Wiesen
- /# - Burg
- 
    ``` Karte:   ```
     ```..........   ```
     ```..........   ```
     ```..++......   ```
     ```......_...   ```
     ```..........   ```
     ```Validator: Karte ist ungueltig   ```

### Externe Schnittstellen

-Format: ASCII, so dass in Terminal printbar
-

## Aufgabe 3: Architektur entwerfen, modellieren und validieren

Alle Diagramme in dieses Kapitel als SVG einfügen. 

### Quellen dokumentieren - Aufgabe 3: Architektur entwerfen, modellieren und validieren

- **Kurzbeschreibung der übernommenen Teile**: *Spielidee und Best Practices wurden aus Moodle Seite abgeleitet. Alle Texte sind eigene Formulierungen. *
- **Quellen der übernommenen Teile**: *[Spielidee](https://moodle.univie.ac.at/mod/book/view.php?id=19904280],  [Spielaufzeichnung](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/ExampleGame.mkv), [Block 2](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/Software%20Engineering%20I%20Anforderungsanalyse%20Unterlagen.pdf), [Netzwerkprotokoll](Netzwerkprotokoll), Vorlage.md.*
### Klassendiagramm

[Klassendiagramm.svg]

### Sequenzdiagramm 1

[Sequenzdiagramm_1.svg]

### Sequenzdiagramm 2

[Sequenzdiagramm_2.svg]
