# Vorlesung Datenschutz & Informationssicherheit

Hier liegen die Vorlesungen aus dem Modul Datenschutz & Informationssicherheit von Prof. Dr. Lukas Iffländer als Quarto-/Reveal.js-Präsentationen.

Jede Vorlesung ist eine eigene Präsentation. Die `.qmd`-Datei ist die bearbeitbare Quelle, die `.html`-Datei ist die gerenderte Präsentation für den Browser.

## Ordnerstruktur

```text
Vorlesung_Datenschutz/
|-- README.md
|-- _quarto.yml
|-- images/
|-- logos/
|-- styles/
`-- Vorlesung/
    |-- 01_Einfuehrung_in_die_Informationssicherheit/
    |-- 02_Historische_Kryptosysteme-1/
    |-- 03_Kryptographische_Grundlagen-4/
    |-- 04_Kryptographische_Protokolle/
    |-- 05_Zufallszahlen-2/
    |-- 06_Einwegfunktionen-2/
    |-- 07_Signaturen/
    |-- 08_Authentifizierung-1/
    |-- 09_Schluesselaustausch-1/
    |-- 10_DES/
    |-- 11_Betriebsmodi/
    |-- 12_Galois-Koerper-1/
    |-- 13_AES-1/
    |-- 14_Zahlentheorie/
    |-- 15_Diffie-Hellman-2/
    |-- 16_RSA-1/
    |-- 17_Schluesselverwaltung/
    |-- 18_Angriffstechniken/
    |-- 19_Heartbleed/
    |-- 20_Hackertools/
    |-- 21_Cookie_und_Session_Security/
    |-- 22_Cross-Site-Scripting/
    |-- 23_Command_Injection/
    |-- 24_SQL_Injection/
    `-- 26_Datenschutz/
```

## Dateien und Ordner

`_quarto.yml` ist die zentrale Konfiguration für alle Präsentationen in diesem Ordner. Quarto findet diese Datei automatisch, wenn eine Vorlesung darunter gerendert wird. Darin stehen unter anderem Reveal.js, Foliengröße, Logo, Footer und CSS.

`styles/theme.css` enthält das gemeinsame Design: Farben, Schriftgrößen, Titelfolie, Footer, kleines Logo, Agenda, Tabellen, Codeblöcke, Bildfolien, Callout-Boxen und responsive Anpassungen.

`images/` enthält gemeinsame Bilder, die von mehreren Vorlesungen genutzt werden können, zum Beispiel Titelbilder oder allgemeine Grafiken.

`logos/` enthält die HTW-Logos. Das kleine Logo im Footer/Inhaltsfolien wird über `_quarto.yml` eingebunden.

`Vorlesung/` enthält die fertigen Vorlesungen. Jede Vorlesung hat einen eigenen Unterordner.

Ein typischer Vorlesungsordner sieht so aus:

```text
Vorlesung/24_SQL_Injection/
|-- 24_SQL_Injection.qmd
|-- 24_SQL_Injection.html
|-- 24_SQL_Injection_files/
`-- images/
```

`<Vorlesung>.qmd` ist die Datei, die bearbeitet wird.

`<Vorlesung>.html` ist die fertige Präsentation für den Browser.

`<Vorlesung>_files/` wird von Quarto erzeugt und enthält Hilfsdateien für die HTML-Präsentation.

`images/` im jeweiligen Vorlesungsordner enthält Bilder, die nur zu dieser einen Vorlesung gehören.

## Präsentationen Öffnen

Eine bereits gerenderte Präsentation kann direkt im Browser geöffnet werden, zum Beispiel:

```powershell
Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.html
```

Wenn Bilder oder CSS nicht aktuell wirken, im Browser hart neu laden:

```text
Strg + F5
```

## Präsentationen Rendern

Wenn eine `.qmd`-Datei geändert wurde, muss sie neu gerendert werden.

Beispiele:

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\01_Einfuehrung_in_die_Informationssicherheit\01_Einfuehrung_in_die_Informationssicherheit.qmd
```

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.qmd
```

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\26_Datenschutz\26_Datenschutz.qmd
```

Danach die jeweilige `.html` im Browser neu laden.

## Live-Vorschau

Für die Bearbeitung kann Quarto Preview genutzt werden:

```powershell
quarto preview Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.qmd
```

Quarto startet dann einen lokalen Server und öffnet die Präsentation im Browser.

## Bildpfade

Bildpfade sind immer relativ zur jeweiligen `.qmd`-Datei.

Ein Bild aus dem lokalen Vorlesungsordner:

```qmd
![](images/beispiel.png)
```

Ein gemeinsames Bild aus `Vorlesung_Datenschutz/images/`:

```qmd
![](../../images/datenschutz.jpg)
```

Wenn ein Bild nicht angezeigt wird:

- Liegt die Bilddatei wirklich im angegebenen Ordner?
- Stimmt der relative Pfad?
- Wurde die `.qmd` neu gerendert?
- Wurde die HTML-Datei im Browser neu geladen?

## Folienklassen

Die Präsentationen nutzen die Folienklassen aus `styles/theme.css`.

Beispiel:

```qmd
## Agenda {.content-slide .agenda-slide}
```

Wichtige Klassen:

- `.title-slide`: Titelfolie und Abschlussfolie.
- `.content-slide`: normale Inhaltsfolie.
- `.agenda-slide`: Agenda-Folie mit nummerierten Punkten.
- `.pdf-slide`: textreichere Folien aus PDF-Konvertierungen.
- `.code-slide`: Folien mit Codeblöcken.
- `.two-column-slide`: zweispaltige Folien.
- `.text-image-slide`: Text links und Bild rechts.
- `.image-text-slide`: Bild links und Text rechts.
- `.image-slide`: große Bild- oder Diagrammfolie.
- `.table-slide`: Tabellenfolie.
- `.low-text-slide`: Folie mit wenig Text.
- `.section-divider-slide`: Kapiteltrenner mit farbiger Fläche und Bild.

## Neue Vorlesung Anlegen

Neue Vorlesungen lassen sich am einfachsten mit einer KI erstellen:

1. Der KI die Vorlesungs-PDF geben.
2. Dazu einen klaren Prompt schreiben, zum Beispiel:

```text
Konvertiere diese PDF zu quarto nach den Regeln in quarto_conv.md
```

Die Datei `../quarto_conv.md` ist dabei wichtig, weil dort das gewünschte Quarto-Format, die Folienklassen, Bildregeln, Codeblöcke, Callout-Boxen, Tabellen und typische Fehler beschrieben sind.

Wenn die Vorlesung manuell angelegt wird:

1. Unter `Vorlesung/` einen neuen Ordner anlegen.
2. Darin eine gleichnamige `.qmd` erstellen.
3. Frontmatter und Folienstruktur aus einer bestehenden Vorlesung übernehmen.
4. Bilder entweder im lokalen `images/`-Ordner der Vorlesung oder im gemeinsamen `images/`-Ordner ablegen.
5. Präsentation rendern:

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\<Ordner>\<Datei>.qmd
```

Für neue PDF-Konvertierungen gelten zusätzlich die Regeln aus `../quarto_conv.md`.

## Automatisch erzeugte Dateien

Quarto erzeugt beim Rendern zusätzliche Dateien und Ordner, zum Beispiel:

- `.quarto/`
- `<Vorlesung>_files/`
- `<Vorlesung>.html`

Diese Dateien gehören zur gerenderten Präsentation. Bearbeitet wird normalerweise nur die `.qmd`-Datei und bei Designänderungen `styles/theme.css`.
