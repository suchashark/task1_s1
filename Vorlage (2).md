## Abgabedokument - Teilaufgabe 1 (Anforderungsanalyse und Planungsphase)

### Persönliche Daten, bitte vollständig ausfüllen:

- Nachname, Vorname: Kariavkina Elizaveta
- Matrikelnummer: 12450960



## Aufgabe 1: Anforderungsanalyse

### Quellen dokumentieren - Aufgabe 1: Anforderungsanalyse

- **Kurzbeschreibung der übernommenen Teile**: *Die Business Rules, Szenarien und Zahlenwerte wurden aus Spielidee abgeleitet.Alle Texte sind eigene Formulierungen.*
- **Quellen der übernommenen Teile**: *Die Anforderungen 1-7 wurden aus Spielidee[https://moodle.univie.ac.at/mod/book/view.php?id=19904280] abgeleitet*

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

- **Anforderung**: Benutzeroberflaeche - Waehrend des Spiels muss der Client alle Ausgaben fuer den ANwender ausschliesslich ueber ein Command-Line-Interface darstellen
- **Bezugsquelle**: Spielidee, **Während des Spiels müssen die Karte und deren bekannten Eigenschaften und wichtige Spielzustände von den Clients mittels command-line interface (CLI) für Anwender nachvollziehbar visualisiert werden**


## Aufgabe 2: Anforderungsdokumentation

### Quellen dokumentieren - Aufgabe 2: Anforderungsdokumentation

- **Kurzbeschreibung der übernommenen Teile**: *Die Business Rules, Szenarien und Zahlenwerte wurden aus Spielidee abgeleitet. Alle Texte sind eigene Formulierungen.*
- **Quellen der übernommenen Teile**: [Spielidee](https://moodle.univie.ac.at/mod/book/view.php?id=19904280],  [Spielaufzeichnung](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/ExampleGame.mkv),  
* [Block 2](https://moodle.univie.ac.at/pluginfile.php/32629322/mod_lesson/page_contents/255150/Software%20Engineering%20I%20Anforderungsanalyse%20Unterlagen.pdf), Vorlage.md.

### Anforderungsüberblick

- **Name**: Kartenhälfte erzeugen
- **Beschreibung und Priorität**: [Nach der Registrierung erzeugt der Client eine Kartenhälfte mit 5 x 10 Feldern. Nach der Sendung der Kartenhälfte und wartet auf Überprüfung vom Server. Mit nicht gültige Kartenhälfte ist das Spiel verloren, deshalb ist die Priorität hoch]
- **Relevante Anforderungen**: [Anforderung 1, Anforderung 3, Anforderung 4, Anforderung 7]
- **Relevante Business Rules**: [
- Eine Karte besteht  aus 5 x 10 Feldern
- Jedes Feld repräsentiert genau eine von drei möglichen Terrainarten: Wasser, Wiese oder Berg
- Kartenhälften müssen zufällig mit Algorithmen generiert und nicht statisch vorgegeben werden
- Jede Kartenhälfte muss mindestens 10% Bergfelder, 48% Wiesenfelder, 14% Wasserfelder
- Es muss genau eine Burg auf der Kartenhälfte sein
- Jeder potentiell betretbare Felder muss betretbar sein
- Mindestens 51% der Felder jedes Randes der Kartenhälfte müssen betretbar sein
- Der Client verliert, wenn seine Kartenhälfte ungültig ist.     ]

### Impuls/Ergebnis - Typisches Szenario

[Welche Schritte werden durchlaufen, um das der Anforderung zugehörige Verhalten auszulösen bzw. zu nutzen, und was ist das unmittelbare Ergebnis jedes Schrittes? Die Impuls-/Ergebnis-Pärchen entsprechend kennzeichnen. Mehrere aufeinander aufbauende bzw. zusammengehörige Pärchen definieren. Diese dienen dazu, den Stakeholdern relevante Abläufe, Bedingungen und Reihenfolgen zu verdeutlichen. Sich dieser Pärchen bewusst zu werden, hilft bei der späteren Architektur in Aufgabe 3 (z. B. wann wird welche Methode aufgerufen).] 

**Vorbedingungen:**

- [Stellen Sie sicher, dass erkennbar ist welche Schritte dazu führen, dass eine Anforderung relevant wird (Vorbedingungen).]

**Hauptsächlicher Ablauf:**

- [Schritte des Ablaufs beschreiben.]

**Nachbedingungen:**

- [Auch die Auswirkung des hauptsächlichen Ablaufs und die direkt anschließenden Schritte müssen angeführt werden (Nachbedingungen). Dies soll EntwicklerInnen verdeutlichen wie sich eine Anforderung in den typischen Programmablauf einbettet.]

### Impuls/Ergebnis - Alternativszenario

[Ein Alternativszenario, das vergleichbare Vorbedingungen (zum typischen Szenario) aufweist, jedoch sich im Ablauf und Nachbedingungen unterscheidet. Hilft sich Variationen und Verzweigungen im Ablauf bewusst zu werden.]. 

**Vorbedingungen:**

- [Stellen Sie sicher, dass erkennbar ist welche Schritte dazu führen, dass eine Anforderung relevant wird (Vorbedingungen).]

**Hauptsächlicher Ablauf:**

- [Schritte des Ablaufs beschreiben.]

**Nachbedingungen:**

- [Auch die Auswirkung des hauptsächlichen Ablaufs und die direkt anschließenden Schritte müssen angeführt werden (Nachbedingungen). Dies soll EntwicklerInnen verdeutlichen wie sich eine Anforderung in den typischen Programmablauf einbettet.]

### Impuls/Ergebnis - Fehlerfall

[Erwarteten Fehlerfall beschreiben und wie dieser gehandhabt wird. Dies ist besonders relevant, da ansonsten nur Gutfälle berücksichtigt werden was im Produktiveinsatz schnell nicht mehr ausreichend ist.]

**Vorbedingungen:**

- [Stellen Sie sicher, dass erkennbar ist welche Schritte dazu führen, dass eine Anforderung relevant wird (Vorbedingungen).]

**Hauptsächlicher Ablauf:**

- [Schritte des Ablaufs beschreiben, insbesondere wie der Fehler entstanden ist und wie er behandelt wird.]

**Nachbedingungen:**

- [Auch die Auswirkung des hauptsächlichen Ablaufs und die direkt anschließenden Schritte müssen angeführt werden (Nachbedingungen). Dies soll EntwicklerInnen verdeutlichen wie sich eine Anforderung in den typischen Programmablauf einbettet.]

### Benutzergeschichten

- [Zugehörige User Stories, welche die Anforderung genauer beschreiben mit folgendem Aufbau: Als \<Rolle> möchte ich \<Ziel/Wunsch> um s folgendes \<Nutzen> zu erreichen. Geeignete Rollen wären: (Menschlicher) Anwender, Client, KI oder Server. Darauf achten alle drei Themen abzudecken (Rolle, Ziel, Nutzen).]

### Benutzerschnittstelle

- [Geben Sie hier ein Beispiel/Mockup für die zugehörige Benutzerschnittstelle an, um darzustellen welchen Einfluss diese Anforderung auf die CLI Benutzeroberfläche hat. Dies soll Ihnen ermöglichen schon vor dem Entwurf festzustellen was und wie Informationen in einer Anwendung dargestellt werden – was wiederum beim späteren Entwurf der Architektur hilft. Da nur CLI verlangt ist kann das Beispiel/Mockup einfach als Text in dieses Dokument eingegeben werden. **Tipp:** Verwenden Sie in Markdown Code-Blöcke mit drei Backticks \`\`\` oder \` für Inline-Code. Dies sorgt für eine dicktengleiche Schrift (alle Zeichen haben identische Maße).]
-  ```
   First A B C 
   Second Step
   And Something More
   ```
- `Let's goooo!`

### Externe Schnittstellen

- [Beschreiben Sie hier kurz die für die gewählte Anforderung bzw. dessen Realisierung relevanten Schnittstellen zu externen Systemen. 1-2 Sätze je Schnittstelle mit Informationen zu den ausgetauschten Informationen, Netzwerkverbindungen, Protokollen, wesentliche Daten, Beschränkung usw. (siehe Netzwerkprotokoll) die EntwicklerInnen erkennbar machen sollen wie mit den Schnittstellen interagiert werden muss. In Blick in das Netzwerkprotokoll soll so abgekürzt oder sogar vermieden werden können während der Entwicklung.]

## Aufgabe 3: Architektur entwerfen, modellieren und validieren

Alle Diagramme in dieses Kapitel als SVG einfügen. 

### Quellen dokumentieren - Aufgabe 3: Architektur entwerfen, modellieren und validieren

- **Kurzbeschreibung der übernommenen Teile**: *Was & Wo im Projekt, In welchem Umfang (Idee, Konzept, Texte, Grafik etc.) mit und ohne Anpassungen, etc.*
- **Quellen der übernommenen Teile**: *Folien, Bücher, Namen der Quell-Studierenden, URLs zu Webseiten, KI Prompts, etc.*

### Klassendiagramm

[Klassendiagramm hier samt, bei Bedarf, Beschreibung beziehungsweise Erläuterung einfügen]

### Sequenzdiagramm 1

[Sequenzdiagramm 1 hier samt, bei Bedarf, Beschreibung beziehungsweise Erläuterung einfügen]

### Sequenzdiagramm 2

[Sequenzdiagramm 2 hier samt, bei Bedarf, Beschreibung beziehungsweise Erläuterung einfügen]
