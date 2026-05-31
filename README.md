# EL++ (Easy Language)

Természetes, beszédszerű programozási nyelv **magyar** és **angol** parancsszavakkal.

**GitHub:** [github.com/fonokur55/EL-](https://github.com/fonokur55/EL-)

**Letöltés (Windows):** [Releases](https://github.com/fonokur55/EL-/releases) → `EL++-v0.1.2.zip` → kicsomagolás → dupla kattintás **`install.bat`**

> Az EL++ nem ért meg tetszőleges mondatot – **korlátozott, dokumentált mintákat** használ, szinonimákkal és barátságos hibákkal.

## Telepítés (egy parancs)

**Windows** – a projekt mappájában (PowerShell):

```powershell
.\install.ps1
```

Vagy dupla kattintás: **`install.bat`**

A telepítő **automatikusan telepíti a Pythont is**, ha még nincs a gépen (winget, majd python.org letöltés).

Ez telepíti a nyelvet, hozzáadja az **`el++`** parancsot a PATH-hoz, beállítja az ikonokat és a VS Code bővítményt.

**Fontos a csomagban:** `EL++.png`, `install.bat`, `install.ps1`, `src/`, `vscode-elpp/` — ZIP-be mindet tedd bele!

**Új terminál** után:

```text
el++
```

→ elindul a REPL; azonnal írhatsz programot.

Fájl futtatása:

```text
el++ examples/hello.elpp
```

Manuális telepítés (ha kell):

```bash
pip install -e .
```

## Frissítések

A frissítésfigyelő a [`release.json`](release.json) fájlban lévő **`fonokur55/EL-`** repót használja.

**Ellenőrzés:**

```text
el++ check-update
```

**Automatikus frissítés** (GitHub repo beállítása után):

```text
el++ update          → megkérdezi: frissítsem?
el++ update --yes    → azonnal frissít
```

| Honnan telepítetted | Mit csinál az `el++ update` |
|---------------------|-----------------------------|
| **Git clone** | `git pull` + `install.ps1` |
| **ZIP** | Letölti a legújabb Release ZIP-et + telepít |

GitHub Releases-en legyen **`.zip` csomag** (pl. `EL++-v0.1.2.zip`) minden verzióhoz.

## Visual Studio Code

> **Fontos:** **Visual Studio Code**-ot vagy **Cursor**-t használj — a lila **Visual Studio** (2022) **nem** támogatja a VS Code bővítményeket!

### Telepítés (ajánlott – egy parancs)

```powershell
.\install.ps1
```

Ez létrehozza és telepíti a **`elpp-language-0.1.2.vsix`** fájlt a VS Code-ba.

### Kézi telepítés (ha az automatikus nem sikerül)

1. Nyisd meg a VS Code-ot
2. **Extensions** (Ctrl+Shift+X) → jobb felső **`⋯`** menü
3. **Install from VSIX...** (NEM „Install from Location”!)
4. Válaszd ki ezt a fájlt:

   `vscode-elpp\elpp-language-0.1.2.vsix`

5. Ctrl+Shift+P → **Developer: Reload Window**
6. Extensions listában megjelenik: **EL++ (Easy Language)** az arany tehén ikonnal

### Nyelv kiválasztása

- Nyiss meg egy `.elpp` fájlt (pl. `examples/hello.elpp`)
- Jobb alsó sarok → **EL++**
- Vagy: Ctrl+Shift+P → **Change Language Mode** → **EL++**

### Futtatás szerkesztőből

- **F5** — aktuális `.elpp` fájl futtatása (Output panelen látod a kimenetet)
- **Ctrl+F5** — futtatás terminálban
- Jobb felső **▶ Run** gomb (`.elpp` fájlnál)
- Jobb klikk → **EL++: Aktuális fájl futtatása**
- **Ctrl+Shift+B** — build feladat (terminál)
- Run and Debug panel → **EL++: Aktuális fájl futtatása**

## Példák

### Magyar

```text
legyen x egyen 10
ha x nagyobb mint 5 akkor
    írd ki "nagy"
különben
    írd ki "kicsi"
kész
```

### Angol

```text
set x to 10
if x is greater than 5 then
    print "big"
else
    print "small"
end
```

A hivatalos kiterjesztés: **`.elpp`** (a régi `.el` fájlok továbbra is futtathatók).

### Fájl ikonok – hol jelenik meg a tehén?

| Hol | Automatikus? | Mit kell tenni |
|-----|--------------|----------------|
| **VS Code / Cursor** (fül, oldalsáv) | Igen, minden `.elpp` fájlra | EL++ bővítmény telepítve + Reload Window |
| **Windows Intéző** (Asztal, mappa) | Telepítés után igen | `.\install.ps1`, majd ha kell: `.\refresh-icons.ps1` |

Ha a `.elpp` fájlok fehér lap ikont mutatnak (pl. VS Code volt az alapértelmezett), futtasd újra: `.\refresh-icons.ps1` — ez beállítja az EL++ ikont alapértelmezettként is.

Minden `.elpp` fájl megkapja az ikont — **nem kell fájlonként külön beállítani**.

További demók: [`examples/`](examples/).

## Kulcsszavak (válogatás)

| Jelentés | Magyar | Angol |
|----------|--------|-------|
| Változó | legyen, állíts | set, let, make |
| Kiírás | írd ki, mutasd | print, show, say |
| Feltétel | ha, amennyiben | if, when |
| Ág | akkor | then |
| Különben | különben, egyébként | else, otherwise |
| Ciklus | amíg, ismételd amíg | while, repeat while |
| Blokk vége | kész, vége | end, done |
| Egyenlő | egyen, egyenlő | to, is, equals |
| Nagyobb | nagyobb mint | greater than |
| Kisebb | kisebb mint | less than |

Opcionális töltőszavak (kihagyva): `az`, `the`, `hogy`, …

Komment: `#`, `//`, `megjegyzés:`, `note:`

## Új szinonima hozzáadása

Szerkeszd a [`src/elpp/synonyms.py`](src/elpp/synonyms.py) fájlban a `_PHRASES` listát, majd:

```bash
python -m pytest
```

## Projekt felépítés (bővíthetőség)

```
src/elpp/
  synonyms.py    ← uj magyar/angol szavak (1 sor)
  lexer.py       ← tokenizalas
  parser.py      ← szintaxis / AST
  ast.py         ← program struktura
  interpreter.py ← futtatás
  updater.py     ← frissites
```

**Uj szinonima:** `_PHRASES` listához adsz egy sort → keszen.
**Uj utasitas** (pl. fuggveny): `ast.py` + `parser.py` + `interpreter.py` — tiszta, kis lepesek.

```
src/elpp/        – forráskód
vscode-elpp/     – VS Code bővítmény (.elpp)
examples/        – példaprogramok (.elpp)
install.ps1      – telepítő (+ Python auto)
release.json     – GitHub frissítés beállítás
```

## Licenc

MIT
