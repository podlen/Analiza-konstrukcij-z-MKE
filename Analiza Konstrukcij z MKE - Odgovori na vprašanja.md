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

Ploskovnim elementom moramo določiti še debelino KE in normalo na površino KE.

## 33. Določitev geometrijskih lastnosti linijskih KE.

Linijskim elementom moramo definirati karakteristike prereza:
- ploščina prereza - $A$
- težiščni vztrajnostni momenti ploskve - $I_x, I_y$ in $I_{xy}$
- torzijski vztrajnostni moment - $I_t$

Definirati moramo tudi lego prereza glede na težiščnico - od te lege je so odvisni vztrajnostni momenti prereza.

Prav tako moramo definirati lego glavnih vztrajnostnih osi.

## 34. Izpeljava šibke integralske enačbe za časovno ustaljen prostorski prevod toplote.

Najprej zapišemo enačbo za časovno ustaljen prevod toplote:

$$k\Delta T + q_v = 0$$

Prvi člen enačbe lahko zapišemo tudi preko Fourierovega zakona:

$$\mathbf{q} = -k\nabla T = -k
\begin{Bmatrix}
\frac{\partial T}{\partial x}\\
\frac{\partial T}{\partial y}\\
\frac{\partial T}{\partial z}
\end{Bmatrix}$$

Vodilno enačbo lahko zapišemo kot:

$$-\nabla^T\cdot \mathbf{q} + q_v = 0$$

$$\begin{Bmatrix}\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z}\end{Bmatrix}(-k)\begin{Bmatrix}
\frac{\partial T}{\partial x}\\
\frac{\partial T}{\partial y}\\
\frac{\partial T}{\partial z}
\end{Bmatrix}+q_v = 0$$

Enačbo integriramo in pomnožimo z $v(x)$:

$$\int_\Omega(-\nabla^T\cdot \mathbf{q})\,v\, d\Omega + \int_\Omega q_v v\, d\Omega = 0$$

Osredotočimo se na izraz v prvem integralu in zapišemo sledeče:

---
*Pri produktnem pravilu z divergenco velja, da kadar delujemo na produkt vektorskega polja $\mathbf{q}$ in skalarne funkcije $v$, dobimo:

$$\nabla^T\cdot(\mathbf{q}\, v) = (\nabla^T\cdot \mathbf{q})\,v + \mathbf{q}^T(\nabla v)$$

*Drugi člen vsebuje $\nabla v$ in ne $\nabla \cdot v$, ker je $v$ skalarna funkcija — divergenca 
skalarја nima smisla. Operator $\nabla v$ predstavlja **gradient** skalarja $v$, ki vrne vektor parcialnih odvodov:*

$$\nabla v = \begin{Bmatrix}
\frac{\partial v}{\partial x}\\
\frac{\partial v}{\partial y}\\
\frac{\partial v}{\partial z}
\end{Bmatrix}$$

*S tem je skalarni produkt $\mathbf{q}^T(\nabla v)$ dimenzijsko skladen — gre za produkt dveh vektorjev*.

---
$$\nabla^T\cdot(\mathbf{q}\, v) = (\nabla^T\cdot \mathbf{q})\,v + \mathbf{q}^T(\nabla v)$$

$$-(\nabla^T\cdot \mathbf{q})\,v = -\nabla^T\cdot(\mathbf{q}\, v) + \mathbf{q}^T(\nabla v)$$

Izraz lahko vstavimo v integral in preko Gaussovega izreka dobimo:

$$\begin{align} \int_\Omega(-\nabla^T\cdot \mathbf{q})\,v\, d\Omega &= -\int_\Omega \nabla^T\cdot(\mathbf{q}\, v)\, d\Omega + \int_\Omega \mathbf{q}^T(\nabla v)\, d\Omega \\ &= -\int_\Gamma \mathbf{q}^T\mathbf{n}\, v\, d\Gamma + \int_\Omega \mathbf{q}^T(\nabla v)\, d\Omega \end{align}$$

Splošna enačba potem zgleda tako:

$$\int_\Omega \mathbf{q}^T(\nabla v)\, d\Omega - \int_\Gamma (\mathbf{q}^T\mathbf{n})\,v\, d\Gamma + \int_\Omega q_v v\, d\Omega = 0$$

Toplotni tok v prvem členu lahko zapišemo s Fourierovim zakonom $\mathbf{q}^T = (-k\nabla T)^T$. Enačba se preoblikuje v:

$$k\int_\Omega(\nabla T)^T(\nabla v)\,d\Omega = -\int_\Gamma q_n\, v\, d\Gamma + \int_\Omega q_v v\, d\Omega$$

Enačbo lahko razpišemo po členih:

$$k\int_\Omega \left(\frac{\partial T}{\partial x}\frac{\partial v}{\partial x} + \frac{\partial T}{\partial y}\frac{\partial v}{\partial y} + \frac{\partial T}{\partial z}\frac{\partial v}{\partial z}\right)d\Omega = -\int_\Gamma q_n\, v\, d\Gamma + \int_\Omega q_v v\, d\Omega$$

## 35. Interpolacija temperaturnega polja po območju prostorskega heksaedričnega KE.

Po območju KE se temperaturno polje interpolira preko oblikovnih funkcij:

$$T(x,y,z) \approx\hat T(x,y,z) = \sum_{j=1}^{N_v}T_j\psi_j(x,y,z)$$


Vsota gre od 1 do števila vozlišč v končnem elementu (v primeru heksaedričnega KE je to vsaj 8 - KE ima vsaj 8 vozlišč).

## 36. Interpolacija geometrije v primeru izoparametričnega KE. 

Izoparametrični KE nam omogočajo, da popišemo bolj kompleksno geometrijo - izoparametrični elementi so lahko "nepravilne" oblike in lahko bolje popisujejo geometrijo.

Nepravilno obliko dobimo tako, da KE iz naravnega KS preslikamo v kartezični KS. To naredimo preko naslednjih funkcij: 

$$x = x(\tilde x, \tilde y, \tilde z) = \sum_{j=1}^{N_v}x_j \tilde \psi_j( \tilde x, \tilde y, \tilde z)$$


$$y = y(\tilde x, \tilde y, \tilde z) = \sum_{j=1}^{N_v}y_j \tilde \psi_j (\tilde x, \tilde y, \tilde z)$$


$$z = z (\tilde x,\tilde y, \tilde z) = \sum_{j=1}^{N_v} z_j \tilde \psi_j ( \tilde x, \tilde y, \tilde z)$$


## 37. Razlika med Kartezijskim in naravnim koordinatnim sistemom.

Naravni koordinatni sistem je namišljen prostor, kjer je geometrija končnega elementa "pravilna", pravokotna. Koordinatni sistem je brez-dimenzijski (koordinate $(\tilde x,\tilde y, \tilde z)$ gredo običajno od -1 do +1), kar poenostavi numerično integriranje.

Za KE v naravnem koordinatnem sistemu lahko brez problema zapišemo funkcijo za interpolacijo primarne spremenljivke.

V kartezičnem koordinatnem sistemu je lahko KE poljubne oblike - zanj ne moremo napisati interpolacijskih funkcij. Zato rabimo interpolacijsko funkcijo preslikati iz naravnega v kartezični koordinatni sistem.

## 38. Kaj predstavlja Jacobijeva matrika?

Jacobijeva matrika predstavlja parcialne odvode kartezičnih koordinat $(x,y,z)$ po naravnih koordinatah $(\tilde x,\tilde y, \tilde z)$.  Predstavlja matematično transformacijo (preslikavo) med obema koordinatnima sistemoma in omogoča preračunavanje iz dejanske geometrije v referenčni naravni sistem elementa.


# Predavanje 6 - 23.3.2026

## 39. Katere zahteve mora izpolnjevati interpolacijska funkcija?

1. Polinomska funkcija z vsaj toliko monomi, kot je vozlišč KE.
2. Monomi morajo biti med seboj linearno neodvisni.
3. Zagotavljati mora zvezni prehod primarne spremenljivke preko meja KE (včasih tudi njenih odvodov).
4. Biti mora kompletna (enaka zastopanost vseh spremenljivk) oz. vsaj geometrijsko izotropna.

## 40. Določitev interpolacijske funkcije za določene KE

Za določitev interpolacijske funkcije gledamo Pascalov tetraeder monomov. Poskrbimo, da so polinomske funkcije kompletne in da imajo toliko neznanih koeficientov, kolikor je vozlišč v KE.

**4-vozliščni tetraedrični KE** ($N_v = 4$):

$$
\psi(x,y,z) = C_1 + C_2 x + C_3 y + C_4 z
$$

**8-vozliščni heksaedrični KE** ($N_v = 8$):

$$
\psi(x,y,z) = C_1 + C_2 x + C_3 y + C_4 z + C_5 xy + C_6 xz + C_7 yz + C_8 xyz
$$

**10-vozliščni tetraedrični KE** ($N_v = 10$):

$$
\psi(x,y,z) = C_1 + C_2 x + C_3 y + C_4 z + C_5 x^2 + C_6 y^2 + C_7 z^2 + C_8 xy + C_9 xz + C_{10} yz
$$

**20-vozliščni heksaedrični KE** ($N_v = 20$):

$$
\begin{aligned}
\psi(x,y,z) &= C_1 + C_2 x + C_3 y + C_4 z \\
&+ C_5 x^2 + C_6 y^2 + C_7 z^2 \\
&+ C_8 xy + C_9 xz + C_{10} yz + C_{11} xyz \\
&+ C_{12} x^2y + C_{13} xy^2 + C_{14} x^2z + C_{15} xz^2 \\
&+ C_{16} y^2z + C_{17} yz^2 + C_{18} x^2yz + C_{19} y^2xz + C_{20} z^2xy
\end{aligned}
$$

## 41. Matrični zapis sistema enačb za posamezni KE (ustaljeni prevod toplote)

Sistem enačb za posamezni KE:

$$
k[M]\{T\} = \{q\} + \{Q\}
$$

- $k$: toplotna prevodnost materiala
- $[M]$: matrika toplotne prevodnosti — **simetrična**, elementi so:

$$
M_{Ij} = \int_\Omega \left( \frac{\partial\psi_I}{\partial x}\frac{\partial\psi_j}{\partial x} + \frac{\partial\psi_I}{\partial y}\frac{\partial\psi_j}{\partial y} + \frac{\partial\psi_I}{\partial z}\frac{\partial\psi_j}{\partial z} \right) d\Omega = M_{jI}
$$

- $\{T\}$: vektor temperatur v vozliščih (primarna neznanka)
- $\{q\}$: vektor toplotnih tokov skozi površino KE:

$$
q_I = -\int_\Gamma[q_x n_x + q_y n_y + q_z n_z]\, \psi_I\, d\Gamma
$$

- $\{Q\}$: vektor ekvivalentnih vozliščnih vrednosti izvora/ponora toplote:

$$
Q_I = \int_\Omega Q_V\, \psi_I\, d\Omega
$$

## 42. Kako pri integriranju po volumnu KE preidemo iz Kartezijevega koordinatnega sistema v naravni koordinatni sistem?

Izhajamo iz zapisa krajevnega vektorja $\vec{r} = x\vec{e}_x + y\vec{e}_y + z\vec{e}_z$ in definiramo bazne vektorje:

$$
\vec{a} = \frac{\partial\vec{r}}{\partial\tilde{x}}d\tilde{x}, \quad \vec{b} = \frac{\partial\vec{r}}{\partial\tilde{y}}d\tilde{y}, \quad \vec{c} = \frac{\partial\vec{r}}{\partial\tilde{z}}d\tilde{z}
$$

Diferencial volumna postane mešani produkt:

$$
\begin{aligned}
d\Omega &= \vec{a}(\vec{b}\times\vec{c}) \\
&= \begin{vmatrix} 
\frac{\partial x}{\partial\tilde{x}} & \frac{\partial y}{\partial\tilde{x}} & \frac{\partial z}{\partial\tilde{x}}\\
\frac{\partial x}{\partial\tilde{y}} & \frac{\partial y}{\partial\tilde{y}} & \frac{\partial z}{\partial\tilde{y}}\\ 
\frac{\partial x}{\partial\tilde{z}} & \frac{\partial y}{\partial\tilde{z}} & \frac{\partial z}{\partial\tilde{z}}
\end{vmatrix} d\tilde{x}\,d\tilde{y}\,d\tilde{z} \\
&= |J|\,d\tilde{x}\,d\tilde{y}\,d\tilde{z} = |J|\,d\tilde\Omega
\end{aligned}
$$

Jakobijeva matrika je odvisna le od koordinat vozlišč v kartezijskem KS. Za heksaedrični element so meje integracije od $-1$ do $+1$ v vsaki smeri.

## 43. Prehod iz Kartezijevega v naravni KS pri integriranju po površini

Diferencial površine je dolžina vektorskega produkta vektorjev ploskve:

$$
d\Gamma = |\vec{a}\times\vec{b}| = 
\begin{vmatrix} 
\vec{e}_x & \vec{e}_y & \vec{e}_z \\ 
\frac{\partial x}{\partial\tilde{x}} & \frac{\partial y}{\partial\tilde{x}} & \frac{\partial z}{\partial\tilde{x}} \\ 
\frac{\partial x}{\partial\tilde{y}} & \frac{\partial y}{\partial\tilde{y}} & \frac{\partial z}{\partial\tilde{y}} 
\end{vmatrix} 
d\tilde{x}\,d\tilde{y} = |j|\,d\tilde{x}\,d\tilde{y} = |j|\,d\tilde\Gamma
$$

Meje integracije v naravnem KS so od $-1$ do $+1$.

## 44. Gaussovo numerično integriranje po eni spremenljivki

Gaussova integracijska formula pretvori integral s poljubnimi mejami na integral od $-1$ do $+1$, ki ga aproksimiramo z uteženo vsoto funkcijskih vrednosti v izbranih točkah:

$$
I = \int_{x_{sp}}^{x_{zg}} f(x)\,dx = \int_{-1}^{+1}\tilde{f}(\tilde{x})\,d\tilde{x} \approx \sum_{i=1}^m w_i\,\tilde{f}(\tilde{x}_i)
$$

Uteži $w_i$ in položaje točk $\tilde{x}_i$ določimo z analitičnim integralom splošnega polinoma stopnje $n$. Ker lihe potence $\tilde{x}$ pri integraciji od $-1$ do $+1$ prispevajo nič, integral vsebuje le sode člene:

$$
I = 2a_0 + \frac{2}{3}a_2 + \frac{2}{5}a_4 + \cdots + \frac{2}{2k+1}a_{2k}
$$

Z izenačenjem aproksimacije z analitičnim rezultatom dobimo sistem (nelinearnih) enačb, ki določi optimalne pare $(w_i, \tilde{x}_i)$. Ti so vnaprej tabelirani in zagotavljajo točen rezultat za polinome stopnje do $2m-1$, kjer je $m$ število integracijskih točk.

## 45. Numerično integriranje po več spremenljivkah z Gaussovo formulo

Gaussovo formulo razširimo z večkratnimi vsotami. Za **2D** območje:

$$
I = \int_{-1}^{+1}\int_{-1}^{+1}\tilde{f}(\tilde{x},\tilde{y})\,d\tilde{x}\,d\tilde{y} \approx \sum_{j=1}^m\sum_{i=1}^m w_j\,w_i\,\tilde{f}(\tilde{x}_i,\tilde{y}_j)
$$

Za **3D** območje:

$$
I = \int_{-1}^{+1}\int_{-1}^{+1}\int_{-1}^{+1}\tilde{f}(\tilde{x},\tilde{y},\tilde{z})\,d\tilde{x}\,d\tilde{y}\,d\tilde{z} \approx \sum_{k=1}^m\sum_{j=1}^m\sum_{i=1}^m w_k\,w_j\,w_i\,\tilde{f}(\tilde{x}_i,\tilde{y}_j,\tilde{z}_k)
$$

## 46. Numerično integriranje po trikotnem ali tetraedričnem območju

Gaussovo formulo prilagodimo za trikotno/tetraedrično obliko s pomočjo **površinskih** oz. **volumskih koordinat** ($\Lambda$).

**Trikotno območje** ($\Gamma \equiv A_{IJK}$):

$$
I = \int_\Gamma f(x,y)\,d\Gamma \approx A_{IJK}\sum_{i=1}^m w_i\,\tilde{f}(\Lambda_{Ii}, \Lambda_{Ji}, \Lambda_{Ki})
$$

**Tetraedrično območje** ($\Omega \equiv V_{1234}$):

$$
I = \int_\Omega f(x,y,z)\,d\Omega \approx V_{1234}\sum_{i=1}^m w_i\,\tilde{f}(\Lambda_{1i},\Lambda_{2i},\Lambda_{3i},\Lambda_{4i})
$$

Uteži in koordinate integracijskih točk so vnaprej tabelirane za različno število točk $m$.

## 47. Izračun integrala po volumnu z volumskimi koordinatami

Kadar pod integralom nastopajo volumske koordinate, lahko integral izračunamo **analitično**: 

$$
\int_\Omega (\Lambda_1)^r(\Lambda_2)^p(\Lambda_3)^s(\Lambda_4)^t\,d\Omega = (6\Omega)\frac{r!\,p!\,s!\,t!}{(r+p+s+t+3)!}, \quad 0! = 1
$$

Za integral po trikotni površini:

$$
\int_\Gamma (\Lambda_I)^r(\Lambda_K)^p(\Lambda_L)^s\,d\Gamma = (2\Gamma)\frac{r!\,p!\,s!}{(r+p+s+2)!}
$$

Volumen tetraedra izračunamo iz determinante:

$$
\Omega = V_{1234} = \frac{1}{6}
\begin{vmatrix} 
1 & x_1 & y_1 & z_1 \\ 
1 & x_2 & y_2 & z_2 \\ 
1 & x_3 & y_3 & z_3 \\ 
1 & x_4 & y_4 & z_4 
\end{vmatrix}
$$

## 48. Kako pridemo do sistema linearnih enačb za posamezni KE?

**1.** Zapišemo šibko (integralsko) formulacijo fizikalnega problema.
**2.** Po **Galerkinovi metodi** izberemo testne funkcije $v = \psi_I(x,y,z)$.
**3.** Primarno spremenljivko po elementu aproksimiramo z interpolacijskimi funkcijami: $T \approx \hat{T} = \sum_{j=1}^{N_v} T_j\,\psi_j(x,y,z)$
**4.** Aproksimacijo vstavimo v integralsko enačbo in izpeljemo:

$$
k[M]\{T\} = \{q\} + \{Q\}, \quad I = 1,\ldots,N_v
$$

**5.** Integrale po volumnu in površini izračunamo numerično (Gaussova formula) ali analitično (volumske koordinate).

## 49. Kako pridemo do sistema linearnih enačb za celotno območje?

**1.** Za vsak posamezni KE sestavimo lokalni sistem enačb ($N_v \times N_v$ matrika).
**2.** Vsako lokalno matriko **razširimo** na dimenzijo globalnega sistema (vrstice/stolpci vozlišč, ki ne pripadajo elementu, dobijo vrednost 0).
**3.** Vse razširjene matrike in vektorje **seštejemo** (superpozicija):

$$
k[M_k]\{T\} = \{q_q\} + \{q_Q\}
$$

kjer so skupni elementi matrike vsota prispevkov vseh elementov, ki si delijo isto vozlišče:
   
$$
M_{ij}^{(skupni)} = M_{ij}^{(1)} + M_{ij}^{(2)} + \cdots
$$

**4.** Upoštevamo robne pogoje (predpisane temperature ali tokovi) in rešimo globalni sistem enačb za neznane temperature $\{T\}$.

# Predavanje 7 - 31.3.2026
## 50. Zakaj se ne izračunava integralov po površini, ki je skupna dvema končnima elementoma?

Ker na skupni površini sosednjih elementov velja zakon o ohranitvi toplotnega toka, kar pomeni, da je iztekajoči tok iz prvega elementa enak pritekajočemu toku v drugi element ($q_n^{(1)} = -q_n^{(2)}$). Pri sestavljanju globalnega sistema enačb se prispevki teh integralov v vozliščih med seboj izničijo ($\{q^{(1)}\} + \{q^{(2)}\} = 0$), zato se integrali izračunavajo le po zunanjih (prostih) površinah območja.

## 51. Kako je v izračunu z MKE upoštevan konvektivni robni pogoj prestopa toplote na površini območja?

$$q = h(T_{stena}  -T_{okoloca})$$


Konvektivni robni pogoj se upošteva preko površinskega integrala, ki se razdeli na dva dela:
1.  Del, ki je odvisen od neznanih temperatur vozlišč $\{T\}$, tvori **matriko prestopnosti** $[M_h]$, ki se prišteje k prevodnostni matriki $[M]$.

2.  Del, ki je odvisen od znane temperature okolice $T_{zrak}$, tvori **vektor ekvivalentnih vozliščnih toplotnih virov** $\{q_q\}$, ki se prišteje na desno stran sistema enačb.

## 52. Kako je v izračunu z MKE upoštevan robni pogoj prestopa toplote s sevanjem na površini območja?

Sevanje se upošteva podobno kot konvekcija, vendar je zaradi četrte potence temperature v enačbi  $q_s = \sigma \varepsilon (T^4 - T_0^4)$  ta robni pogoj **nelinearen**. 

V MKE se to običajno rešuje z uvedbo nadomestne (linearizirane) toplotne prestopnosti za sevanje:

$$T^4 - T_{\infty}^4 = (T^2-T_{\infty}^2)(T^2 + T_{\infty}^2)$$

$$T^2 - T_{\infty}^2 = (T-T_{\infty})(T+T_{\infty})$$



Vzamemo člen $(T-T_{\infty})$, ostale člene pa združimo v koeficient, ki ga iterativno izračunamo. Formula za toplotni tok zaradi sevanja je torej:

$$q_{s} = \sigma\varepsilon c(T - T_{\infty})$$

kjer je $c = (T+T_{\infty})(T^2 + T_{\infty}^2)$.

## 53. Primerjaj metode za reševanje sistema linearnih enačb.

Metode delimo na direktne in iterativne:

*   **Direktne metode** (Gaussova eliminacija s pivotiranjem, razcep LU ali Choleskega):
    *   **Prednosti:** So numerično stabilne in dajo natančno rešitev v končnem številu korakov.
    *   **Slabosti:** Čas reševanja s številom enačb narašča potenčno (eksponentna krivulja na grafu), zahtevajo veliko delovnega pomnilnika.
*   **Iterativne metode** (Gauss-Seidlova, Gauss-Jacobijeva metoda, metoda konjugiranih gradientov):
    *   **Prednosti:** Čas reševanja narašča približno linearno s številom enačb. Porabijo manj pomnilnika.
    *   **Slabosti:** Potrebujejo konvergenčni kriterij in niso vedno stabilne.
*   **Povzetek:** Za manjše sisteme so boljše direktne metode, pri velikih sistemih (nad $10^6$ enačb) pa so zaradi hitrosti in pomnilniške učinkovitosti bolj smiselne iterativne metode.

# Predavanje 8 - 13.4.2026
## 54. Izhodiščna enačba za reševanje statičnega 3D mehanskega problema z MKE.

Fizikalno izhodišče so diferencialne enačbe ravnotežja, ki pa jih za reševanje z MKE preoblikujemo v šibko obliko. Ta uravnoteži notranje napetosti z zunanjimi površinskimi in volumskimi obremenitvami:

$$ \int_\Omega \{\delta v\}^T \{\sigma\} d\Omega = \int_\Gamma \{\delta v\}^T \{p\} d\Gamma + \int_\Omega \{\delta v\}^T \rho \{a\} d\Omega $$

## 55. Kako je izbrana poljubna funkcija $v$ v primeru 3D KE za reševanje mehanskega problema?

V skladu z Galerkinovo metodo so $v$ enake kot oblikovne funkcije $[N]$. V primeru 3D mehanskega problema so pomnožene še s poljubno vozliščno vrednostjo $\Upsilon$. 

$$ \{v\} = [N]\{\Upsilon\} \quad \text{in} \quad \{\delta v\} = [L][N]\{\Upsilon\} $$


## 56. Katere so primarne neznanke pri reševanju 3D mehanskih problemov?


Primarne neznanke so pomiki v vozliščih (ali pa reakcijske sile). V 3D prostoru ima vsako vozlišče 3 translacijske prostostne stopnje:


$$ \{U\} = \{U_x, U_y, U_z\}^T $$

## 57. Kako se izračunajo komponente napetostnega tenzorja?


Izračunajo se v **integracijskih točkah** preko reološkega (Hookovega) zakona, ki deformacije pomnoži z materialno matriko $[E]$. Deformacije pa dobimo iz odvodov vozliščnih pomikov:


$$ \{\sigma\}_e = [E]\{\varepsilon\}_e = [E] ([L][N]) \{U\}_e $$

## 58. Kaj predstavlja vrednost in predznak komponente vektorja pomika?


Vrednost pove, za koliko dolžinskih enot se je vozlišče premaknilo glede na neobremenjeno stanje. Predznak določa smer premika vzdolž osi ($x, y$ ali $z$) globalnega koordinatnega sistema.

## 59. Kaj predstavlja vrednost in predznak normalne komponente deformacijskega tenzorja?


Predstavlja linearno deformacijo (razteg) materialnega delca vzdolž osi. Pozitiven predznak (+) pomeni **razteg**, negativen (-) pa **skrček**.
$$ \varepsilon_{xx} = \frac{\partial u_x}{\partial x} $$


## 60. Kaj predstavlja vrednost in predznak normalne komponente napetostnega tenzorja?


Predstavlja velikost normalne obremenitve na prerez. Pozitiven predznak (+) pomeni natezno napetost, negativen (-) pa tlačno napetost.

## 61. Kako je definirana strižna komponenta deformacijskega tenzorja?


Strižne deformacije predstavljajo spremembo pravega kota v materialnem delcu. Zapisane so s pomočjo parcialnih odvodov pomikov pravokotno na koordinatne osi:

$$ \varepsilon_{xy} = \frac{1}{2} \left( \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x} \right) $$

## 62. Kako preverimo ali je obremenitev mehansko obremenjene komponente v dopustnih vrednostih?

Kompleksno 3D napetostno stanje pretvorimo v eno **primerjalno napetost**, ki jo primerjamo z dopustno mejo materiala. Najpogosteje uporabimo Von Misesovo primerjalno napetost, ki je vedno pozitivna:


$$ \sigma_{ekv}^{\text{Mises}} = \sqrt{0.5 \left[ (\sigma_1-\sigma_2)^2 + (\sigma_1-\sigma_3)^2 + (\sigma_2-\sigma_3)^2 \right]} $$

## 64. Kako so definirane komponente deformacijskega tenzorja v cilindričnem koordinatnem sistemu?


Normalne komponente opisujejo razteg v smereh $r, z, \varphi$:


$$ \varepsilon_{rr} = \frac{\partial u_r}{\partial r}, \quad \varepsilon_{zz} = \frac{\partial u_z}{\partial z}, \quad \varepsilon_{\varphi\varphi} = \frac{u_r}{r} + \frac{1}{r}\frac{\partial u_\varphi}{\partial \varphi} $$


Strižne komponente vsebujejo dodatne člene ($1/r$) zaradi ukrivljenosti sistema:


$$ \varepsilon_{r\varphi} = \frac{1}{2} \left( \frac{1}{r} \frac{\partial u_r}{\partial \varphi} + \frac{\partial u_\varphi}{\partial r} - \frac{u_\varphi}{r} \right) $$

## 65. Katere mehanske veličine se v primeru uporabe 3D KE izračunavajo v vozliščih in katere v integracijskih točkah posameznega KE?


*   **Vozlišča:** primarne neznanke – pomiki ($\{U\}$) in ekvivalentne sile ($\{F\}$).

*   **Integracijske točke:** sekundarne neznanke – deformacije ($\{\varepsilon\}$) in napetosti ($\{\sigma\}$).

## 66. Vloga globalnega koordinatnega sistema.
Omogoča rotacijo vseh poljubno zasukanih elementov v skupen referenčni sistem in sestavljanje sistema enačb celotnega problema:


$$ [K]\{U\} = \{F\} $$


V njem se definirajo tudi vsi robni pogoji in obremenitve.

## 67. Kako je zajet vpliv lastne teže v primeru uporabe 3D KE?


Zajet je kot volumska obremenitev. Teža (gostota $\rho$ $\times$ pospešek $a$) se integrira preko volumna elementa in s pomočjo interpolacijskih funkcij $[N]$ pretvori v ekvivalentne vozliščne sile:


$$ \{F_v\}_e = \int_{\Omega_e} \rho \cdot a_k [N]^T d\Omega $$