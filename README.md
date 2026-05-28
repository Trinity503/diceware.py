# Diceware Passphrase Generator

## Inhaltsverzeichnis
- [Beschreibung](#beschreibung)
- [Voraussetzungen](#voraussetzungen)
- [Installation](#installation)
- [Verwendung](#verwendung)
- [Optionen](#optionen)
- [Konfigurationsdatei](#konfigurationsdatei)
- [Beispiele](#beispiele)
- [Lizenz](#lizenz)

---

## Beschreibung

**Diceware Passphrase Generator** erzeugt sichere Passphrasen, indem er zufällige Daten aus dem Betriebssystem-Zufallszahlengenerator liest und diese verwendet, um Wörter aus einer Diceware-Wortliste auszuwählen.

Für mehr Informationen über Diceware, siehe:
[http://world.std.com/~reinhold/diceware.html](http://world.std.com/~reinhold/diceware.html)

---

## Voraussetzungen

- **Python 3.x**
- Internetverbindung (beim ersten Start, für den Download der Wortliste)

---

## Installation

1. **Repository klonen oder Datei herunterladen:**
   ```bash
   git clone https://github.com/Trinity503/diceware.git
   cd diceware
   ```

2. **Skript ausführbar machen (Linux/macOS):**
   ```bash
   chmod +x diceware.py
   ```

3. **Beim ersten Start** wird die gewählte Wortliste automatisch heruntergeladen und unter `~/.diceware.py/cache/` gespeichert.

---

## Verwendung

```bash
python3 diceware.py [OPTIONEN]
```

oder (nach `chmod +x`):

```bash
./diceware.py [OPTIONEN]
```

---

## Optionen

| **Option**               | **Beschreibung**                                                                 | **Standard** |
|--------------------------|---------------------------------------------------------------------------------|--------------|
| `-n N`, `--words N`      | Anzahl der Wörter in der Passphrase                                             | `5`          |
| `-s M`, `--special M`    | Anzahl der Sonderzeichen, die in die Passphrase eingefügt werden                | `0`          |
| `-d D`, `--digits D`     | Anzahl der Ziffern, die eingefügt werden (überschreibt keine Sonderzeichen)     | `0`          |
| `-l LANG`, `--lang LANG` | Sprache der Wortliste (`de`, `en`, `fi`, `it`, `nl`, `se`, `tr`)               | `en`         |
| `-f FILE`, `--file FILE` | Pfad zu einer benutzerdefinierten Wortliste (überschreibt `-l`)                 | –            |
| `-p P`, `--separator P`  | Trennzeichen zwischen den Wörtern                                               | `" "` (Leerzeichen) |
| `-g`, `--grid`           | Erzeugt ein NxN-Raster von Wörtern (erschwertes Mitlesen)                      | –            |

### Unterstützte Sprachen:

| **Kürzel** | **Sprache**     |
|------------|-----------------|
| `de`       | Deutsch         |
| `en`       | Englisch        |
| `fi`       | Finnisch        |
| `it`       | Italienisch     |
| `nl`       | Niederländisch  |
| `se`       | Schwedisch      |
| `tr`       | Türkisch        |

---

## Konfigurationsdatei

Der Generator unterstützt eine Konfigurationsdatei, die Standardwerte für alle Optionen festlegt.

### Speicherort:
```
~/.diceware.py/config
```

### Format:

```ini
[defaults]
# Sprache der Wortliste (de, en, fi, it, nl, se, tr)
lang = de

# Anzahl der Wörter in der Passphrase
words = 6

# Anzahl der Sonderzeichen
special = 2

# Anzahl der Ziffern (überschreibt keine Sonderzeichen)
digits = 1

# Pfad zu einer benutzerdefinierten Wortliste (leer = Standard)
file =

# Trennzeichen zwischen den Wörtern
separator = -
```

### Beschreibung der Konfigurationsoptionen:

| **Option**  | **Beschreibung**                                              | **Mögliche Werte**                        | **Standard**        |
|-------------|---------------------------------------------------------------|-------------------------------------------|---------------------|
| `lang`      | Sprache der Wortliste                                         | `de`, `en`, `fi`, `it`, `nl`, `se`, `tr` | `en`                |
| `words`     | Anzahl der Wörter in der Passphrase                           | Positive ganze Zahl                       | `5`                 |
| `special`   | Anzahl der Sonderzeichen                                      | Nicht-negative ganze Zahl                 | `0`                 |
| `digits`    | Anzahl der Ziffern (überschreibt keine Sonderzeichen)         | Nicht-negative ganze Zahl                 | `0`                 |
| `file`      | Pfad zu einer benutzerdefinierten Wortliste (Vorrang vor `lang`) | Dateipfad oder leer                    | –                   |
| `separator` | Trennzeichen zwischen den Wörtern                             | Beliebige Zeichenkette                    | `" "` (Leerzeichen) |

### Hinweise:
- **Kommandozeilenoptionen** haben immer **Vorrang** vor den Einstellungen in der Konfigurationsdatei.
- Die Option `file` hat **Vorrang** vor `lang`.
- Zeilen, die mit `#` beginnen, werden als **Kommentare** ignoriert.
- Das Verzeichnis `~/.diceware.py/cache/` wird zum **Cachen** der heruntergeladenen Wortlisten verwendet.

---

## Beispiele

### Einfache Passphrase (5 Wörter, Englisch):
```bash
python3 diceware.py
```
```
passphrase   : cleft cam excess swarm lame
```

### 6 Wörter auf Deutsch:
```bash
python3 diceware.py -n 6 -l de
```
```
passphrase   : Apfel Baum Wolke Stein Fluss Berg
```

### Mit Sonderzeichen und Ziffern:
```bash
python3 diceware.py -n 5 -s 2 -d 2 -l de
```
```
passphrase   : Apfel Baum Wolke Stein Fluss
with specials: Ap#el Ba3m W@lke St2in Fluss
```

### Mit benutzerdefiniertem Trennzeichen:
```bash
python3 diceware.py -n 4 -p "_"
```
```
passphrase   : cleft_cam_excess_swarm
```

### Als NxN-Raster:
```bash
python3 diceware.py -g -n 4
```
```
cleft  cam    excess swarm
lame   bone   crisp  fluff
dawn   elder  frost  giant
hatch  ivory  joust  kneel
```

### Mit eigener Wortliste:
```bash
python3 diceware.py -f /pfad/zur/eigenen/wordlist.txt
```

---

## Format einer benutzerdefinierten Wortliste

Eine gültige Diceware-Wortliste enthält genau **7776 Wörter** im folgenden Format:

```
11111 Wort1
11112 Wort2
11113 Wort3
...
66666 Wort7776
```

Jede Zeile besteht aus:
- **5 Ziffern** (von `11111` bis `66666`)
- **einem Leerzeichen**
- **dem Wort**

---

## Lizenz

```
Copyright (c) 2008, 2009 Petri Lehtinen <petri@digip.org>

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation files
(the "Software"), to deal in the Software without restriction,
including without limitation the rights to use, copy, modify, merge,
publish, distribute, sublicense, and/or sell copies of the Software,
and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
