# Template

Hier liegt das allgemeine Design der HTW Dresden in HTML/Quarto.

Dieser Ordner ist als Grundgerüst gedacht. Er enthält Beispiel-Folien, das zentrale Theme, Logos, Bilder und technische Vorlagen. Fertige Vorlesungen sollen nicht hier abgelegt werden, sondern in einem eigenen Vorlesungsordner.

## Zweck

`Template/` dient als Vorlage für neue Präsentationen:

- einheitliches HTW-Dresden-Design
- Reveal.js-Konfiguration über Quarto
- Beispiel für Titel-, Agenda-, Text-, Bild-, Tabellen-, Code- und Abschlussfolien
- zentrale CSS-Datei für Layout und Responsivität
- gemeinsame Logos und Beispielbilder

## Ordnerstruktur

```text
Template/
|-- README.md
|-- _quarto.yml
|-- slides.qmd
|-- slides.html
|-- images/
|-- logos/
|-- partials/
|-- styles/
`-- templates/
```

## Dateien und Ordner

`_quarto.yml` enthält die globale Quarto-Konfiguration für dieses Template. Dort werden Reveal.js, Foliengröße, Theme-CSS, Logo, Footer und weitere Ausgabeoptionen gesetzt.

`slides.qmd` ist die Beispiel-Präsentation. Dort sieht man, wie die verschiedenen Folienklassen verwendet werden.

`slides.html` ist die gerenderte HTML-Ausgabe von `slides.qmd`. Diese Datei kann direkt im Browser geöffnet werden.

`styles/theme.css` ist die zentrale CSS-Datei. Hier stehen Farben, Schriftgrößen, Footer, Logo, Titelfolie, Agenda, Bildfolien, Tabellen, Codefolien und responsive Anpassungen.

`images/` enthält allgemeine Beispielbilder und gemeinsame Bilder für das Design, zum Beispiel das Titelbild.

`logos/` enthält die HTW-Logos für Titelfolie, Inhaltsfolien und Footer.

`partials/` enthält zusätzliche Quarto-/HTML-Bausteine, falls sie vom Projekt gebraucht werden.

`templates/` ist für technische Quarto- oder Pandoc-Vorlagen gedacht, nicht für fertige Vorlesungsfolien.

## Template Starten

Die fertige HTML-Datei kann direkt im Browser geöffnet werden:

```powershell
Template\slides.html
```

Wenn `slides.qmd` geändert wurde, muss die HTML-Datei neu gerendert werden:

```powershell
quarto render Template\slides.qmd
```

Für eine Live-Vorschau kann Quarto Preview genutzt werden:

```powershell
quarto preview Template\slides.qmd
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

In `Template/slides.qmd` kann ein Bild aus `Template/images/` so eingebunden werden:

```qmd
![](images/bild1.jpg)
```

Das Titelbild wird bei `title-slide` üblicherweise als echtes Bild eingebunden:

```html
<img class="title-image" src="images/datenschutz.jpg" alt="">
```

Die genaue Position und Größe der Titelfolie kann über die dafür vorgesehenen CSS-Variablen am Bild angepasst werden.

## Typische Arbeitsweise

1. `slides.qmd` als Beispiel ansehen.
2. Für neue Vorlesungen die Struktur und Klassen übernehmen.
3. Eigene Inhalte in einem separaten Vorlesungsordner anlegen.
4. Präsentation mit `quarto render` neu erzeugen.
5. HTML-Datei im Browser öffnen oder mit `quarto preview` ansehen.
