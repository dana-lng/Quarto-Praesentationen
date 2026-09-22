# HTW PPT Vorlage

Hier liegt die HTW-Dresden-PowerPoint-Vorlage als HTML/Quarto-Präsentation.

Dieser Ordner ist nur für die aus `Präsentationsvorlage.ppt` übertragene HTW-PPT-Vorlage gedacht. Fertige Vorlesungen sollen nicht hier abgelegt werden, sondern in einem eigenen Vorlesungsordner.

## Zweck

`HTW_PPT_Vorlage/` dient als Referenz für das HTW-PPT-Design:

- einheitliches HTW-Dresden-Design
- Reveal.js-Konfiguration über Quarto
- Beispiel für Titel-, Text-, Bild-, Tabellen-, Diagramm- und Abschlussfolien
- zentrale CSS-Datei für Layout und Responsivität
- gemeinsame Logos und Beispielbilder

## Ordnerstruktur

```text
HTW_PPT_Vorlage/
|-- README.md
|-- _quarto.yml
|-- ppt-vorlage.qmd
|-- ppt-vorlage.html
|-- images/
|-- logos/
`-- styles/
```

## Dateien und Ordner

`_quarto.yml` enthält die globale Quarto-Konfiguration für diese Vorlage. Dort werden Reveal.js, Foliengröße, Theme-CSS, Logo, Footer und weitere Ausgabeoptionen gesetzt.

`ppt-vorlage.qmd` ist die aus der PowerPoint-Datei `Präsentationsvorlage.ppt`
nach Quarto übertragene HTW-Dresden-Präsentationsvorlage. Sie enthält die
Layout-Beispiele aus der PPT-Vorlage als bearbeitbare Quarto-Folien.

`ppt-vorlage.html` ist die gerenderte HTML-Ausgabe von `ppt-vorlage.qmd`.

`styles/theme.css` ist die zentrale CSS-Datei. Hier stehen Farben, Schriftgrößen, Footer, Logo, Titelfolie, Agenda, Bildfolien, Tabellen, Codefolien und responsive Anpassungen.

`images/` enthält die aus der PowerPoint-Vorlage übernommenen Bilder und Screenshots, die von `ppt-vorlage.qmd` verwendet werden.

`logos/` enthält die HTW-Logos für Titelfolie, Inhaltsfolien und Footer.

## Vorlage Starten

Die fertige HTML-Datei kann direkt im Browser geöffnet werden:

```powershell
HTW_PPT_Vorlage\ppt-vorlage.html
```

Die aus PowerPoint übertragene Vorlage wird so gerendert:

```powershell
quarto render HTW_PPT_Vorlage\ppt-vorlage.qmd
```

Für eine Live-Vorschau kann Quarto Preview genutzt werden:

```powershell
quarto preview HTW_PPT_Vorlage\ppt-vorlage.qmd
```

## Wichtige Folienklassen

Folienklassen stehen direkt an der Überschrift:

```qmd
## Titel {.content-slide}
```

Mehrere Klassen können kombiniert werden:

```qmd
## Beispiel {.content-slide .code-slide}
```

Die wichtigsten Klassen:

- `.title-slide`: Titelfolie und Abschlussfolie mit großem Titelbild.
- `.content-slide`: normale Inhaltsfolie.
- `.agenda-slide`: Agenda mit nummerierten Agenda-Punkten.
- `.pdf-slide`: textreichere Folie, häufig für aus PDFs übernommene Inhalte.
- `.code-slide`: Folie mit Codeblöcken.
- `.two-column-slide`: zweispaltige Folie.
- `.text-image-slide`: Text links, Bild rechts.
- `.image-text-slide`: Bild links, Text rechts.
- `.image-slide`: große Bild- oder Diagrammfolie.
- `.table-slide`: Folie mit Tabelle.
- `.low-text-slide`: Folie mit wenig Text und viel Weißraum.

## Bildpfade

Bildpfade sind relativ zur `.qmd`-Datei.

In `HTW_PPT_Vorlage/ppt-vorlage.qmd` kann ein Bild aus `HTW_PPT_Vorlage/images/` so eingebunden werden:

```qmd
![](images/image1.png)
```

Das Titelbild wird bei `title-slide` üblicherweise als echtes Bild eingebunden:

```html
<img class="title-image" src="images/image1.png" alt="">
```

Die genaue Position und Größe der Titelfolie kann über die dafür vorgesehenen CSS-Variablen am Bild angepasst werden.

## Typische Arbeitsweise

1. `ppt-vorlage.qmd` als Beispiel ansehen.
2. Für neue Vorlesungen die Struktur und Klassen übernehmen.
3. Eigene Inhalte in einem separaten Vorlesungsordner anlegen.
4. Präsentation mit `quarto render` neu erzeugen.
5. HTML-Datei im Browser öffnen oder mit `quarto preview` ansehen.
