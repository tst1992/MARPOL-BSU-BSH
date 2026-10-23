# MARPOL-BSU&BSH

Trainer für die Prüfungsfragen **MARPOL** (6 Fragen) und **BSU & BSH**
(14 Fragen) des Sportseeschifferscheins. Die Fragen kommen in zufälliger
Reihenfolge, die Antwort wird frei formuliert und gegen feste
Schlüsselelemente geprüft. Danach erscheint immer die Musterlösung.

Die App läuft ohne Server, ohne Anmeldung und nach dem ersten Aufruf auch
ohne Netz. Gestaltung übernommen aus dem SSS-Trainer Seemannschaft.

---

## Auf GitHub veröffentlichen

1. Auf GitHub ein neues Repository anlegen, z. B. `marpol-bsu-bsh`.
2. **Add file → Upload files** wählen und den **Inhalt** dieses Ordners
   hineinziehen: `index.html`, `manifest.webmanifest`, `sw.js`, `README.md`,
   `.nojekyll` und den Ordner `icons`. Dann **Commit changes**.
   Hinweis: `.nojekyll` ist eine versteckte Datei. Auf dem Mac blendet
   **Cmd + Shift + .** sie im Finder ein. Fehlt sie, läuft die App trotzdem.
3. Im Repository **Settings → Pages** öffnen. Unter **Build and deployment**
   als Quelle **Deploy from a branch** wählen, Branch **main**, Ordner
   **/ (root)**, speichern.
4. Nach ein bis zwei Minuten ist die App erreichbar unter
   `https://<benutzername>.github.io/marpol-bsu-bsh/`.

Alle Pfade sind relativ, die App läuft deshalb auch in einem Unterordner.

## Als App installieren und offline nutzen

- **iPhone/iPad**: Adresse in Safari öffnen → Teilen → „Zum Home-Bildschirm“.
- **Android**: in Chrome öffnen → Menü ⋮ → „App installieren“.
- **Desktop (Chrome/Edge)**: Installations-Symbol rechts in der Adresszeile.

Nach dem ersten Aufruf liegt alles auf dem Gerät. Die App startet dann auch
im Flugmodus. Im Info-Fenster der App steht, ob der Offlinespeicher aktiv ist.

## Örtlich ausprobieren

`index.html` doppelklicken. Die Datei ist in sich geschlossen: Stylesheet,
Programm und alle 20 Fragen stecken darin. Installation und Offlinebetrieb
funktionieren erst über eine Webadresse (GitHub Pages oder z. B.
`python3 -m http.server 8080` in diesem Ordner).

---

## Bereiche und Runden

| Bereich   | Rundengrösse                                              |
| --------- | --------------------------------------------------------- |
| MARPOL    | alle 6 Fragen                                             |
| BSU & BSH | 10 Fragen oder alle 14                                    |
| Gemischt  | 10 (3 MARPOL + 7 BSU & BSH), 15 (5 + 10) oder alle 20     |

Gemischte Runden ziehen im Verhältnis der Bestände. „Nur bisher Falsche
üben“ stellt alle Fragen des gewählten Bereichs, die zuletzt nicht richtig
beantwortet wurden.

Sehr ähnliche Fragen tragen dieselbe `gruppe` und kommen nicht direkt
hintereinander:
`sondergebiete` (MARPOL Nr. 1, 3, 6), `bsu-stelle` (BSU & BSH Nr. 7, 11,
12, 13), `flagge` (BSU & BSH Nr. 8, 9).

## Bewertung und Wiederholung

| Ergebnis  | Bedingung                                                 |
| --------- | --------------------------------------------------------- |
| Richtig   | alle Pflichtelemente und mindestens `mindestanzahl`       |
| Teilweise | mindestens die Hälfte von `mindestanzahl`                 |
| Falsch    | weniger                                                   |

Die Automatik erkennt Begriffe, keine Begründungen. Mit „Doch richtig“ lässt
sich die Bewertung überstimmen.

- **Falsch** oder **gelöst** (Knopf „Lösen“): Die Frage kommt frühestens
  nach drei anderen Fragen wieder, höchstens zweimal. Danach bleibt sie offen.
- **Teilweise** oder **übersprungen**: keine Wiederholung in der Runde, aber
  Eintrag im Ergebnis unter „Noch einmal ansehen“ und in
  „Fehler nochmals üben“.

## Fragen bearbeiten

Die Fragen stehen in `index.html` im Block
`<script id="fragen-daten" type="application/json">`. Je Frage:

```json
{
  "id": "b09", "bereich": "bsu", "nummer": 9, "gruppe": "flagge",
  "frage": "Welches Schiffsdokument …?",
  "loesung": [
    { "p": "Flaggenzertifikat, ausgestellt vom BSH." },
    { "ul": ["Dokument …: Flaggenzertifikat", "Ausstellende Behörde: …"] }
  ],
  "anmerkung": "optional, erscheint unter der Musterlösung",
  "hinweis": "Das Dokument ist nach dem benannt, was es erlaubt …",
  "mindestanzahl": 2,
  "elemente": [
    { "label": "Flaggenzertifikat", "pflicht": true,
      "treffer": ["flaggenzertifikat", "flaggenschein"] }
  ]
}
```

- **`bereich`**: `marpol` oder `bsu`. **`gruppe`**: optional, siehe oben.
- **`loesung`**: Blöcke in Reihenfolge. `{ "h": … }` Zwischenüberschrift,
  `{ "h2": … }` Unterüberschrift, `{ "p": … }` Absatz, `{ "ul": […] }`
  Aufzählung, `{ "ol": […] }` nummerierte Liste.
- **`frage`**: Zeilenumbrüche mit `\n` bleiben in der Anzeige erhalten.
- **`elemente`**: die Schlüsselelemente. `pflicht: true` = muss vorkommen.
  `verneinend: true`, wenn das Element selbst eine Verneinung enthält
  („nicht erlaubt“, „kein Widerspruch“), dann entwertet ein „nicht“ den
  Treffer nicht.
- **`treffer`**: Wörter oder Wortfolgen, die das Element ausdrücken.
  Gross-/Kleinschreibung, Umlaute und ß spielen keine Rolle.
  - `wort` – unter 4 Zeichen exakt, 4 Zeichen am Wortanfang, 5–6 Zeichen auch
    als Wortteil, ab 7 Zeichen als Wortteil mit Tippfehler-Toleranz
    (7–9 Zeichen 1 Fehler, ab 10 Zeichen 2 Fehler)
  - `=wort` ganzes Wort exakt · `^wort` Wortanfang · `~wort` ganzes Wort mit
    Toleranz · `#10-15` Zahl im Bereich
  - Wortfolgen: Wörter in dieser Reihenfolge, bis zu zwei Wörter dazwischen
- **`mindestanzahl`**: so viele Elemente braucht „Richtig“ (zusätzlich zu allen
  Pflichtelementen). „Teilweise“ ab der Hälfte davon.

Nach einer Änderung in `sw.js` die Zeile `const BESTAND = "marpolbsu-v1";`
hochzählen (`v2`, `v3` …), damit installierte Apps die neue Fassung laden.

## Datengrundlage

Fragensammlungen „MARPOL“ und „BSU/BSH“. Fragen und Musterlösungen sind
wörtlich übernommen, mit diesen Ausnahmen:

- **BSU & BSH Nr. 8**: Das Schiffszertifikat stellt das Registergericht
  (Amtsgericht) aus, nicht das BSH (§ 60 SchRegO). Den Internationalen
  Bootsschein stellt auch der ADAC aus. Der Zusatz „(Schiffszertifikat)“ beim
  Flaggenzertifikat ist entfallen.
- **BSU & BSH Nr. 14**: Die Registerpflicht gilt erst bei einer Rumpflänge
  von mehr als 15 m (§ 10 SchRegO); Merkhilfe angepasst.
- **BSU & BSH Nr. 2**: Punkt zur Bewegung der Wasserteilchen in der
  brechenden Welle ergänzt.
- Formatfehler bereinigt: BSU & BSH Nr. 12 (offene Klammer), MARPOL Nr. 3
  (Aufzählung der Frage), MARPOL Nr. 6 (fehlender Schlusspunkt).

Die Hinweise sind für diese App neu formuliert.

## Datenschutz

Keine Übertragung, kein Tracking. Gespeichert werden nur die zuletzt
gewählte Einstellung und der Lernstand (letztes Ergebnis je Frage) im
`localStorage` des Browsers. Zurücksetzen im Info-Fenster.
