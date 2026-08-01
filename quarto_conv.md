# QUARTO_CONVENTIONS.md

Diese Datei ist die **verbindliche Referenz** für die Umwandlung von PDF-Vorlesungen
(LaTeX-Beamer-Export) in Quarto/Reveal.js-Folien im HTW-Dresden-Theme.

Sie ergänzt `AGENTS.md`: `AGENTS.md` beschreibt die Architektur, **diese Datei
beschreibt die konkrete Folien-Syntax, die Slide-Klassen und die bekannten Fallen.**
Beim Konvertieren wird diese Datei immer befolgt.

> Grundregel: **Inhalt in Markdown, Layout über die Slide-Klassen des Themes.**
> Kein individuelles CSS pro Folie, keine absolute Positionierung, keine Pixel-Hacks.

---

## 1. Dokument-Grundgerüst

Jede `.qmd` beginnt mit diesem Frontmatter. Nur die Werte anpassen, die Struktur
bleibt gleich:

```yaml
---
pagetitle: "<Titel der Vorlesung>"
date: today
date-format: "DD.MM.YYYY"
veranstaltung: "<Titel der Vorlesung>"
studiengang: "HTW Dresden"
professor: "Prof. Dr. <Name>"
---
```

Wichtig:

- Logo, Footer, Datum, Foliennummer werden **global** aus `_quarto.yml` und dem
  Theme erzeugt. **Niemals** manuell auf einer Folie einfügen.
- Der Footer zieht sich `veranstaltung`, `studiengang`, `professor`, `date`
  automatisch aus dem Frontmatter über `{{< meta ... >}}`.

Folien werden mit `---` (eigene Zeile, Leerzeile davor und danach) getrennt.
**Keine Leer- oder Sonderzeichen hinter dem `---`** — sonst versucht Quarto, den
folgenden Inhalt als YAML zu parsen (führt zu „Error parsing YAML metadata").

---

## 2. Slide-Klassen (verbindlich)

Klassen werden an die Folienüberschrift gehängt: `## Titel {.klasse}`.
Mehrere Klassen sind kombinierbar: `## Titel {.image-slide .code-slide}`.

| Klasse | Wofür | Besonderheit |
|---|---|---|
| `title-slide` | Titelfolie / Schlussfolie | Braucht `data-state="hide-footer"` + `.title-image`. Hintergrundbild + HTW-Logo automatisch. |
| `content-slide` | Standard-Inhaltsfolie (Bullets, kurzer Text) | Weißer Hintergrund. Meistgenutzt. |
| `pdf-slide` | Textreiche Folie mit vielen Bullets / langen Absätzen | Scrollbar bei Überlauf. Für Fließtext-lastige Beamer-Folien. |
| `code-slide` | Folie mit einem oder mehreren Codeblöcken | Code wird passend skaliert, `pre` scrollt bei Bedarf. |
| `two-column-slide` | Zwei Spalten (Text/Text) | Mit `:::: {.columns}` / `::: {.column width="…"}`. |
| `text-image-slide` | Text links, Bild rechts | Grid, Bild rechts. |
| `image-text-slide` | Bild links, Text rechts | Grid, Bild links. |
| `image-slide` | Eine große Grafik (z. B. Diagramm) | Bild zentriert, skaliert auf Folienhöhe. |
| `table-slide` | Folie, deren Kern eine Tabelle ist | Tabellenstil global (blaue Header). |
| `agenda-slide` | Agenda / Gliederung | Nutzt die `.agenda`-Liste (siehe unten). |
| `low-text-slide` | Sehr wenig Text, groß gesetzt | Linksbündig, große Schrift. |

Faustregeln zur Wahl:

- Überwiegend Bullets/kurzer Text → `content-slide`.
- Viel Fließtext, lange Aufzählungen (Beamer-„Wall of text") → `pdf-slide`.
- Enthält Codeblock/-blöcke → immer zusätzlich `code-slide`.
- Enthält ein zentrales Bild/Diagramm ohne viel Text → `image-slide`.
- Bild **und** Code untereinander → `image-slide code-slide` kombinieren.

---

## 3. Titelfolie (Muster)

Titel- und Schlussfolie sind identisch aufgebaut:

```markdown
## <Titel der Vorlesung> {.title-slide data-state="hide-footer"}

<img class="title-image" src="../../images/datenschutz.jpg" alt=""
     style="--title-image-width: 120vw; --title-image-right: -500px;
            --title-image-top: 0px; --title-image-height: 100vh;
            --title-image-object-position: right right;">

Prof. Dr. <Name>   
HTW Dresden  
{{< meta date >}}
```

- `data-state="hide-footer"` blendet Footer/Logo/Nummer auf dieser Folie aus.
- Das `<img class="title-image">` ist die **einzige** erlaubte Stelle für
  Inline-`style`, und nur zum Justieren des Hero-Bilds über die CSS-Variablen
  (`--title-image-*`). Diese Variablen sind vom Theme vorgesehen.
- Die drei Zeilen am Ende: zwei Leerzeichen am Zeilenende erzwingen den Umbruch.

### Abschlussfolie (Pflicht)

**Jede Präsentation endet mit einer „Vielen Dank!"-Folie.** Sie ist identisch zur
Titelfolie aufgebaut (gleiche Klasse, gleiches Hero-Bild, gleiche drei Zeilen),
nur mit „Vielen Dank!" als Überschrift. Sie steht als letzte Folie **nach** dem
Literaturverzeichnis.

```markdown
## Vielen Dank! {.title-slide data-state="hide-footer"}

<img class="title-image" src="../../images/datenschutz.jpg" alt=""
     style="--title-image-width: 120vw; --title-image-right: -500px;
            --title-image-top: 0px; --title-image-height: 100vh;
            --title-image-object-position: right right;">

Prof. Dr. <Name>   
HTW Dresden  
{{< meta date >}}
```

Dieselben `--title-image-*`-Werte wie auf der Titelfolie verwenden, damit Titel-
und Schlussfolie optisch zusammenpassen.

---

## 4. Agenda (Muster)

```markdown
## Agenda {.content-slide .agenda-slide}

<ul class="agenda">
<li class="agenda-item"><strong>01</strong><span>Erstes Thema</span></li>
<li class="agenda-item"><strong>02</strong><span>Zweites Thema</span></li>
<li class="agenda-item"><strong>03</strong><span>Drittes Thema</span></li>
</ul>
```

Die `.agenda`/`.agenda-item`-Struktur ist Pflicht — das Grid, die Nummern-Kästen
und die Abstände kommen aus dem Theme. Bis zu ~6 Punkte werden automatisch kleiner
gesetzt.

---

## 5. Code-Folien

### 5.1 Codeblock einbetten

Immer eingezäunte Blöcke mit Sprachkennung verwenden:

````markdown
## Reflektierte XSS Angriffe {.content-slide .code-slide}

```{.javascript}
app.get('/', (req, res) => {
    const { source } = req.query
    res.send(`<h1>Hi ${source}</h1>`)
})
```
````

Sprachen, die hier vorkommen: `javascript`, `html`, `http`, `text`.

### 5.2 Zeilen hervorheben / schrittweise aufdecken

Mit `code-line-numbers` einzelne Zeilen betonen oder per `|` schrittweise
aufdecken (jeder `|`-Abschnitt ist ein Klick):

````markdown
```{.javascript code-line-numbers="|1|2|3-9|5"}
```
````

- `"2"` → nur Zeile 2 hervorheben
- `"3-9"` → Zeilenbereich
- `"|1|2|3-9"` → erst nichts, dann Zeile 1, dann 2, dann Bereich 3–9

### 5.3 Inline-Code im Fließtext

Ein Backtick statt drei — Code läuft mitten im Text mit (Monospace, kein
eigener Kasten, kein Highlighting):

```markdown
- `<script src='USER_DATA_HERE'></script>` kann niemals sicher sein.
```

### 5.4 Bild + Code auf einer Folie

`image-slide` und `code-slide` kombinieren; Bild zuerst, dann der Codeblock:

````markdown
## Beispiel {.image-slide .code-slide}

![](../../images/diagramm.jpg)

```{.html}
<p>Search result for hey there</p>
```
````

---

## 6. KRITISCH: `<script>` und Payloads in XSS-/Web-Folien

Diese Vorlesungen zeigen oft HTML-/JS-Payloads **als Text**. Steht ein
`<script>…</script>` als **normaler Fließtext** (Bullet, Absatz) in der `.qmd`,
führt Reveal.js es beim Laden tatsächlich aus (z. B. ein `alert()`-Popup bei
jedem Reload). Das ist der häufigste Fehler bei diesen Folien.

Regeln:

- Payloads im Fließtext **immer in Backticks** setzen:
  ```markdown
  - **User input:** `<script>alert(document.cookie)</script>`
  ```
  Innerhalb von Backticks wird alles wörtlich als Text dargestellt, nichts
  ausgeführt.
- Alternativ HTML-escapen: `&lt;script&gt;…&lt;/script&gt;`.
- Payloads **innerhalb** eines ```` ```html ````-Codeblocks sind unkritisch — die
  werden als Text gerendert, nicht ausgeführt. Die müssen **nicht** angefasst
  werden.
- URL-enkodierte Payloads (`%3Cscript%3E…`) sind harmlos und bleiben, wie sie
  sind.

Kurz: **Jedes `<script>` außerhalb eines Codeblocks → in Backticks.**

---

## 7. Callout-Boxen (farbige Problem/Lösung-Kästen)

LaTeX-Beamer-Blöcke (farbige Titelbalken + heller Body) werden zu Quarto-Callouts:

```markdown
::: {.callout-important title="Problem"}
Browser führen jeden eingebetteten JavaScript-Code aus – auch injizierten.
:::

::: {.callout-tip title="Lösung"}
Server definiert per HTTP-Header, welche Script-Quellen erlaubt sind.
:::
```

Farbzuordnung:

- `callout-important` → **rot** (Problem, Risiko, Gefahr)
- `callout-tip` → **grün** (Lösung, Schutz, Empfehlung)
- `callout-note` → **blau** (Hinweis, neutrale Info, „inhaltsbasiert/zeitbasiert")
- `callout-warning` → orange, `callout-caution` → gelb (seltener)

**Falle:** Jeder Callout muss mit einem eigenen `:::` **geschlossen** werden.
Ein fehlendes `:::` verschluckt den folgenden `---`-Trenner und zerschießt die
Folienstruktur. Vor jedem `---` prüfen, ob alle offenen `:::` geschlossen sind.

Code **innerhalb** eines Callouts als normalen Codeblock einbetten; darauf achten,
dass Blöcke und der Callout jeweils sauber geschlossen sind.

---

## 8. Tabellen

Normale Markdown-Tabellen verwenden, Folie als `table-slide` markieren. Der Stil
(blaue Kopfzeile, Padding, Scroll) kommt global aus dem Theme — **keine**
Inline-Styles pro Tabelle.

```markdown
## CSP-Direktiven {.content-slide .table-slide}

| Direktive | Kontrolliert |
|---|---|
| `script-src` | JavaScript-Quellen |
| `style-src` | CSS-Quellen |
```

---

## 9. Diagramme (Client/Server-Abläufe) → Mermaid

Beamer-Grafiken mit Säulen + Pfeilen (z. B. Session-Cookie-Ablauf,
Client↔Server↔Angreifer) werden als **Mermaid-`sequenceDiagram`** neu gezeichnet,
nicht als Bild eingebunden. Folie als `content-slide` (ggf. mit Spalten).

````markdown
```{mermaid}
sequenceDiagram
    participant C as Client
    participant S as Server
    C->>S: POST /login HTTP/1.1<br>username=alice
    Note right of S: G() -> k
    S->>C: HTTP/1.1 200 OK<br>Set-Cookie: sessionId=1234
```
````

Konventionen:

- `->>` = Anfrage (durchgezogen), `-->>` = Antwort (gestrichelt).
- `Note right of X:` / `Note over X,Y:` für Operationen/Kommentare.
- `loop <Text> … end` für Wiederholungen.

**Mermaid-Fallen (führen zu „Syntax error in text"):**

- **Keine `→`-Pfeile** in Beschriftungen — nur ASCII `->` verwenden.
- **Kein `;` direkt vor `<br>`** (`sessionId=1234;<br>` bricht). Semikolon
  weglassen oder durch Komma ersetzen.
- **Kein `;` in Nachrichtentexten innerhalb von `loop`-Blöcken** — dort Komma statt
  Semikolon.
- Keine Sonderzeichen wie `✓` in Notes; stattdessen `OK!` ausschreiben.
- Bei Fehlern minimal anfangen (zwei Teilnehmer, ein Pfeil) und schrittweise
  ergänzen, bis die fehlerhafte Zeile gefunden ist.

Wenn eine Grafik sich **nicht** sinnvoll als Sequenzdiagramm abbilden lässt (Fotos,
Screenshots, Diagramme aus der Vorlesung), dann als `image-slide` mit dem Bild
einbinden.

---

## 10. Abstände / Layout

- Vertikalen Abstand **nicht** mit `\n` erzeugen (wird wörtlich ausgegeben).
- Für einen Absatz: eine echte Leerzeile.
- Für mehr Luft: `<br>` bzw. `<br><br>`, oder ein Spacer
  `<div style="height: 1.5em;"></div>` (sparsam einsetzen).
- Keine absolute Positionierung, keine großen negativen `left`/`top`-Werte, keine
  Pixel-Hacks pro Folie (siehe `AGENTS.md`). Layout kommt aus den Slide-Klassen.

---

## 11. Bilder

```markdown
![](../../images/dateiname.jpg)
```

- Pfade relativ zum `.qmd`-Speicherort (in den Vorlagen `../../images/…`).
- Für „ein Bild ist die Folie" → `image-slide`.
- Für Text+Bild nebeneinander → `text-image-slide` / `image-text-slide` mit
  `:::: {.columns}`.
- Keine festen Pixelmaße erzwingen; das Theme skaliert Bilder auf die Folienhöhe.

---

## 12. Checkliste vor dem Abschluss einer konvertierten Datei

1. Frontmatter vollständig (`pagetitle`, `veranstaltung`, `studiengang`,
   `professor`, `date`).
2. Jede Folie hat eine passende Slide-Klasse.
3. Titelfolie am Anfang **und** „Vielen Dank!"-Abschlussfolie am Ende (nach dem
   Literaturverzeichnis), beide mit `title-slide` + `data-state="hide-footer"` und
   identischen `--title-image-*`-Werten.
4. **Alle `<script>` außerhalb von Codeblöcken in Backticks** (Abschnitt 6).
5. **Alle Callouts mit `:::` geschlossen**, kein `---` von einem offenen Callout
   verschluckt (Abschnitt 7).
6. Codeblöcke mit korrekter Sprachkennung.
7. Mermaid-Diagramme frei von `→`, `;<br>` und `;` in `loop`-Nachrichten
   (Abschnitt 9).
8. Kein `\n` als Abstandshalter, keine Inline-Styles außer der `title-image`.
9. Kein Footer/Logo/Datum manuell eingefügt.
10. Keine doppelten Folien (Beamer-Overlays, die als mehrere identische Seiten
    exportiert wurden, zu **einer** Folie zusammenfassen — ggf. mit
    `code-line-numbers`/`.fragment` statt Kopien).