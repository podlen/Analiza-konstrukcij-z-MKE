---
tags:
  - fakulteta
  - mag
  - AKMM
file_creation: 2026-02-23
---
Zbirka odgovorov na vprašanja pri predmetu analiza konstrukcij z MKE.

## 1. Značilnosti geometrijskega modela.
Geometrijski model popisuje **geometrijski prostor** analiziranega območja. Ponavadi geometrijski model izdelamo s CAD programi.

Geom. model vključuje vse elemente geometrijskega območja analiziranega problema. Ponavadi ga je za potrebe numeričnega modela poenostaviti. Za poenostavitve je ključno poznati fizikalno ozadje problema. 

Poenostavimo lahko na več načinov:
- [ ] simetrije
- [ ] če je vel enakih elementov - upoštevamo le enega (lopatice turbine npr.)
- [ ] Preproste poenostavitve - glave vijakov, navoji vijakov. Zmanjšamo kompleksnost mreže, brez da prizadenemo natančnost izračuna.
## 2. Značilnosti fizikalnega modela.
Fizikalni model popisuje **fizikalno dogajanje** v analiziranem območju. To ne pomeni enačbe $\rightarrow$ te so v matematičnem modelu.

Fizikalno območje v obravnavanem območju je lahko povezano:
- [ ] mehansko stanje (mehanika deformabilnih teles)
- [ ] termalno stanje
- [ ] termo-mehansko stanje
- [ ] elektro-magnetno stanje
- [ ] dinamika tekočin
- [ ] ipd.

Dogajanje je lahko časovno spremenljivo ali nespremenljivo.

Razumevanje fizikalnega dogajanje je ključno, saj nam napačen fizikalni model vrača napačne rešitve problema - tudi če je numerični model napreden.

Razumevanje fizikalnega modela nam omogoča tudi vrednotenje rezultatov - pogledamo ali je rezultat fizikalno smiseln ali ne.

## 3. Značilnosti matematičnega modela.

Matematični model opisuje fizikalno dogajanje z enačbami. Treba se je zavedati, da je matematični model približek dejanskega dogajanja - rabimo vedeti pod kakšnimi pogoji lahko enačbo uporabimo. 

