# HTW Quarto Vorlesungsfolien

Dieses Projekt enthält Quarto-/Reveal.js-Präsentationen im Design der HTW Dresden.

Es gibt zwei Hauptbereiche:

- `HTW_PPT_Vorlage/` enthält die aus der HTW-PowerPoint-Vorlage übertragene Quarto-/HTML-Vorlage.
- `Vorlesung_Datenschutz/` enthält konkrete Vorlesungen aus dem Modul Datenschutz & Informationssicherheit.

Die beiden Markdown-Dateien im Hauptordner haben unterschiedliche Aufgaben:

- `quarto_conv.md` ist die zentrale Regeldatei für PDF-zu-Quarto-Konvertierungen.
- `Agend.md` ist eine Planungsdatei für den Aufbau einer konkreten Präsentation.

## Ordnerstruktur

```text
vorlesungsfolien_html/
|-- README.md
|-- quarto_conv.md
|-- Agend.md
|-- HTW_PPT_Vorlage/
|   |-- README.md
|   |-- _quarto.yml
|   |-- ppt-vorlage.qmd
|   |-- ppt-vorlage.html
|   |-- images/
|   |-- logos/
|   `-- styles/
`-- Vorlesung_Datenschutz/
    |-- README.md
    |-- _quarto.yml
    |-- images/
    |-- logos/
    |-- styles/
    `-- Vorlesung/
        |-- 01_Einfuehrung_in_die_Informationssicherheit/
        |-- 02_Historische_Kryptosysteme-1/
        |-- ...
        |-- 24_SQL_Injection/
        `-- 26_Datenschutz/
```

## Die Markdown-Dateien

`quarto_conv.md` beschreibt, wie Vorlesungs-PDFs in Quarto umgewandelt werden sollen. Dort stehen die Regeln für Folienklassen, Überschriften, Codeblöcke, Bilder, Tabellen, Callout-Boxen, Kapiteltrenner und typische Quarto-Fehler.

Diese Datei ist wichtig, wenn neue Vorlesungen aus PDFs erstellt werden. Ein typischer Prompt dafür ist:

```text
Konvertiere diese PDF zu quarto nach den Regeln in quarto_conv.md
```

`Agend.md` ist dagegen keine allgemeine Konvertierungsregel, sondern eher eine inhaltliche Planungsdatei. Sie beschreibt, welche Folientypen oder Themen in einer bestimmten Präsentation vorkommen sollen.

Kurz gesagt:

- `quarto_conv.md` = Wie wird technisch und gestalterisch in Quarto umgesetzt?
- `Agend.md` = Was soll in eine bestimmte Präsentation hinein?

## Wichtige Dateien und Ordner

`HTW_PPT_Vorlage/README.md` erklärt die HTW-PPT-Vorlage, ihre Dateien und die enthaltenen Beispielfolien.

`Vorlesung_Datenschutz/README.md` erklärt die Datenschutz-Vorlesungen, ihre Ordnerstruktur und wie man Präsentationen startet oder neu rendert.

`_quarto.yml` liegt jeweils in `HTW_PPT_Vorlage/` und `Vorlesung_Datenschutz/`. Diese Datei steuert Reveal.js, Foliengröße, Logo, Footer, CSS und globale Optionen.

`styles/theme.css` enthält das Design: Farben, Typografie, Footer, kleines Logo, Titelfolie, Inhaltsfolien, Tabellen, Codeblöcke, Callout-Boxen und responsive Anpassungen.

`images/` enthält Bilder, die von Präsentationen genutzt werden.

`logos/` enthält die HTW-Logos.

## Arbeiten mit dem Projekt

Neue allgemeine Layouts oder Beispiel-Folien für die HTW-PPT-Vorlage gehören in:

```powershell
HTW_PPT_Vorlage\
```

Neue Datenschutz-Vorlesungen gehören in einen eigenen Unterordner unter:

```powershell
Vorlesung_Datenschutz\Vorlesung\
```

Jede Vorlesung ist eine eigene `.qmd`-Datei mit eigener gerenderter `.html`-Datei.

Beispiel:

```text
Vorlesung_Datenschutz/Vorlesung/24_SQL_Injection/
|-- 24_SQL_Injection.qmd
|-- 24_SQL_Injection.html
|-- 24_SQL_Injection_files/
`-- images/
```

## Präsentationen Rendern

Eine einzelne Präsentation rendert man direkt über ihre `.qmd`:

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.qmd
```

Das erzeugt oder aktualisiert die passende HTML-Datei im selben Ordner.

Die HTW-PPT-Vorlage rendert man so:

```powershell
quarto render HTW_PPT_Vorlage\ppt-vorlage.qmd
```

## Präsentationen Öffnen

Gerenderte Präsentationen können direkt im Browser geöffnet werden, zum Beispiel:

```powershell
Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.html
```

Wenn sich Änderungen an CSS oder Bildern nicht direkt zeigen, hilft meistens ein harter Reload im Browser:

```text
Strg + F5
```

## Automatisch erzeugte Dateien

Quarto erzeugt beim Rendern zusätzliche Dateien und Ordner, zum Beispiel:

- `.quarto/`
- `*_files/`
- `.gitignore`
- `<Name>.html`

Die HTML-Dateien sind die fertigen Präsentationen. Die `*_files/`-Ordner enthalten Hilfsdateien, die zur jeweiligen HTML-Datei gehören.

## Hinweis zu Pfaden

Bildpfade sind immer relativ zur jeweiligen `.qmd`-Datei.

In einer Vorlesung unter `Vorlesung_Datenschutz/Vorlesung/<Name>/` sieht ein lokales Bild so aus:

```qmd
![](images/beispiel.png)
```

Ein gemeinsames Bild aus `Vorlesung_Datenschutz/images/` wird zwei Ebenen nach oben referenziert:

```qmd
![](../../images/datenschutz.jpg)
```
