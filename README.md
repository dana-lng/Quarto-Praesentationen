# HTW Quarto Vorlesungsfolien

Dieses Projekt enthält ein Quarto/Reveal.js-System für Vorlesungsfolien im Design der HTW Dresden.

Die Struktur ist bewusst getrennt:

- `Template/` enthält das allgemeine Design und ein Grundgerüst.
- `Vorlesung_Datenschutz/` enthält konkrete Vorlesungen aus dem Modul Datenschutz & Informationssicherheit.
- `quarto_conv.md` enthält die zentralen Regeln für neue PDF-zu-Quarto-Konvertierungen.

## Ordnerstruktur

```text
vorlesungsfolien_html/
|-- README.md
|-- quarto_conv.md
|-- Agend.md
|-- Template/
|   |-- _quarto.yml
|   |-- slides.qmd
|   |-- slides.html
|   |-- images/
|   |-- logos/
|   |-- partials/
|   |-- styles/
|   `-- templates/
`-- Vorlesung_Datenschutz/
    |-- _quarto.yml
    |-- slides.qmd
    |-- images/
    |-- logos/
    |-- partials/
    |-- styles/
    `-- Vorlesung/
        |-- 18_Angriffstechniken/
        |-- 19_Heartbleed/
        |-- 20_Hackertools/
        |-- 21_Cookie_und_Session_Security/
        |-- 22_Cross-Site-Scripting/
        |-- 23_Command_Injection/
        |-- 24_SQL_Injection/
        `-- 26_Datenschutz/
```

## Wichtige Dateien

`quarto_conv.md` ist die verbindliche Anleitung für neue Vorlesungskonvertierungen. Dort stehen die erlaubten Folienklassen, Titel-/Abschlussfolien, Codeblock-Regeln, Bildpfade und typische Quarto-Fallen.

`Template/README.md` erklärt das allgemeine HTW-Design und das Grundgerüst.

`Vorlesung_Datenschutz/README.md` erklärt die fertigen Datenschutz-Vorlesungen, ihre Ordnerstruktur und wie man sie startet oder neu rendert.

`_quarto.yml` liegt jeweils in `Template/` und `Vorlesung_Datenschutz/`. Diese Datei steuert Reveal.js, Foliengröße, Logo, Footer, CSS und globale Optionen.

`styles/theme.css` enthält das Design: Farben, Typografie, Footer, Logo, Titelfolie und Folienlayouts.

## Arbeiten mit dem Projekt

Neue allgemeine Layouts oder Beispiel-Folien gehören in `Template/`.

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

## Quarto Rendern

Eine einzelne Präsentation rendert man direkt über ihre `.qmd`:

```powershell
quarto render Vorlesung_Datenschutz\Vorlesung\24_SQL_Injection\24_SQL_Injection.qmd
```

Das erzeugt oder aktualisiert die passende HTML-Datei im selben Ordner.

Das Template-Grundgerüst rendert man so:

```powershell
quarto render Template\slides.qmd
```

## Automatisch erzeugte Dateien

Quarto erzeugt beim Rendern zusätzliche Dateien und Ordner, zum Beispiel:

- `.quarto/`
- `*_files/`
- `.gitignore`
- `slides.html` oder `<Vorlesung>.html`

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
