# Kiezatlas-Maschine

Der ortsunabhängige Teil des Kiezatlas: Laufzeit-Module der Seiten und Karten, Seitenrahmen, Sprachschicht und
Seitengenerator. Eine Stadt besteht aus dieser Maschine plus eigener Ortskonfiguration (`config/<stadt>.yaml`),
eigenen Texten (`texte/<sprache>/`), eigenen Seitenvorlagen (`vorlagen/`), eigenen Daten (`daten/`) und den
Skripten, die diese Daten aus offenen Quellen berechnen.

Städte, die die Maschine nutzen:

- Kiezatlas Kraków: https://github.com/andremadstop/kiezatlas-krakow
- Kiezatlas Potsdam: https://github.com/andremadstop/kiezatlas-potsdam (Umzug auf die Maschine in Arbeit)

## So kommt die Maschine in eine Stadt

Jede Stadt enthält eine **Kopie** der Maschine zu einem festen Commit. So bleibt jedes Stadt-Repository und jedes
Archiv (z. B. bei Zenodo) für sich allein vollständig und lauffähig.

```sh
# im Stadt-Repository; Maschine liegt daneben unter ../kiezatlas (oder $KIEZ_MASCHINE)
python3 -I skripte/maschine.py holen --commit <commit>   # Dateien aus MASCHINE.txt schreiben, MASCHINE.lock neu
python3 -I skripte/maschine.py pruefen                   # Kopie unverändert? (gehört in die Prüfungen der Stadt)
```

`MASCHINE.txt` nennt die Dateien der Maschine. `MASCHINE.lock` in der Stadt nennt Commit und SHA256 je Datei.
Dateien der Maschine werden in einer Stadt nicht von Hand geändert: Änderungen entstehen hier und kommen über
`holen` in die Städte. Ob eine neue Fassung taugt, entscheiden die Prüfungen der Städte (in jeder Stadt
`./pruefen.sh`), nicht dieses Repository allein.

## Herkunft

Herausgelöst am 16.11.2026 aus dem Kiezatlas Kraków, Commit `e7c85ca13f7e`, Dateien byte-gleich. Was noch
Kraków-Vorgaben trägt (z. B. Standardpfad `config/krakow.yaml` in `skripte/ort_konfig.py`, wenn `$KIEZ_CONFIG`
fehlt), wird hier schrittweise verallgemeinert.

## Lizenz

Apache-2.0 (`LICENSE`), siehe `NOTICE`.

---

**EN.** The place-independent part of the Kiezatlas city atlases (page and map runtime, page frame, language layer,
page generator). Each city repository contains a pinned copy (`MASCHINE.lock`), fetched with
`skripte/maschine.py holen --commit <commit>` and verified with `skripte/maschine.py pruefen`. Apache-2.0.
