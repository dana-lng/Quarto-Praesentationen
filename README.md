# Quarto-Vorlesungsfolien

Dieser Ordner enthaelt ein Reveal.js/Quarto-Grundgeruest fuer Vorlesungsfolien im HTW-Stil.

Es gibt zwei wichtige Praesentationen:

- `slides.qmd`: allgemeines Grundgeruest mit Beispiel-Folientypen
- `templates/26_Datenschutz.qmd`: Datenschutz-Vorlesung auf Basis des Grundgeruests

Die Gestaltung liegt in `styles/theme.css`.

## HTML-Seiten Starten

### Variante 1: HTML direkt oeffnen

Nach dem Rendern kann die HTML-Datei direkt im Browser geoeffnet werden:

- `slides.html`
- `templates/26_Datenschutz.html`

Wenn Bilder oder CSS nicht aktuell wirken, den Browser hart neu laden:

```powershell
Strg + F5
```

### Variante 2: Mit Quarto rendern

Wenn du eine `.qmd`-Datei geaendert hast, muss sie neu gerendert werden.

Fuer das Grundgeruest:

```powershell
quarto render slides.qmd --no-cache
```

Fuer die Datenschutz-Folien:

```powershell
quarto render templates\26_Datenschutz.qmd --no-cache
```

Danach die passende HTML-Datei im Browser neu laden.

### Variante 3: Mit Quarto Preview

In VS Code kann man auch die Quarto Preview benutzen. Alternativ im Terminal:

```powershell
quarto preview slides.qmd
```

oder:

```powershell
quarto preview templates\26_Datenschutz.qmd
```

## Wichtig: Pfade Zu Bildern

Der Bildpfad ist immer relativ zur `.qmd`-Datei.

In `slides.qmd`:

```qmd
![](images/bild1.jpg)
```

In `templates/26_Datenschutz.qmd`, weil die Datei einen Ordner tiefer liegt:

```qmd
![](../images/bild1.jpg)
```

Wenn ein Bild nicht angezeigt wird, zuerst diese drei Dinge pruefen:

- Liegt die Bilddatei wirklich im Ordner `images/`?
- Stimmt der relative Pfad?
- Wurde die passende `.qmd` neu gerendert?

## Ordnerstruktur

```text
2_Grundgeruest/
├─ _quarto.yml
├─ slides.qmd
├─ slides.html
├─ styles/
│  └─ theme.css
├─ images/
│  ├─ bild1.jpg
│  ├─ datenschutz.jpg
│  ├─ Geschichte_nach_Schutzzielen.jpg
│  └─ title-hero.jpg
├─ logos/
│  ├─ htw-logo-large.jpg
│  └─ htw-logo-small.jpg
├─ templates/
│  ├─ 26_Datenschutz.qmd
│  ├─ 26_Datenschutz.html
│  └─ 26_Datenschutz_files/
├─ slides_files/
├─ partials/
└─ README.md
```

### `_quarto.yml`

Zentrale Quarto-Konfiguration:

- Reveal.js als Ausgabeformat
- Foliengroesse
- Footer
- kleines Logo
- verwendete CSS-Datei

### `slides.qmd`

Beispiel-Praesentation mit den wichtigsten Folientypen.

### `templates/26_Datenschutz.qmd`

Eigene Vorlesungsdatei fuer Datenschutz. Diese Datei benutzt dasselbe Design wie `slides.qmd`.

### `styles/theme.css`

Zentrale CSS-Datei fuer Layout, Farben, Logo, Footer und Folienklassen.

### `images/`

Bilder fuer Folien. Bilder werden normalerweise direkt in der `.qmd` eingebunden.

### `logos/`

HTW-Logos fuer Titelfolie und Inhaltsfolien.

### `*_files/`

Von Quarto erzeugte Hilfsordner. Diese entstehen automatisch beim Rendern.

## Folienklassen

Folienklassen stehen direkt an der Ueberschrift:

```qmd
## Titel {.content-slide}
```

Mehrere Klassen sind moeglich:

```qmd
## Text links, Bild rechts {.two-column-slide .text-image-slide}
```

## Verwendete Folientypen

### `.title-slide`

Titelfolie mit grossem Logo, diagonaler weisser Flaeche und optionalem Titelbild.

Beispiel:

```qmd
## Datenschutz {.title-slide data-state="hide-footer"}
```

Mit `data-state="hide-footer"` werden kleines Logo, Footer und Foliennummer auf dieser Folie ausgeblendet.

In `slides.qmd` wird das Titelbild als CSS-Hintergrund gesetzt:

```qmd
## Titel {.title-slide data-state="hide-footer" style="--title-image: url('images/title-hero.jpg'); --title-image-size: cover; --title-image-position: right center;"}
```

In `templates/26_Datenschutz.qmd` wird das Titelbild als echtes Bild gesetzt:

```html
<img class="title-image" src="../images/datenschutz.jpg" alt="" style="--title-image-width: 120vw; --title-image-right: -500px; --title-image-top: 0px; --title-image-height: 100vh; --title-image-object-position: right right;">
```

Wichtige Variablen fuer das echte Titelbild:

- `--title-image-width`: Bildbreite
- `--title-image-height`: Bildhoehe
- `--title-image-right`: Bild nach rechts/links schieben
- `--title-image-top`: Bild nach oben/unten schieben
- `--title-image-object-position`: Bildausschnitt innerhalb der Bildbox

### `.content-slide`

Normale Inhaltsfolie mit weissem Hintergrund.

Beispiel:

```qmd
## Lernziele {.content-slide}
```

Diese Klasse ist die Basis fuer einfache Textfolien.

### `.agenda-slide`

Agenda-Folie. Wird zusammen mit `.content-slide` verwendet.

Beispiel:

```qmd
## Agenda {.content-slide .agenda-slide}

<ul class="agenda">
<li class="agenda-item"><strong>01</strong><span>Einleitung</span></li>
<li class="agenda-item"><strong>02</strong><span>Grundlagen</span></li>
</ul>
```

Dazugehoerige Klassen:

- `.agenda`: Container der Agenda
- `.agenda-item`: einzelner Agenda-Punkt

### `.low-text-slide`

Folie mit wenig Text, viel Weissraum und grosser ruhiger Typografie.

Beispiel:

```qmd
## Beispiel mit wenig Text {.content-slide .low-text-slide}

Kurzer Text ...
```

### `.two-column-slide`

Zweispaltige Folie.

Beispiel:

```qmd
## Zweispaltiger Text {.two-column-slide}

:::: {.columns}
::: {.column width="50%"}
### Links

- Punkt 1
- Punkt 2
:::

::: {.column width="50%"}
### Rechts

- Punkt 1
- Punkt 2
:::
::::
```

Die Klassen `.columns` und `.column` kommen von Quarto.

### `.text-image-slide`

Zweispaltige Folie mit Text links und Bild rechts.

Immer zusammen mit `.two-column-slide` benutzen:

```qmd
## Text links, Bild rechts {.two-column-slide .text-image-slide}
```

Beispiel:

```qmd
:::: {.columns}
::: {.column width="60%"}
- Textpunkt
- Noch ein Punkt
:::

::: {.column width="40%"}
<img src="../images/bild1.jpg" alt="Beschreibung">
:::
::::
```

### `.image-text-slide`

Zweispaltige Folie mit Bild links und Text rechts.

Immer zusammen mit `.two-column-slide` benutzen:

```qmd
## Bild links, Text rechts {.two-column-slide .image-text-slide}
```

### `.table-slide`

Folie fuer Tabellen.

Beispiel:

```qmd
## Tabelle {.table-slide}

| Kategorie | Beschreibung |
|---|---|
| A | Beispiel |
```

Tabellen bekommen automatisch passende Zellabstaende und einen farbigen Kopf.

### `.image-slide`

Folie fuer ein grosses Bild.

Beispiel:

```qmd
## Geschichte nach Schutzzielen {.image-slide}

<img src="../images/Geschichte_nach_Schutzzielen.jpg" alt="Geschichte nach Schutzzielen">
```

Fuer Bildfolien ist `<img src="...">` oft robuster als Markdown-Bilder, weil Quarto Markdown-Bilder manchmal automatisch mit Reveal-Stretch-Klassen versieht.

### `.pdf-slide`

Inhaltsfolie fuer aus PDF uebernommene Folien. Diese Folien enthalten oft mehr Text als normale Folien.

Beispiel:

```qmd
## Lernziele {.content-slide .pdf-slide}
```

Die CSS macht Text etwas kompakter und erlaubt Scrollen, falls eine Folie zu voll wird.

### `.pdf-summary`

Variante fuer die Zusammenfassungsfolie der PDF-Folien.

Beispiel:

```qmd
## Zusammenfassung {.content-slide .pdf-slide .pdf-summary}
```

### `.summary`

Box fuer Zusammenfassungen oder hervorgehobene Textbereiche.

Beispiel:

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
4. Datei rendern:

```powershell
quarto render templates\26_Datenschutz.qmd --no-cache
```

5. HTML im Browser neu laden.

Wenn nur `styles/theme.css` geaendert wurde, reicht oft ein harter Browser-Reload. Wenn sich aber `.qmd` oder `_quarto.yml` geaendert haben, muss neu gerendert werden.
