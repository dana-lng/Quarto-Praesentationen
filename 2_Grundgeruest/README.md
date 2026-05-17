# Quarto-Vorlagenordner

Dieser Ordner ist ein Grundgeruest fuer wartbare Reveal.js-Vorlesungsfolien im HTW-Stil.

## Dateien

- `slides.qmd`: Inhalt der Praesentation, moeglichst in Markdown.
- `_quarto.yml`: zentrale Reveal.js-Konfiguration, Logo, Footer und Theme.
- `styles/theme.scss`: zentrales Theme fuer Farben, Typografie, Footer, Tabellen und Folientypen.
- `images/`: Bilder fuer Folien.
- `logos/`: Logos fuer Titel- und Inhaltsfolien.
- `partials/` und `templates/`: Platz fuer spaetere wiederverwendbare Fragmente oder Templates.

## Neue Folientypen

Folientypen werden ueber Klassen am Heading gesetzt:

```markdown
## Titel {.title-slide}

## Kapitel {.chapter-slide}

## Inhalt {.content-slide}

## Zwei Spalten {.two-column-slide}

## Tabelle {.table-slide}

## Bild {.image-slide}
```

Footer, kleines Logo, Datum und Slide-Nummern kommen automatisch aus `_quarto.yml` und `styles/theme.scss`.
