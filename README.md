# 🧩 Mathmosaic: Vertex Nexus

> *„Když se čísla setkají na vrcholu, probudí se rovnice.“*  

---

## Základní idea  

**Mathmosaic** je logicko-strategická hra na hexové mřížce.  
Každá destička (*tile*) má na svých hranolcích čísla a operátory.  
Když se tři hrany z různých tiles protnou v jednom bodu (*vortex*),  
vyhodnotí se mini-rovnice – a svět matematiky ožije.  

Cílem je vytvářet validní kombinace, řetězit výpočty a získávat body za logické i strategické umístění destiček.  

---

## Herní princip  

- Hexová mřížka (6 směrů místo 4).  
- Každý tile má 6 hranic: může na nich být číslo (1–13), operátor (+ − × ÷) nebo nic.  
- Když tři hrany z různých tiles sdílí společný bod, vznikne **vortex**.  
- Pokud má vortex 2 čísla a 1 operátor → proběhne výpočet.  
- Pokud má 3 čísla / 3 operátory → penalizace.  

---

## Herní flow  

1. **Začátek hry:**  
   - Hráč má zásobu tiles (20 ks).  
   - Každý tile je náhodně vygenerovaný (čísla a operátory na hranicích).  

2. **Tah hráče:**  
   - Položí tile na volné místo v mřížce.  
   - Hra zkontroluje 6 vortexů kolem destičky.  
   - Každý validní vortex se vyhodnotí → body + bonusy.  
   - Neplatné vortexy → penalizace.  

3. **Odměny a penalty:**  
   - Výsledek = 7 nebo 11 → + 1 tile.  
   - Výsledek = 13 → „zlatý vortex“ (+ bonus body, efekt).  
   - Neplatný vortex → − max(hodnoty).  

4. **Konec hry:**  
   - Jakmile dojdou tiles, sečte se skóre.  

---

## Výpočet vortexu  

| Kombinace | Akce | Body |
|------------|------|------|
| 2 čísla + 1 operátor | Výpočet | = výsledná hodnota |
| 3 čísla / 3 operátory | Chyba | − max hodnota |
| Jiná kombinace | Nic | 0 |

Výsledky > 13 zůstávají – mohou řetězit další reakce.  
Součet všech validních vortexů = aktuální skóre.  

---

## Bodování a bonusy  

| Výsledek | Efekt |
|-----------|--------|
| 5 | + 1 bod |
| 7 | + 1 tile |
| 11 | + 2 tiles |
| 13 | „stabilní tile“ – nelze dále měnit |
| Nevalidní | − max(vortex hodnoty) |

---

## Technická architektura  

**Jazyk:** C++ 17  
**Knihovna:** raylib  
**Build:** CMake  
**Cíl:** Windows / Linux  

### Struktura souborů  

```
src/
 ├── main.cpp
 ├── Game.cpp / Game.h
 ├── Board.cpp / Board.h
 ├── Tile.cpp / Tile.h
 ├── Vertex.cpp / Vertex.h
 └── Edge.cpp / Edge.h
include/
assets/
build/
```

### Základní třídy  

| Třída | Popis |
|--------|--------|
| `Game` | hlavní smyčka + UI + skóre |
| `Board` | správa mřížky, vortexů, umístění |
| `Tile` | 6 hran, pozice, rotace |
| `Edge` | typ (None, Number, Operator) + hodnota |
| `Vertex` | trojice hran → vyhodnocení rovnice |
| `ScoreEngine` | výpočet bodů a bonusů |

---

## Vývojový plán  

| Fáze | Popis | Cíl |
|------|--------|-----|
| I. Koncept | Dokončit pravidla a dokumentaci | Přehledný design |
| II. Engine setup | Okno, mřížka, tile renderer | První vizuální build |
| III. Logika vortexů | Detekce a výpočet tří hran | Základ bodování |
| IV. Score & bonusy | Systém body / tiles | Herní loop |
| V. Efekty a UI | Animace, zvuky, barvy | Prezentovatelná verze |
| VI. Balanc & testy | Doladění matematiky a obtížnosti | Finální prototyp |

---

## Atmosféra a styl  

- **Vizuál:** čistá geometrie – šestiúhelníky, barevné linky, světelné vortexy.  
- **Hudba:** ambientní, elektronicko-logická („počítací flow“).  
- **UI:** minimalistické – čísla a symboly svítí podle aktivity.  

---

## Cíl projektu  

> Vytvořit originální logickou hru, kde matematika není úkol,  
> ale živý organismus – síť výpočtů, která roste a mění se s každým tahem.  

---
