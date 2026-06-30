# Quarto-Vorlesungsfolien

Dieser Ordner enthaelt ein Reveal.js/Quarto-Grundgeruest fuer Vorlesungsfolien im HTW-Stil.

## Wichtige Dateien

- `slides.qmd`: allgemeines Grundgeruest mit Beispiel-Folientypen
- `slides.html`: gerenderte HTML-Datei zu `slides.qmd`
- `Vorlesung/24_SQL_Injection/24_SQL_Injection.qmd`: konkrete Vorlesungsfolie SQL Injection
- `Vorlesung/24_SQL_Injection/24_SQL_Injection.html`: gerenderte HTML-Datei zur SQL-Injection-Vorlesung
- `Vorlesung/26_Datenschutz/26_Datenschutz.qmd`: konkrete Vorlesungsfolie Datenschutz
- `Vorlesung/26_Datenschutz/26_Datenschutz.html`: gerenderte HTML-Datei zur Datenschutz-Vorlesung
- `styles/theme.css`: zentrale CSS-Datei fuer Layout, Farben, Logo, Footer und Folientypen
- `_quarto.yml`: zentrale Quarto/Reveal-Konfiguration

## HTML-Seiten Starten

Nach dem Rendern kannst du die HTML-Dateien direkt im Browser oeffnen:

- `slides.html`
- `Vorlesung/24_SQL_Injection/24_SQL_Injection.html`
- `Vorlesung/26_Datenschutz/26_Datenschutz.html`

Wenn CSS oder Bilder nicht aktuell wirken, im Browser hart neu laden:

```powershell
Strg + F5
```

## Rendern

Wenn du eine `.qmd`-Datei geaendert hast, muss sie neu gerendert werden.

Grundgeruest rendern:

```powershell
quarto render slides.qmd --no-cache
```

Datenschutz-Vorlesung rendern:

```powershell
quarto render Vorlesung\26_Datenschutz\26_Datenschutz.qmd --no-cache
```

SQL-Injection-Vorlesung rendern:

```powershell
quarto render Vorlesung\24_SQL_Injection\24_SQL_Injection.qmd --no-cache
```

## Ordnerstruktur

```text
2_Grundgeruest/
|-- _quarto.yml
|-- README.md
|-- slides.qmd
|-- slides.html
|-- Vorlesung/
|   |-- 24_SQL_Injection/
|   |   |-- 24_SQL_Injection.qmd
|   |   |-- 24_SQL_Injection.html
|   |   `-- 24_SQL_Injection_files/
|   `-- 26_Datenschutz/
|       |-- 26_Datenschutz.qmd
|       |-- 26_Datenschutz.html
|       `-- 26_Datenschutz_files/
|-- styles/
|   `-- theme.css
|-- images/
|   |-- bild1.jpg
|   |-- datenschutz.jpg
|   |-- title-hero.jpg
|   `-- weitere Bilder
|-- logos/
|   |-- htw-logo-large.jpg
|   `-- htw-logo-small.jpg
|-- slides_files/
|-- partials/
`-- templates/
```

`Vorlesung/` ist der Ordner fuer konkrete Vorlesungsfolien. Jede Vorlesung hat darin ihren eigenen Unterordner.

`templates/` ist nicht fuer fertige Vorlesungen gedacht, sondern nur als Ablage fuer spaetere technische Quarto- oder Pandoc-Templates.

## Bildpfade

Der Bildpfad ist immer relativ zur `.qmd`-Datei.

In `slides.qmd`:

```qmd
![](images/bild1.jpg)
```

In `Vorlesung/26_Datenschutz/26_Datenschutz.qmd`, weil die Datei zwei Ordner tiefer liegt:

```qmd
![](../../images/bild1.jpg)
```

Wenn ein Bild nicht angezeigt wird:

- Liegt die Datei wirklich im Ordner `images/`?
- Stimmt der relative Pfad?
- Wurde die passende `.qmd` neu gerendert?
- Wurde die HTML im Browser hart neu geladen?

## Folienklassen

Folienklassen stehen direkt an der Ueberschrift:

```qmd
## Titel {.content-slide}
```

Mehrere Klassen sind moeglich:

```qmd
## Text links, Bild rechts {.two-column-slide .text-image-slide}
```

### `.title-slide`

Titelfolie mit grossem Logo, diagonaler weisser Flaeche und optionalem Titelbild.

```qmd
## Datenschutz {.title-slide data-state="hide-footer"}
```

`data-state="hide-footer"` blendet kleines Logo, Footer und Foliennummer auf dieser Folie aus.

### `.content-slide`

Normale Inhaltsfolie mit weissem Hintergrund.

```qmd
## Lernziele {.content-slide}
```

### `.agenda-slide`

Agenda-Folie. Wird zusammen mit `.content-slide` benutzt.

```qmd
## Agenda {.content-slide .agenda-slide}
```

Dazugehoerige Klassen:

- `.agenda`: Container der Agenda
- `.agenda-item`: einzelner Agenda-Punkt

### `.low-text-slide`

Folie mit wenig Text und viel Weissraum.

```qmd
## Beispiel mit wenig Text {.content-slide .low-text-slide}
```

### `.two-column-slide`

Zweispaltige Folie.

```qmd
## Zweispaltiger Text {.two-column-slide}

:::: {.columns}
::: {.column width="50%"}
Text links
:::

::: {.column width="50%"}
Text rechts
:::
::::
```

### `.text-image-slide`

Text links, Bild rechts. Immer zusammen mit `.two-column-slide` verwenden.

```qmd
## Text links, Bild rechts {.two-column-slide .text-image-slide}
```

### `.image-text-slide`

Bild links, Text rechts. Immer zusammen mit `.two-column-slide` verwenden.

```qmd
## Bild links, Text rechts {.two-column-slide .image-text-slide}
```

### `.table-slide`

Folie fuer Tabellen.

```qmd
## Tabelle {.table-slide}
```

### `.image-slide`

Folie fuer ein grosses Bild.

```qmd
## Geschichte nach Schutzzielen {.image-slide}

<img src="../images/Geschichte_nach_Schutzzielen.jpg">
```

Bei Bildfolien ist HTML mit `<img src="...">` oft robuster als Markdown-Bilder.

### `.pdf-slide`

Inhaltsfolie fuer aus PDF uebernommene Vorlesungsfolien. Diese Folien duerfen mehr Text enthalten und koennen bei Bedarf scrollen.

```qmd
## Lernziele {.content-slide .pdf-slide}
```

### `.code-slide`

Folie fuer Codebeispiele. Codebloecke bleiben scrollbar und bekommen eine kleinere Schrift.

````qmd
## Beispiel {.content-slide .code-slide}

```js
const query = `SELECT * FROM users WHERE username = "${username}"`
```
````

### `.pdf-summary`

Zusammenfassungsvariante fuer PDF-Folien.

```qmd
## Zusammenfassung {.content-slide .pdf-slide .pdf-summary}
```

### `.summary`

Box fuer hervorgehobene Zusammenfassungen.

```qmd
::: {.summary}
- Wichtigster Punkt
- Zweiter Punkt
:::
```

## Typische Arbeitsweise

1. Inhalt in der passenden `.qmd` aendern.
2. Bilder in `images/` ablegen.
3. Bildpfade relativ zur `.qmd` schreiben.
4. Passende `.qmd` rendern.
5. HTML im Browser neu laden.
