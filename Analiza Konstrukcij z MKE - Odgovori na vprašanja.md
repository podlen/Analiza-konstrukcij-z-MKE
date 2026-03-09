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

Rešitev numeričnega modela je eksaktna ko rešitev eksaktno izpolnjuje DE na celotnem območju. Rešitev eksaktno izpolnjuje tudi RP in PP. 

## 6. Opiši izhodišča MKR.

Osnovna ideja MKR je, da v določenih točkah aproksimiramo odvode. Aproksimacija odvodov v določeni točki temelji na razvoju funkcije v Taylorjevo vrsto:
$$f(x+h) = f(x) + h f'(x) + \frac{h^2}{2!} f''(x) + \frac{h^3}{3!} f'''(x) + \mathcal{O}(h^4)$$

To nam omogoča, da poljubni red odvoda zapišemo kot kombinacijo funkcijskih vrednosti.

Rešitev problema z MKR so funkcijske vrednosti v diskretnih točkah. Med točkami lahko naknadno napnemo interpolacijsko funkcijo. Najbolj pogosti sta linearna in kvadratna funkcija. Polinomi višje stopnje nam lahko dajo ne-fizikalne rešitve.

Primarni robni pogoji in primarni pogoji prehoda so pri MKR izpolnjeni eksaktno (to velja če imamo na robu/prehodu območja točko). Sekundarni pogoji pa so izpolnjeni aproksimativno preko aproksimacije odvoda.

## 7. Prednosti in slabosti MKR.

Prednost MKR je preprostost - še posebej za 1D in tudi 2D primere. MKR se uporablja tudi za obravnavo nestacionarnih primerov, kjer z MKR opišemo kako se problem razvija skozi čas.

Slabost MKR je obravnava problemov v 3D, saj je za njih težavno narediti mrežo (še posebej pri neki poljubni geometriji). Aproksimacija odvodov temelji na diferenčnih shemah, ki zahtevajo ekvidistančno mrežo. 

Pri MKR je čas računanja lahko daljši, saj je matrika koeficientov polna in nesimetrična.
## 8. Opiši izhodišča MKE.

MKE bazira na integralski formulaciji problema. Za primer palice:
$$\int_0^L\biggr[\frac{d}{dx}\biggr(EI_u\biggr(\frac{d}{dx}u(x) - \alpha\Delta T(x)\biggr)\biggr) + n(x)\biggr]v(x)\space dx = 0 $$

Zgornjo funkcijo lahko *per-partes* integriramo in dobimo šibko obliko integralske formulacije, ki je osnova za izpeljavo MKE.


Obravnavano območje razdelimo na podobmočja - ta imenujemo končni elementi. Na območju KE aproksimiramo neznane veličine.


## 9. Prednosti in slabosti MKE.

Prednosti je, da je v rešitvi DE zajeta celotna domena. Prav tako je prednost v tem, da so lahko KE poljubne velikosti, kar nam omogoča mreženje poljubnih geometrij.

Slabost MKE je računska intenzivnost. Obstajajo metode, ki pohitrijo izračune - izkorišča se simetričnost in pasovnost matrike koeficientov.  

## 10. Primerjaj MKR in MKE

**Izpolnjevanje DE**
MKR:
- [ ] DE je izpolnjena po točkah. Med točke lahko napnemo aproksimacijsko funkcijo. 
MKE:
- [ ] DE je izpolnjena po celotnem območju (ne nujno eksaktno)

**Upoštevanje RP**


MKR:
- [ ] Primarna količina je izpolnjena eksaktno, sekundarna pa aproksimativno (diferenčne sheme)
MKE:
- [ ] Primarna in sekundarna količina sta izpolnjeni eksaktno. To sledi iz izpeljave in *per-partes* integracije, ki znižuje red odvoda za 1 stopnjo na enkrat. Tako pridemo do eksaktnih izrazov za sekundarne robne pogoje.
# Predavanje 3: 2.3.2026

## 11. Opiši izhodišča MRE.
MRE je zasnovana na integralski formulaciji - natančneje na inverzni obliki integralske formulacije.

Ograja obravnavanega območja je razdeljena na pod-območja - robne elemente. V območju znotraj robnega elementa **aproksimiramo** neznane veličine.

MRE se uporablja za potencialne probleme. Uporablja se tudi za reševanje fizikalnih problemov, ki niso prostorsko omejeni - verjetno kak elektromagentizem.
## 12. Prednosti in slabosti MRE.
**Prednosti**:
- Reševanje območnega problema prevedemo na iskanje neznanih veličin na ograji. Elementi so samo na robu območja, kar pomeni, da imamo za izračunati manj neznank.
- Primerno za reševanje potencialnih problemov (gravitacijski potencial, ustaljen prevod toplote, električni potencial)
- Primerno za reševanje fizikalnih problemov, ki niso prostorsko omejeni
**Slabosti**:
- Poln sistem enačb
- Za izračun vrednosti znotraj obravnavanega območja so potrebni dodatni izračuni.
## 13. Primerjaj MKE in MRE.
Obe metodi izvirata iz integralske formulacije, kar pomeni, da je rešitev definirana na celotnem območju. Glavna razlika med metodami je sestava sistema enačb, ki ga uporabimo za izračun problema. Togostna matrika je pri MKE simetrična in pasovna. Pri MRE pa je matrika polna, ampak nekoliko manjša.

Pri obeh metodah je rešitev vrednost primarne in sekundarne spremenljivke v vozliščih. Pri MKE so vozlišča postavljena po celotni domeni (na ograji in v notranjosti). Pri MRE pa le na ograji. 

V obeh primerih so robni pogoji eksaktno določeni. 

Pogoji prehoda so pri MKE eksaktno določeni (primarna in sekundarna spremenljivka). Pri MRE pa pogojev prehoda nimamo, saj vse točke ležijo na robu območja.
## 14. Opiši izhodišča MKV.
MKV je zasnovana na integralski formulaciji problema, pri čemer se integral po območju (z Gaussovim izrekom) preoblikuje na integral po ograji, ki omejuje obravnavano območje. 

Obravnavano območje je razdeljeno na pod-območja, ki jih imenujemo končni volumni. Znotraj KV so neznane vrednosti **primarne veličine v eni točki**.
## 15. Prednosti in slabosti MKV.
**Prednosti**:
- reševanje območnega problema prevedemo na iskanje vrednosti v posamezni točki - diskretizacija.
- enostavno izpolnjevanje PP med celicami oz. pod-območji.
- Podobno kot MKR - primarna spremenljivka v točki.
- Primerno za reševanje problemov prevoda toplote, toka tekočine

**Slabosti**:
- Robni pogoji primarnih veličin so izpolnjeni aproksimativno, saj točka v kateri določimo primarno veličino ni na robu KV.
## 16. Primerjaj MKR in MKV.
Obe metodi rešujeta problem z iskanjem vrednosti primarne veličine v diskretnih točkah območja. 

Razlikujeta se v matematični formulaciji. MKR temelji na aproksimaciji odvodov z funkcijskimi vrednostmi (s pomočjo razvoja v Taylorjevo vrsto). MKV pa temelji na integralski formulaciji, ki jo prevedemo na integral po ograji območja. Integral se nato aproksimira enako kot pri MKR. 

Pri MKR je primarni robni pogoj izpolnjen eksaktno (točka mora biti na robu območja). Sekundarni RP pa so aproksimirani preko vrednosti primarne spremenljivke. Pri MKV je ravno obratno. Sekundarni RP so eksaktno izpolnjeni, primarni RP pa so izpolnjeni aproksimativno z interpolacijo od računske točke KV do roba.

Za MKR so primarni PP izpolnjeni eksaktno, sekundarni pa aproksimativno. Pri MKV je obratno.
## 17. Primerjaj MKE in MKV.
Obe metodi izvirata iz integralske formulacije problema. Pri MKE neznano veličino aproksimiramo po celotnem območju končnega elementa. Pri MKV pa se integral po območju prevede na integral po površini (ograji volumna), primarna veličina pa se izračuna le v eni diskretni točki znotraj posameznega KV.

Robni pogoji so pri MKE izpolnjeni eksaktno (primarni in sekundarni). Pri MKV so primarni RP izpolnjeni aproksimativno (z interpolacijo). Sekundarni RP so izpolnjeni eksaktno. 

Pogoji prehoda so pri MKE izpolnjeni eksaktno. Pri MKV je pogoj prehoda za sekundarne spremenljivke izpolnjen eksaktno, vrednost primarne spremenljivke med KV pa je določena aproksimativno.
## 18. Komentiraj izpolnjevanje diferencialne enačbe, robnih pogojev in pogojev konsistentnosti prehoda v primeru uporabe MKR.
Diferencialna enačba je izpolnjena aproksimativno le v diskretnih točkah. 

Primarni RP so izpolnjeni eksaktno - pogoj za to je da je računska točka na robu območja. Sekundarni RP so izpolnjeni aproksimativno preko vrednosti primarne spremenljivke (rabimo uporabiti dodatne točke, če uporabljamo centralno diferenčno shemo)

PP so izpolnjeni na enak način kot RP.
## 19. Komentiraj izpolnjevanje diferencialne enačbe, robnih pogojev in pogojev konsistentnosti prehoda v primeru uporabe MKE.
Diferencialna enačba je izpolnjena aproksimativno po celotnem območju.

Primarni in sekundarni RP so izpolnjeni eksaktno.

Za PP velja enako kot RP.
## 20. Komentiraj izpolnjevanje diferencialne enačbe, robnih pogojev in pogojev konsistentnosti prehoda v primeru uporabe MRE.
Diferencialna enačba je **v notranjosti območja izpolnjena eksaktno**, po ograji območja pa je izpolnjena aporksimativno.

Primarni in sekundarni RP so izpolnjeni eksaktno.

Ker so elementi samo na robu območja, PP ni.

**DODATNO:**
*   **Zakaj je DE v notranjosti izpolnjena eksaktno?**
    Z dvakratno *per-partes* integracijo (inverzna oblika) prenesemo odvode na testno funkcijo $v(x)$. Pri MRE za $v(x)$ izberemo **fundamentalno (analitično) rešitev** DE, ki se obnaša kot Diracova delta funkcija. Zaradi njenih matematičnih lastnosti integral po notranjosti območja "izgine" oz. se skrči točno v iskano vrednost. Fizika v notranjosti je tako upoštevana 100-% eksaktno, brez aproksimacij. Aproksimacija se vrši le z diskretizacijo na robu (ograji).
*   **Zakaj je to hkrati slabost?**
    Reševanje osnovnega sistema enačb nam da rezultate **samo na robu**. Če želimo določiti vrednost v poljubni notranji točki (npr. $x = a$), moramo fundamentalno (delta) funkcijo pomakniti v to koordinato in **naknadno izračunati nov integral** na podlagi že znanih robnih vrednosti. Vsaka točka v notranjosti torej zahteva svoj, dodaten računski korak.
## 21. Komentiraj izpolnjevanje diferencialne enačbe, robnih pogojev in pogojev konsistentnosti prehoda v primeru uporabe MKV.
Diferencialna enačba je izpolnjena aproksimativno (v povprečju) po posameznem končnem volumnu, vrednost primarne spremenljivke pa določimo v 1 točki.

Sekundarni RP so izpolnjeni eksaktno. Primarni pa aproksimativno z interpolacijo od središča volumna do roba (zato ker računska točka nikoli ni na robu območja).

Za PP velja enako kot RP.
## 22. Priprava geometrijskega modela. 
Priprava geometrijskega modela je prvi korak pri reševanju problema z MKE.

Večino časa je treba geometrijski model poenostaviti:
- detajle, ki bistveno ne vplivajo na rezultate analize odstranimo iz geometrijskega modela.
- pod določenimi pogoji lahko volumske geometrijske modele nadomestimo s ploskovnimi ali celo z linijskimi modeli.
Da lahko to naredimo rabimo poznati fizikalno ozadje problema. Tako lahko osmislimo poenostavitve.

## 23. Izbira oblike KE.
Glede na geometrijski model lahko izbiramo med različnimi končnimi elementi:
**1D KE**:
- 2-vozliščni KE
- 3-vozliščni KE
- Število vozlišč v KE vpliva na natančnost rešitve. (enako velik 3-vozliščni KE bolj natančno popiše dejansko stanje kot 2-vozliščni KE). 
- 3-vozliščni KE lahko bolj natančno popišejo geometrijo - z njimi lahko popisujemo ukrivljene oblike.


**2D KE**:
- 3-vozliščni KE
- 4-vozliščni KE
- 6-vozliščni KE
- 9-vozliščni KE

**3D KE**:
- Tetraedri
- Prizmatični KE

Na splošno so boljši KE tisti, ki imajo več vozlišč, saj nam dajo bolj natančno rešitev. Prav tako lahko KE z več vozlišči znotraj elementa uporabljajo bolj kompleksno interpolacijsko funkcijo - zato rečemo, da so KE z več vozlišči bolj natančni.

Z več vozlišči se podaljša čas izračuna. Prav tako je potrebno v poštev vzeti čas za pripravo mreže. 

Pri izbiri oblike KE se lahko navežemo še na mreženje, ki vpliva na obliko uporabljenih KE:
- **Prosto mreženje**: Uporablja se predvsem trikotne (2D) in tetraedrične (3D) KE. Priprava mreže je hitra in avtomatizirana, primerna za zelo kompleksne oblike.
- **Strukturirano mreženje:** Uporablja se štirikotne (2D) in heksaedrične/kockaste (3D) elemente. Zahteva več časa za pripravo geometrije, a pogosto daje boljše rezultate.
