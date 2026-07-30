# Magyar Jogtár — a magyar jogrendszer git-natív verziókövetése

Ez a repó a legfontosabb magyar jogszabályok **konszolidált szövegét** tartalmazza
Markdown formátumban, úgy, hogy **a git history maga a jogtörténet**:

- **egy commit = egy időállapot** — a commit dátuma a hatálybalépés napja,
- **a `git diff` = a törvénymódosítás** — szó szerint látszik, mit vettek ki és mit tettek be,
- `git log --follow jogszabalyok/2013-evi-v-torveny-ptk/szoveg.md` — a Ptk. teljes módosítás-történet,
- `git blame` — megmutatja, melyik szakasz mikor változott utoljára,
- `git checkout` egy múltbeli commitra — az akkor hatályos állapot.

## Példák

```bash
# Mit módosított a jogalkotó a Ptk.-n 2024-ben?
git log --since=2024-01-01 --until=2025-01-01 -- jogszabalyok/2013-evi-v-torveny-ptk/

# Két időállapot összevetése
git diff 'main@{2023-01-01}' 'main@{2025-01-01}' -- jogszabalyok/2012-evi-c-torveny-btk/szoveg.md
```

## Szerkezet

```
jogszabalyok/<slug>/szoveg.md   # a konszolidált szöveg (HEAD = aktuális állapot)
jogszabalyok/<slug>/meta.json   # azonosító, cím, forrás-URL, időállapot-lista
index/jogszabalyok.json         # az összes jogszabály listája
index/allapotok.json            # időállapot → commit SHA térkép (a weboldal használja)
```

## ⚠️ Nem hiteles jogforrás

Ez a repó **tájékozódási és kutatási célra** készült, automatikus feldolgozással a
[Nemzeti Jogszabálytár](https://njt.jog.gov.hu) publikus felületéből. **Nem hiteles
szöveg** — a hiteles jogforrás a njt.jog.gov.hu és a Magyar Közlöny. Részletek:
[DISCLAIMER.md](DISCLAIMER.md).

## Frissítés

A repót napi automatikus futás (GitHub Actions) tartja karban: az aznap hatályba
lépő új időállapotokat commitolja. A feldolgozó kód nyílt:
[godavid/gitjog](https://github.com/godavid/gitjog). Weboldal:
[jogtar.remenyfarm.hu](https://jogtar.remenyfarm.hu).

## Licenc

A jogszabályszöveg a szerzői jogról szóló 1999. évi LXXVI. törvény 1. § (4)
bekezdése alapján nem áll szerzői jogi védelem alatt (közkincs). A repó saját
metaadatai és szerkezete: [CC0](LICENSE).
