# milkycode Bricks Theme

Child Theme für den [Bricks Builder](https://bricksbuilder.io/).

Entwickelt und gepflegt von **milkycode GmbH** – <https://www.milkycode.com>

## Voraussetzungen

- WordPress mit installiertem **Bricks** als Eltern-Theme (Ordner `wp-content/themes/bricks`).
  Das Child Theme verweist in `style.css` mit `Template: bricks` darauf – diese Zeile
  nicht ändern, sonst ist es kein Child Theme mehr.
- Der Ordnername `milkycode-bricks` ist der Slug des Themes in WordPress. Wird er
  geändert, behandelt WordPress das Theme als neues Theme.

## Inhalt

```
milkycode-bricks/
├── style.css         Theme-Kopf (Name, Autor, Version …) und eigenes CSS
├── functions.php     lädt style.css, registriert eigene Elemente
├── elements/
│   └── title.php     Beispiel-Element „Title“ aus dem Bricks-Child-Theme
├── screenshot.png    Vorschaubild unter Design → Themes (1200 × 900)
└── README.md         diese Datei
```

**`functions.php`**

- Bindet `style.css` im Frontend und in der Builder-Vorschau ein, **nicht** im
  Builder-Panel – so verstellt eigenes CSS die Oberfläche des Builders nicht. Die
  Version hängt an `filemtime()`, Browser-Caches werden nach jeder Änderung also
  automatisch umgangen.
- Registriert alle Dateien aus `$element_files` als Bricks-Elemente (Kategorie
  „Custom“ im Builder).

## Eigenes Element hinzufügen

1. Datei in `elements/` anlegen (Vorlage: `elements/title.php`, Anleitung:
   <https://academy.bricksbuilder.io/article/create-your-own-elements>).
2. Pfad in `functions.php` in `$element_files` eintragen.

Texte in den Elementen nutzen bewusst die Text Domain `bricks`, damit die Übersetzungen
von Bricks greifen.

## Installation

ZIP aus dem Repo erzeugen (nur eingecheckte Dateien, ohne Git-Dateien):

```bash
git archive --format=zip --prefix=milkycode-bricks/ -o milkycode-bricks.zip HEAD
```

Das ZIP muss den Ordner `milkycode-bricks/` enthalten (nicht nur dessen Inhalt) – dafür
sorgt `--prefix`. Dann unter **Design → Themes → Theme hinzufügen → Theme hochladen**
einspielen und aktivieren.
Einstellungen, Templates und globale Klassen von Bricks liegen in der Datenbank und
bleiben beim Wechsel des Child Themes erhalten.

## Arbeiten mit Claude Code: Skill `bricks-novamira`

Seiten mit diesem Theme bauen und pflegen wir mit Claude Code über die **Novamira-MCP**-
Verbindung der Website. Dafür gibt es unseren Skill **`bricks-novamira`** mit den
verbindlichen Arbeitsregeln für Bricks über MCP – Elementbäume, CSS-Platzierung,
Spezifitätsfallen, Templates, Formulare, Mehrsprachigkeit, Deploy und Prüfung im
Frontend.

- **Repository (privat):** <https://github.com/milkycode/bricks-novamira>
- **Installation** (macOS, Linux, WSL2):

  ```bash
  git clone https://github.com/milkycode/bricks-novamira.git ~/.claude/skills/bricks-novamira
  ```

  Windows, die Einrichtung der MCP-Verbindung und alle weiteren Schritte stehen in der
  README des Skills.
- **Projektprofil:** Der Skill erwartet im Projekt-Repo eine Datei `bricks-design.md`
  mit den Fakten der jeweiligen Website (Cache, Breakpoints, ID-Präfixe …). Claude legt
  sie auf Wunsch an („Erstelle das Bricks-Projektprofil für diese Website“).
- **Projektspezifischer PHP-Code** (Custom Post Types, Dynamic Tags, eigene Elemente,
  Filter) gehört laut Skill in ein eigenes Site-Plugin (`<projekt>-core`, siehe
  `references/custom-code.md` im Skill). Dieses Child Theme bleibt schlank und
  projektunabhängig.
- **Deploy über MCP:** wie für das Site-Plugin beschrieben (`references/mcp-workflow.md`
  §10), nur mit `theme install … --force` statt `plugin install`. Das ZIP danach
  unbedingt wieder aus `uploads/` löschen.

## Version

Die Version steht im Kopf von `style.css` und wird bei jeder Änderung erhöht.

---

© milkycode GmbH – <https://www.milkycode.com>
