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
# Predavanje 3 - 2.3.2026

## 11. Opiši izhodišča MRE.
MRE je zasnovana na integralski formulaciji - natančneje na inverzni obliki integralske formulacije.

Ograja obravnavanega območja je razdeljena na pod-območja - robne elemente. V območju znotraj robnega elementa(v robnem elementu) **aproksimiramo** neznane veličine.

MRE se uporablja za potencialne probleme. Uporablja se tudi za reševanje fizikalnih problemov, ki niso prostorsko omejeni - verjetno kak elektromagnetizem.
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

Razlikujeta se v matematični formulaciji. MKR temelji na aproksimaciji odvodov s funkcijskimi vrednostmi (s pomočjo razvoja v Taylorjevo vrsto). MKV pa temelji na integralski formulaciji, ki jo prevedemo na integral po ograji območja. Integral se nato aproksimira enako kot pri MKR. 

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

Na splošno so boljši KE tisti, ki imajo več vozlišč, saj nam dajo bolj natančno rešitev. Prav tako lahko KE z več vozlišči znotraj elementa uporabljajo bolj kompleksno interpolacijsko funkcijo - zato rečemo, da so KE z več vozlišči bolj natančn

Z več vozlišči se podaljša čas izračuna. Prav tako je potrebno v poštev vzeti čas za pripravo mreže. 

Pri izbiri oblike KE se lahko navežemo še na mreženje, ki vpliva na obliko uporabljenih KE:
- **Prosto mreženje**: Uporablja se predvsem trikotne (2D) in tetraedrične (3D) KE. Priprava mreže je hitra in avtomatizirana, primerna za zelo kompleksne oblike.
- **Strukturirano mreženje:** Uporablja se štirikotne (2D) in heksaedrične/kockaste (3D) elemente. Zahteva več časa za pripravo geometrije, a pogosto daje boljše rezultate.

# Predavanje 4 - 9.3.2026
## 24. Prednosti in slabosti prostega mreženja.
**Prednosti**:
- Hitro in avtomatsko
- Dobro ko hočemo videti, kje so kritična mesta
- Omogoča mreženje kompleksnih oblik

**Slabosti**:
- Dobljen rezultat je manj natančen, kot če bi uporabljali strukturirano mrežo
- Uporabljeni so trikotni oz. tetraedrični KE. Ti elementi so bolj togi - zato jih za natančno rešitev potrebujemo več kot pri strukturirani mreži. 
## 25. Prednosti in slabosti strukturiranega mreženja.
**Prednosti**:
- Mreža je prilagojena problemu.
- Bolj natančni izračuni, saj so uporabljeni heksaedrični, kvadratni KE.
**Slabosti**:
- Ker je mreža specifična glede na problem jo moramo sami narediti, kar vzame več časa.
## 26. Kako lahko vplivamo na obliko mreže 2D KE.
Na obliko mreže 2D KE vplivamo tako, da predpišemo število elementov oz. število vozlišč na robu območja oz. pod-območja. Vozlišča na ograji lahko razporedimo enakomerno ali pa uporabimo "bias", ki v določeno smer zgosti elemente.

Prav tako lahko na obliko mreže vplivamo z izbiro geometrije KE. Lahko izberemo trikotne KE, s katerimi je mreženje vedno izvedljivo.

Lahko izberemo štirikotne KE, s katerimi mreženje ni vedno izvedljivo. (Območje razdeljeno na pod-območja, ki imajo 3,4 ali 5 robov)

Lahko uporabimo tudi kombinacijo obeh elementov. Moramo poskrbeti da imamo na kritičnih območjih štirikotne KE.

Na mrežo lahko vplivamo tudi z načinom delitve na pod-območja.


## 27. Kriterij za oceno kvalitete mreže 2D KE.
Kriterijev za oceno mreže je več:
- razmerje med najdaljšo on najkrajšo stranico elementa:
	- $$1\leq f_r=\frac{a}{b}\leq \infty$$
	- $$f_{max}\leq5$$
	- ![[Pasted image 20260309214606.png]]
	
- največji in najmanjši notranji kot trikotnega ali štirikotnega elementa
	- $$0°\leq\alpha\leq180°$$
	- $$45°\leq\alpha_{min}$$
	- $$\alpha_{max}\leq135°$$
	- ![[Pasted image 20260309214748.png]]
- oblikovni faktor (samo za trikotni KE)
	- $$1\geq f_\Delta=\frac{A_\Delta}{A_{\Delta id}}\geq0$$
	- $$f_{\Delta min}\geq0.5$$
	- ![[Pasted image 20260309214946.png]]

- odstopanje stranice KE od geometrije mreženega območja
	- $$0\leq f_g=\frac{h}{L}\leq \infty$$
	- $$f_{gmax}\leq0.1$$
	- ![[Pasted image 20260309215053.png]]
## 28. Kako lahko vplivamo na obliko mreže 3D KE.
Pri prostem mreženju na obliko vplivamo z mrežo, narejeno na površinah (s trikotniki), ki definirajo volumen. Mrežo na površini definiramo z gostoto točk na ograji (enakomerno ali "bias"). Na gostoto tetraedrov v sami notranjosti volumna lahko vplivamo le delno (z načinom generacije) in predvsem posredno preko mreže na površini.

Pri strukturiranem mreženju na obliko mreže vplivamo tako, da kompleksno geometrijo razdelimo na enostavna pod-območja ali pa (pri swept meshingu) določimo izhodiščno ploskev, na kateri je 2D mreža, ter izberemo smer generiranja heksaedričnih KE v prostor.
## 29. Kriterij za oceno kvalitete mreže 3D KE.
Kriteriji za oceno kvalitete mreže so enaki kot pri 2D mreži:
- razmerje med najdaljšo in najkrajšo stranico
- največji in najmanjši notranji kot na ploskvi, ki omejuje volumski KE
- oblikovni faktor (se računa le za tetraedrični KE)
	- $$1\geq f_\Delta=\frac{V_\Delta}{V_{\Delta id}}\geq0$$
	- $$f_{\Delta min}\geq0.5$$
- odstopanje ploskve KE od geometrije mreženega območja
## 30. Načini strukturiranega mreženja.
Pri mreženju 2D struktur moramo celotno območje razdeliti na pod-območja, ki imajo 3,4 ali 5 robov. Program lahko na takem območju naredi strukturirano mrežo z 4 kotnimi elementi. 

Pri mreženju volumskih modelov imamo 2 možnosti:

Ena možnost je da geometrijo razdelimo na pod-območja. Ta pod-območja ne smejo vsebovati lukenj, vrinjenih ploskev, robov in točk. Odstraniti moramo tudi vse nepotrebne elemente  - pomembnost priprave geometrije. 
Po temu ko smo območje razdelili na pod-območja določimo koliko elementov oz. vozlišč bo na ograjah (na robovih) med pod-območji. Lahko so razporejena enakomerno ali ne. Po temu ko smo to naredili lahko naredimo heksaedrično strukturirano mrežo. 

Drug način izdelave strukturirane mreže je sweep mesh. Na čelni ploskvi geometrije moramo narediti strukturirano mrežo - če želimo imeti heksaedrične KE moramo uporabiti štirikotne elemente. Nato izberemo število vozlišč na robovih čelne ploskve in število vozlišč v vzdolžni smeri. Nato lahko generiramo mrežo, ki ima po celotnem prerezu enako topologijo tj. število vozlišč in število elementov.

# Predavanje 5 - 16.3.2026
## 31. Določitev fizikalnih lastnosti materiala.

Fizikalne lastnosti problema nam poleg diferencialne enačbe, robnih pogojev in območja reševanja določajo lastnosti problema oz. sistema, ki ga hočemo rešiti.

Ko rešujemo reduciran problem - npr. upogib 3D konstrukcije v 1D moramo definirati dodatne materialne lastnosti, ki nam omogočajo, da upoštevamo lastnosti 3D geometrije v 1D.
## 32. Določitev geometrijskih lastnosti ploskovnih KE.
Ploskovnim elementom moramo določiti še debelino KE in pa normalo na površino KE.

## 33. Določitev geometrijskih lastnosti linijskih KE.

Linijskim elementom moramo definirati karakteristike prereza:
- ploščina prereza - $A$
- težiščni vztrajnostni momenti ploskve - $I_x, I_y$ in $I_{xy}$
- torzijski vztrajnostni moment - $I_t$

Definirati moramo tudi lego prereza glede na težiščnico.

## 34. Izpeljava šibke integralske enačbe za časovno ustaljen prostorski prevod toplote.

Najprej zapišemo enačbo za časovno ustaljen prevod toplote:
$$k\Delta T + q_v = 0$$
Prvi člen enačbe lahko zapišemo tudi preko Fourierovega zakona: $$q = -k\nabla \cdot T=-k\begin{Bmatrix}\frac{\partial}{\partial x}\\\frac{\partial}{\partial y}\\\frac{\partial}{\partial z}\end{Bmatrix}$$

Vodilno enačbo lahko zapišemo kot: $$-\nabla^Tq + q_v = 0$$
$$\begin{Bmatrix}\frac{\partial}{\partial x}\frac{\partial}{\partial y}\frac{\partial}{\partial z}\end{Bmatrix}(-k)\begin{Bmatrix}\frac{\partial T}{\partial x}\\\frac{\partial T}{\partial y}\\\frac{\partial T}{\partial z}\end{Bmatrix}+q_v = 0$$

Enačbo integriramo in pomnožimo z $v(x)$:$$\int_\Omega(-\nabla^Tq)v\space d\Omega + \int_\Omega q_vv\space d\Omega = 0$$
Osredotočimo se na izraz v prvem integralu in zapišimo sledeče: $$\nabla^T\cdot(q v) = (\nabla^T\cdot q)v + q^T(\nabla\cdot v)$$
$$-(\nabla^T\cdot q)v = -\nabla^T\cdot(qv) + q^T(\nabla \cdot v)$$
Izraz lahko vstavimo v integral in preko Gaussovega izreka dobimo:$$\begin{align}\int_\Omega(-\nabla^T\cdot q)v\space d\Omega =-\int_\Omega \nabla^T\cdot(qv)\space d\Omega + \int_\Omega q^T(\nabla\cdot v)\space d\Omega\\=-\int_\Gamma q^Tv\space n\space d\Gamma + \int_\Omega q^T(\nabla\cdot v)\space d\Omega\end{align}$$
Splošna enačba potem zgleda tako:$$\int_\Omega q^T(\nabla\cdot v)\space d\Omega - \int_\Gamma (q^Tn)v\space d\Gamma + \int_\Omega q_vv\space d\Omega = 0$$
Toplotni tok v prvem členu lahko zapišemo s Fourierovim zakonom $q^T = -k\nabla \cdot T$. Enačba se preoblikuje v: $$k\int_\Omega(\nabla\cdot T)(\nabla\cdot v)d\Omega = -\int_\Gamma q_n v \space d\Gamma+ \int_\Omega q_vv\space d\Omega $$
Enačbo lahko razpišemo po členih: $$k\int_\Omega \begin{Bmatrix}
\frac{\partial T}{\partial x}\frac{\partial v}{\partial x}+
\frac{\partial T}{\partial y}\frac{\partial v}{\partial y}+
\frac{\partial T}{\partial z}\frac{\partial v}{\partial z}+
\end{Bmatrix}d\Omega = -\int_\Gamma q_nv\space d\Gamma + \int_\Omega q_vv\space d\Omega$$
## 35. Interpolacija temperaturnega polja po območju prostorskega heksaedričnega KE.

Po območju KE se temperaturno polje interpolira preko oblikovnih funkcij:$$T(x,y,z) \approx\hat T(x,y,z) = \sum_{j=1}^{N_v}T_j\psi_j(x,y,z)$$
Vsota gre od 1 do števila vozlišč v končnem elementu (v primeru heksaedričnega KE je to vsaj 8 - KE ima vsaj 8 vozlišč).

## 36. Interpolacija geometrije v primeru izoparametričnega KE. 

Izoparametrični KE nam omogočajo, da popišemo bolj kompleksno geometrijo - izoparametrični elementi so lahko "nepravilne" oblike in lahko bolje popisujejo geometrijo.

Nepravilno obliko dobimo tako, da KE iz naravnega KS preslikamo v kartezični KS. To naredimo preko naslednjih funkcij:$$x=x(\tilde x, \tilde y, \tilde z) = \sum_{j=1}^{N_v}x_j\tilde \psi_j(\tilde x,\tilde y, \tilde z)$$
$$y = y(\tilde x,\tilde y, \tilde z) = \sum_{j=1}^{N_v}y_j\tilde\psi_j(\tilde x,\tilde y, \tilde z)$$
$$z = z(\tilde x,\tilde y, \tilde z) = \sum_{j=1}^{N_v}z_j\tilde\psi_j(\tilde x,\tilde y, \tilde z)$$

## 37. Razlika med Kartezijskim in naravnim koordinatnim sistemom.

Naravni koordinatni sistem je namišljen prostor, kjer je geometrija končnega elementa "pravilna", pravokotna. Koordinatni sistem je brez-dimenzijski (koordinate $(\tilde x,\tilde y, \tilde z)$ gredo običajno od -1 do +1), kar poenostavi numerično integriranje.

Za KE v naravnem koordinatnem sistemu lahko brez problema zapišemo funkcijo za interpolacijo primarne spremenljivke.

V kartezičnem koordinatnem sistemu je lahko KE poljubne oblike - zanj ne moremo napisati interpolacijskih funkcij. Zato rabimo interpolacijsko funkcijo preslikati iz naravnega v kartezični koordinatni sistem.
## 38. Kaj predstavlja Jacobijeva matrika?
Jacobijeva matrika predstavlja parcialne odvode kartezičnih koordinat $(x,y,z)$ po naravnih koordinatah $(\tilde x,\tilde y, \tilde z)$.  Predstavlja matematično transformacijo (preslikavo) med obema koordinatnima sistemoma in omogoča preračunavanje iz dejanske geometrije v referenčni naravni sistem elementa.
