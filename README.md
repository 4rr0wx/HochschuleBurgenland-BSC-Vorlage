# BSC-Arbeit Vorlage für Hochschule Burgenland

**Die meiste Arbeit und Grundlage für diese Vorlage von [igo3r](https://github.com/igo3r)**

Autoren der Anpassungen in das neue Corperate Design und verwandlung in eine BAC-Arbeit:
- [sieber-soehne ](https://github.com/sieber-soehne)
- [4rr0wx](https://github.com/4rr0wx)

Diese Vorlage wurde von uns der Hochschule Burgenland zur verwendung zur Verfügung gestellt.

# Verzeichnisstruktur

## Hauptverzeichnis
- `thesis.tex`: Hauptdatei des LaTeX-Dokuments. (thesis.tex == main.tex)
- `README.md`: Diese Datei mit Anweisungen und Informationen.

## Verzeichnisse

### `00_preamble`
- Enthält Präambel-Dateien für das LaTeX-Dokument (z.B. Sprach- und Formatierungseinstellungen).

### `01_data`
- Enthält Daten, die in der Arbeit verwendet werden.

### `A_FrontMatter`
- `titlepage.tex`: Erstellt die Titelseite.
- `00_Vorwort.tex`: Enthält das Vorwort.
- `00_abstract_de.tex`: Deutsches Abstract.
- `00_abstract_en.tex`: Englisches Abstract.

### `thesis_chapters`
- Enthält die Kapitel der Arbeit:
  - `01_einleitung/_main.tex`: Einleitung.
  - `02_standDesWissens.tex`: Stand des Wissens.
  - `03_Grundlagen/_main.tex`: Grundlagen.
  - `04_Empirische_Studie/_main.tex`: Empirischer Teil.
  - `05_ergebnisse.tex`: Ergebnisse.
  - `06_schlussfolgerung_ausblick.tex`: Schlussfolgerung und Ausblick.
  - `references.bib`: Literaturverzeichnis.

### `C_BackMatter`
- Enthält Anhänge und zusätzliche Materialien:
  - `defns.bib`: Definitionen und Abkürzungen.
  - `Anhang/_main.tex`: Anhang.
  - `Eidesstattliche Erklärung.tex`: Eidesstattliche Erklärung.


### `references.bib`
- Bibliographie-Datei mit allen Literaturangaben. (Hier muss die eigene Datei aus Zotero eingefügt werden)

## Nützliche Links
- [Apa7 in LaTeX](https://ctan.org/pkg/biblatex-apa)
- [Using Zotero in LaTeX](https://guides.library.iit.edu/c.php?g=720120&p=6296986)

# Benötigte/Empfohlene Plugins für Zotero und VS-Code
### VS-Code
- [Latex-Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
- [Latex-Utilities](https://marketplace.visualstudio.com/items?itemName=tecosaur.latex-utilities)
- [Zotero Connector for VS-Code/LaTeX](https://marketplace.visualstudio.com/items?itemName=bnavetta.zoterolatex)

### Zotero
- [Better Bibtex](https://retorque.re/zotero-better-bibtex/)

> [!IMPORTANT]
> Falls das Plugin mit dem Firefox Browser heruntergeladen wird muss mit Rechtsklick -> Ziel speichern unter heruntergeladen werden, da sonnst Firefox versucht das Plugin für sich zu installieren
> 
Für die Installation in Zotero bitte die Zotero Dokumentation durchsehen


# LaTeX Workshop Configuration in Visual Studio Code

> [!WARNING]
> Falls die Zitate nicht in APA7 generiert werden, die Configuraiton mit dieser anleitung überprüfen.

## Ziel
Diese Anleitung beschreibt, wie man LaTeX Workshop in Visual Studio Code so konfiguriert, dass es automatisch die richtigen Befehle in der richtigen Reihenfolge ausführt, um LaTeX-Dokumente zu kompilieren und Bibliographien zu generieren, um den APA7 Zitierstil zu bekommen.


## Schritte
### 1. Öffnen der Einstellungen
- Gehe zu `Datei > Einstellungen > Einstellungen` oder drücke `Ctrl+,`.

  

### 2. Öffnen der `settings.json`
- Klicke auf das Symbol für die `settings.json` Datei in der oberen rechten Ecke der Einstellungen.

### 3. Hinzufügen der Konfigurationen
Füge die folgenden Konfigurationen in die `settings.json` Datei ein:
```json

{
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": ["%DOCFILE%"],
            "env": {}
        },
        {
            "name": "biber",
            "command": "biber",
            "args": ["%DOCFILE%"]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "pdfLaTeX",
            "tools": ["pdflatex"]
        },
        {
            "name": "latexmk 🔃",
            "tools": ["latexmk"]
        },
        {
            "name": "xelatex",
            "tools": ["xelatex"]
        },
        {
            "name": "pdflatex ➞ bibtex ➞ pdflatex`×2",
            "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
        },
        {
            "name": "xelatex ➞ bibtex ➞ xelatex`×2",
            "tools": ["xelatex", "bibtex", "xelatex", "xelatex"]
        },
        {
            "name": "pdflatex -> biber -> pdflatex*2",
            "tools": ["pdflatex", "biber", "pdflatex", "pdflatex"]
        }
    ],
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.latex.autoClean.run": "onBuilt"
}

```

### 4. Verwenden des Rezepts
- Drücke `Ctrl+Shift+P`, um die Kommandozeile zu öffnen.
- Wähle `LaTeX Workshop: Build with recipe`.
- Wähle das Rezept `pdflatex -> biber -> pdflatex*2`.

### 5. Kompilieren des Dokuments
- LaTeX Workshop wird nun automatisch die richtigen Befehle in der richtigen Reihenfolge ausführen, wenn du deine `.tex` Datei änderst und speicherst.

Beispiel für ein Zitat: \autocite[14-15]{favaro2012} wobei favaro2012 der Cite-Key ist.