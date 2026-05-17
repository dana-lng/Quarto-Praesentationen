# AGENTS.md

## Projektziel

Dieses Projekt erstellt HTML-Vorlesungsfolien mit Quarto + Reveal.js im Corporate Design der HTW Dresden.

Die Präsentationen sollen:

* langfristig wartbar sein
* leicht erweiterbar sein
* für 50+ Vorlesungen skalieren
* von anderen Personen (z. B. Professoren) bearbeitet werden können
* möglichst wenig manuelles HTML/CSS pro Folie benötigen

Die Folien werden in Quarto (`.qmd`) geschrieben und als Reveal.js HTML-Präsentationen gerendert.

---

# Technologien

* Quarto
* Reveal.js
* HTML
* CSS / SCSS
* Markdown
* optional Python/Jupyter

---

# Wichtige Architekturprinzipien

## 1. Inhalt und Layout trennen

Die `.qmd` Dateien sollen primär Inhalt enthalten.

Komplexes Layout soll:

* global im Theme
* oder über wiederverwendbare Klassen
  gelöst werden.

Vermeide:

* individuelle absolute Positionierung pro Folie
* pixelgenaue Hacks pro Slide
* duplizierten HTML-Code

---

## 2. Wiederverwendbare Folientypen

Das Projekt soll mit standardisierten Folientypen arbeiten.

Beispiele:

* `title-slide`
* `chapter-slide`
* `content-slide`
* `table-slide`
* `image-slide`
* `two-column-slide`

Diese Typen sollen zentral definiert werden.

---

## 3. Globale Komponenten

Folgende Elemente sollen global automatisiert werden:

* Logo
* Footer
* Datum
* Schriftarten
* Tabellenstil
* Farben
* Header
* Slide-Nummern

Diese Elemente sollen NICHT manuell auf jeder Folie eingefügt werden.

---

## 4. CSS-Prinzipien

Bevorzugt:

* Flexbox
* CSS Grid
* margin/padding
* responsive Layouts

Vermeiden:

* exzessive absolute Positionierung
* große negative left/top Werte
* manuelle Pixelverschiebungen
* Layout-Hacks

Absolute Positionierung nur für:

* Logos
* Hero Images
* spezielle Titel-Layouts

---

## 5. Markdown bevorzugen

Normale Inhaltsfolien sollen möglichst reines Markdown verwenden.

Beispiel:

```markdown
## Motivation

- Punkt 1
- Punkt 2
```

HTML nur verwenden für:

* Speziallayouts
* komplexe Titel
* strukturierte Komponenten

---

# Projektstruktur

```text
projekt/

├── slides.qmd
├── _quarto.yml
├── styles/
│   └── theme.scss
├── images/
├── logos/
├── partials/
└── templates/
```

---

# Theme-System

Das Projekt soll ein zentrales HTW-Theme verwenden.

Das Theme definiert:

* Farben
* Typografie
* Tabellenstil
* Logos
* Footer
* Kapitel-Layouts
* Standardabstände

Neue Vorlesungen sollen möglichst ohne zusätzliches CSS erstellt werden können.

---

# Tabellen

Tabellen sollen:

* global gestylt werden
* konsistente Farben besitzen
* responsive sein
* nicht pro Folie individuell angepasst werden

---

# Footer

Der Footer soll automatisiert werden und enthalten:

* Datum
* Veranstaltung
* Studiengang
* Professor
* kleines HTW-Logo

Footer nicht manuell pro Folie einfügen.

---

# Logos

Logos sollen:

* global eingebunden werden
* positionsabhängig über CSS geregelt werden
* je nach Folientyp unterschiedlich dargestellt werden können

Beispiele:

* große Logos auf Titelfolien
* kleine Logos auf Inhaltsfolien

---

# Reveal.js Anforderungen

Die Präsentation soll:

* responsive sein
* auf verschiedenen Bildschirmgrößen funktionieren
* mit Reveal.js kompatibel bleiben
* keine Reveal.js internen Layouts zerstören

Vermeide globale Überschreibungen wie:

```css
.reveal .slides section {
    position: absolute;
}
```

---

# Zielworkflow

Der langfristige Workflow soll sein:

1. Neue Vorlesung anlegen
2. Inhalte in Markdown schreiben
3. Automatisches Theme übernimmt Layout
4. Möglichst kein individuelles CSS pro Folie notwendig

---

# Ziel

Das Projekt soll eher ein professionelles Präsentationssystem sein als eine Sammlung individuell gebauter Folien.
