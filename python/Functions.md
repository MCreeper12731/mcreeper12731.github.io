# Python - Funkcije
## Uvod
Pri programiranju pogosto pride do ponavljanja kode. Zgodi se, da potrebujemo isti postopek izvesti na večih mestih. Da se izognemu podvajanju, lahko tak del kode preoblikujemo v **funkcijo**.
```python
def pozdrav(ime):
	print(f"Pozdravljen, {ime}!")

pozdrav("Martin")
pozdrav("Luka")
```
```lua
Pozdravljen, Martin!
Pozdravljen, Luka!
```
*primer funkcije, ki imenu* `ime` *doda pozdrav in ga izpiše*

Funkcije definiramo z besedo `def`, za tem pa njeno ime. Po imenu sledijo oklepaji, v katere lahko navedemo morebitne **parametre**. Parametri delujejo podobno kot spremenljivke - hranijo tiste vrednosti, ki jih funkciji podamo ob njenem **klicu**. Funkcija se sama od sebe ne bo izvedla - izvedla se bo le, ko jo pokličemo. Pokličemo jo s tem, da navedemo ime funkcije s parom oklepajev, med njimi pa navedemo vse morebitne parametre.

Preprost primer klica funkcije je nadvse znan `print()`. S klicom te funkcije na zaslon izpišemo katerokoli vrednost smo navedli med oklepaji.
```python
print("Hello, World!")
```
```lua
Hello, World!
```
*primer uporabe funkcije **print** s parametrom* `"Hello, World!"`

### Primer pisanja lastnih funkcij
Uzemimo za primer [prejšnji sklop nalog](https://github.com/MCreeper12731/ds-ucni-nacrti/blob/main/python/Dictionaries.md), kjer bomo posamezne naloge pretvorili v funkcije.
Prva naloga je enaka:
```python
izdelki = {
	'ananas': 2.5,
	'banana': 1.1,
	'grozdje': 1.7,
	'jagode': 3.1,
	'borovnice': 1.7
}
```
Drugo (dodatno) nalogo bomo pretvorili v funkcijo. Na tem mestu se vprašajmo, katere vrednosti lahko funkciji podamo kot parameter. Prva možnost je, da funkciji podamo koliko novih izdelkov želimo dodati:
```python
def dodaj_izdelke(stevilo_izdelkov):
	...
```
Klic funkcije bi v tem primeru izgledal tako:
```python
stevilo_izdelkov = int(input("Koliko novih izdelkov? "))
dodaj_izdelke(stevilo_izdelkov)
```
Ta način še vedno zahteva branja podatkov pred funkcijo. Tega se pri uporabi funkcij želimo izogniti, razen če vemo, da bomo nek podatek potrebovali še naprej. V tem primeru, zelo verjetno `stevilo_izdelkov` ne bomo potrebovali nikjer drugje, zato lahko ta del premaknemo v funkcijo. Funkcija tako ne bo imela nobenih parametrov:
```python
def dodaj_izdelke():
	stevilo_izdelkov = int(input("Koliko novih izdelkov? "))
	for i in range(stevilo_izdelkov):
	    ime = input("Vnesi nov izdelek: ")
	    izdelki[ime] = float(input("Vnesi ceno: "))
```
Nadaljujemo s tretjo (dodatno) nalogo. Že v prvotni rešitvi ni bilo potrebe po prebiranju novih podatkov, tako da možnosti za parametre prav tako ni.
```python
def najdrazji_izdelki():
	most_expensive = []
	for izdelek, cena in izdelki.items():
	    if (len(most_expensive) == 0):
	        most_expensive.append(izdelek) # Ce je seznam prazen, dodamo element
	    elif cena > izdelki[most_expensive[0]]:
	        most_expensive = [izdelek] # Ce je trenutna cena višja, seznam prepišemo s trenutnim izdelkom
	    elif cena == izdelki[most_expensive[0]]:
	        most_expensive.append(izdelek) # Ce je trenutna cena enaka, izdelek dodamo
	return most_expensive
```
V tem primeru se pojavi nov stavek `return`. S tem stavkom lahko iz funkcije vrnemo poljubno vrednost. Zakaj je to uporabno? Spremenljivke v funkcijah imajo omejen dostop. To pomeni, da so spremenljivke, definirane znotraj funkcije, dostopne le znotraj te funkcije:
```python
def test():
	a = 10
	print(a)

test() # 10
print(a) # Napaka: name 'a' is not defined
```
S stavkom return lahko na tak način vrnemo izbrane vrednosti spremenljivk. Funkcijo, ki vrača vrednost, preberemo tako:
```python
izdelek = nadrazji_izdelek()
print(izdelek) # Najdražji izdelek v slovarju
```
Naredimo še primer za peto nalogo, kjer vse izdelke podražimo za določen faktor. Tukaj se odločimo, da bomo faktor podražitve funkciji poslali kot paramater:
```python
def podrazi(faktor):
	for izdelek, cena in izdelki.items():
    izdelki[izdelek] = cena * faktor 
```
Funkcijo bomo uporabili tako, da ji bomo poslali fiksno vrednost:
```python
podrazi(5) # Vsi izdelki bojo 5x dražji
```
Opazimo tudi, da ne vračamo ničesar, saj v tem primeru le spreminjamo slovar izdelkov. Prav tako opazimo, da je slovar `izdelki` dostopen znotraj funkcije, kljub temu da te spremenljivke nismo definirali znotraj funkcije. Tukaj nastopi pojem **globalnih spremenljivk**. To so vse spremenljivke, ki so definirane izven kakršnekoli funkcije. Te spremenljivke so dostopne kjerkoli v programu, tudi v funkcijah:
```python
a = 10
def test():
	print(a)

test() # 10
```
## Naloge
V tem sklopu nalog bomo zgradili komponente popularne igre s kartami - enka (UNO).
### 1. Naloga - Ustvarjanje kompleta kart
Preden lahko karkoli počnemo, potrebujemo komplet kart. Karte bomo predstavili s seznamom `string`ov, kjer je karta oblike '[barva] [številka]' (izločimo črne in posebne karte - `rdeca 2` je v kompletu vključena, karta `+4` pa ne). To bo naš komplet kart.<br>**Primer**
```python
komplet_kart = ...
print(komplet_kart)
```
```lua
['zelena 0', 'zelena 1', 'zelena 2', 'zelena 3', 'zelena 4', 'zelena 5', 'zelena 6', 'modra 0', 'modra 1', 'modra 2', 'modra 3', 'modra 4', 'modra 5', 'modra 6', 'rdeca 0', 'rdeca 1', 'rdeca 2', 'rdeca 3', 'rdeca 4', 'rdeca 5', 'rdeca 6', 'rumena 0', 'rumena 1', 'rumena 2', 'rumena 3', 'rumena 4', 'rumena 5', 'rumena 6']
```
### 2. Naloga - Mešanje kart
Brez mešanja kart bi vsaka igra potekala enako. Komplet kart, ki smo ga ustvarili, premešajte. *Namig:* `random.shuffle(seznam)` *naključno zamenja vrstni red elementov v seznamu.*<br>**Primer**
```python
komplet_kart = ...
print(komplet_kart)
```
```lua
['rdeca 6', 'modra 0', 'rumena 6', 'rdeca 0', 'rumena 1', 'rdeca 5', 'modra 2', 'zelena 0', 'zelena 6', 'zelena 4', 'rdeca 1', 'zelena 3', 'modra 6', 'rumena 0', 'rumena 3', 'rdeca 2', 'rumena 5', 'modra 3', 'rdeca 3', 'modra 4', 'zelena 5', 'modra 5', 'zelena 1', 'rumena 4', 'rdeca 4', 'modra 1', 'zelena 2', 'rumena 2']
```
### 3. Naloga - Deljenje kart
Za igro vsak igralec potrebuje karte. Napišite funkcijo, ki kot parameter prejme **komplet** in **število kart**, ki jih razdeli igralcu in vrne **razdeljene karte**. Razdeljene karte naj bojo odstranjene iz kompleta kart. *Namig:* `seznam.pop()` *odstrani in vrne zadnji element seznama.*<br>**Primer**
```python
igralec1 = razdeli(komplet_kart, 6)
igralec2 = razdeli(komplet_kart, 4)
print(igralec1)
print(igralec2)
```
```lua
['rumena 2', 'zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
['modra 5', 'zelena 5', 'modra 4', 'rdeca 3']
```
### 4. Naloga - Začetek igre
Igra se začne s tem, da iz kupčka vzamemo prvo karto. Ustvarite spremenljivko, ki bo hranila zadnjo igrano karto, začne pa s prvo karto iz kupčka.<br>**Primer**
```python
zadnja_karta = ...
print(zadnja_karta)
```
```lua
modra 3
```
### 5. Naloga - Kupovanje kart
Najpomembnejši del enke - koliko kart lahko nabereš preden tvoj prijatelj zmaga. Napišite funkcijo, ki kot paramater prejme **število kart, ki jih igralec kupi**, **igralčeve karte** in **kupček kart**. Funkcija naj igralčevim kartam doda toliko kart, kot je bilo podano preko parametra.<br>**Primer**
```python
kupi(2, igralec2, komplet_kart)
print(igralec2)
```
```lua
['modra 5', 'zelena 5', 'modra 4', 'rdeca 3', 'rumena 5', 'rdeca 2']
```

### 6. Naloga - Igranje kart
Eden izmed osrednjih elementov - odmetavanje kart. Ustvarite funkcijo, ki kot paramater prejme **igralčeve karte**. Igralcu naj funkcija izpiše njegove karte, nato pa naj z uporabo funkcije `input()` prebere željeno potezo. Če karta ni v igralčevi roki, naj program še enkrat vpraša po karti. Če pa je, naj se karta odstrani iz igralčeve roke in funkcija vrne **igrano karto**. Na tem mestu nas še ne zanima, če je poteza veljavna. *Namig:* `seznam.remove(element)` *odstrani poljuben element; kombinacija* `while True` *in* `break` *stavka omogoči neskončno izvajanje zanke, dokler ne izpolnimo nekega pogoja.*<br>**Primer**
```python
zadnja_karta = igraj_karto(igralec1)
print(f"Zadnja igrana karta: {zadnja_karta}")
print(f"Karte igralca: {igralec1}")
```
```lua
Trenutne karte: ['rumena 2', 'zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
Vnesi potezo: rumena 3
Karte ni v roki!
Trenutne karte: ['rumena 2', 'zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
Vnesi potezo: rumena 2
Zadnja igrana karta: rumena 2
Karte igralca: ['zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
```

### 7. Naloga - Veljavne poteze
Vsako potezo lahko igralec igra katerokoli karto, ki ima enako barvo ali številko (ali oboje). Napišite funkcijo, ki kot paramatere prejme **zadnjo igrano karto** in **igralčeve karte**. Vrne naj **vse veljavne poteze**. *Namig:* `string.split()` *loči besedo po presledkih (ali drugih znakih).* <br>**Primer**
```python
poteze1 = veljavne_poteze(zadnja_karta, igralec1)
poteze2 = veljavne_poteze(zadnja_karta, igralec2)
print(poteze1)
print(poteze2)
```
```lua
['modra 1']
['modra 5', 'modra 4', 'rdeca 3']
```

### 8. Naloga - Igranje veljavnih kart
Dopolnite funkcijo `igraj_karto()` iz 6. naloge tako, da igralec lahko igra le veljavne poteze. Program naj napiše, če je igralec igral neveljavno karto. Igralec naj ima tudi na voljo potezo 'kupi', da kupi karto.
```python
zadnja_karta = igraj_karto(igralec1)
print(f"Zadnja igrana karta: {zadnja_karta}")
print(f"Karte igralca: {igralec1}")
```
```lua
Trenutne karte: ['rumena 2', 'zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
Vnesi potezo: rumena 2
Poteza ni veljavna!
Trenutne karte: ['rumena 2', 'zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
Vnesi potezo: modra 1
Zadnja igrana karta: rumena 2
Karte igralca: ['zelena 2', 'modra 1', 'rdeca 4', 'rumena 4', 'zelena 1']
```
