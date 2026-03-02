---
tags:
  - fakulteta
  - mag
  - AKMM
file_creation: 2026-02-23
---
Zbirka odgovorov na vprašanja pri predmetu analiza konstrukcij z MKE.

# Predavanje 1 - 16.2.2026
## 1. Značilnosti geometrijskega modela.
Geometrijski model popisuje **geometrijski prostor** analiziranega območja. Ponavadi geometrijski model izdelamo s CAD programi.

Geom. model vključuje vse elemente geometrijskega območja analiziranega problema. Ponavadi ga je za potrebe numeričnega modela poenostaviti. Za poenostavitve je ključno poznati fizikalno ozadje problema. 

Poenostavimo lahko na več načinov:
- [ ] simetrije
- [ ] če je več enakih elementov - upoštevamo le enega (lopatice turbine npr.)
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

Dogajanje je lahko časovno spremenljivo ($\frac{\partial }{\partial t}\neq 0$) ali nespremenljivo ($\frac{\partial }{\partial t} = 0$).

Razumevanje fizikalnega dogajanje je ključno, saj nam napačen fizikalni model vrača napačne rešitve problema - tudi če je numerični model napreden.

Razumevanje fizikalnega modela nam omogoča tudi vrednotenje rezultatov - pogledamo ali je rezultat fizikalno smiseln ali ne.

## 3. Značilnosti matematičnega modela.

Matematični model opisuje fizikalno dogajanje z enačbami. Treba se je zavedati, da je matematični model približek dejanskega dogajanja - rabimo vedeti pod kakšnimi pogoji lahko enačbo uporabimo. 

# Predavanje 2 - 23.2.2026
## 4. Značilnosti numeričnega modela.

Numerični model lahko enačbe izpolnjuje **eksaktno** - eksaktno reševanje:
- [ ] To pomeni da je DE izpolnjena v vseh točkah območja (eksaktno), prav tako so eksaktno izpolnjeni RP in PP.

V večini primerov eksaktne rešitve DE ni mogoče določiti. 

Zato enačbe lahko rešujemo tudi **aproksimativno**:
- [ ] Rešitev je aproksimativna če DE ni izpolnjena v vseh točkah (eksaktno izpolnjena) ali pa ni izpolnjena na robovih območja (RP ali PP).
Aproksimativno reševanje prevede reševanje DE v reševanje sistema linearnih enačb. 
Pri izbiri aproksimativne metode se je treba zanašati na značilnosti fizikalnega modela.
## 5. Kdaj je rešitev numeričnega modela eksaktna?

Rešitev numeričnega modela je eksaktna ko rešitev eksaktno izpolnjuje DE na celotnem območju. Rešitev izpolnjuje tudi RP in PP. 

## 6. Opiši izhodišča MKR.

Osnovna ideja MKR, da v določenih točkah aproksimiramo odvode. Aproksimacija odvodov v določeni točki temelji na razvoju funkcije v Taylorjevo vrsto:
$$f(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + \cdots$$

To nam omogoča, da poljubni red odvoda zapišemo kot kombinacijo funkcijskih vrednosti.

Rešitev problema z MKR so funkcijske vrednosti v diskretnih točkah. Med točkami lahko naknadno napnemo interpolacijsko funkcijo. Najbolj pogosti sta linearna in kvadratna funkcija. Polinomi višje stopnje nam lahko dajo ne-fizikalne rešitve.

Primarni robni pogoji in primarni pogoji prehoda so pri MKR izpolnjeni eksaktno (to velja če imamo na robu/prehodu območja točko). Sekundarni pogoji pa so izpolnjeni aproksimativno preko aproksimacije odvoda.

## 7. Prednosti in slabosti MKR.

Prednost MKR je preprostost - še posebej za 1D in tudi 2D primere.

Slabost MKR je obravnava problemov v 3D, saj je za njih težavno narediti mrežo (še posebej pri neki poljubni geometriji). Aproksimacija odvodov temelji na diferenčnih shemah, ki zahtevajo ekvidistančno mrežo. 

Pri MKR je čas računanja lahko daljši, saj je matrika koeficientov polna in nesimetrična.
## 8. Opiši izhodišča MKE.

MKE bazira na integralski formulaciji problema. Za primer palice:
$$\int_0^L\biggr[\frac{d}{dx}\biggr(EI_u\biggr(\frac{d}{dx}u(x) - \alpha\Delta T(x)\biggr)\biggr) + n(x)\biggr]v(x)\space dx = 0 $$

Zgornjo funkcijo lahko *per-partes* integriramo in dobimo šibko obliko integralske formulacije, ki je osnova za izpeljavo MKE.


Obravnavano območje razdelimo na podobmočja - ta imenujemo končni elementi. Na območju KE aproksimiramo neznane veličine.


## 9. Prednosti in slabosti MKE.

Prednosti je, da je v rešitvi DE zajeta celotna domena. Prav tako je prednost v tem, da so lahko KE poljubne velikosti, kar nam omogoča mreženje poljubnih geometrij.

Slabost MKE je računska intenzivnost. Obstajajo metode, ki pohitrijo izračune - izkorišča se simetričnost in pasovnost matrike keoficientov.  

## 10. Primerjaj MKR in MKE

**Izpolnjevanje DE**
MKR:
- [ ] DE je izpolnjena po točkah. Med točke lahko napnemo aporksimacijsko funkcijo. 
MKE:
- [ ] DE je izpolnjena po celotnem območju (ne nunjo eksaktno)

**Upoštevanje RP**


MKR:
- [ ] Primarna količina je izpolnjena eksaktno, sekundarna pa aproksimativno (diferenčne sheme)
MKE:
- [ ] Primarna in sekundarna količina sta izpolnjeni eksaktno. To sledi iz izpeljave in *per-partes* integracije, ki znižuje red odvoda za 1 stopnjo na enkrat. Tako pridemo do eksaktnih izrazov za sekundarne robne pogoje.