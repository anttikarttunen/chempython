---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
# if-elif-else -ehtolauseet ja vertailuoperaattorit
if-ehtolauseen avulla ohjataan ohjelman suoritusta haluttuun suuntaan. if-ehtolauseen lyhyempi muoto on **if-else**:
``` ipython3
if EHTO:
    jos EHTO toteutuu, suoritetaan tässä sisennetty koodi
else:
    jos EHTO ei toteudu, suoritetaan tässä sisennetty koodi
```
if-ehtolauseen pidempi muoto on **if-elif-else**:
``` ipython3
if EHTO1:
    jos EHTO1 toteutuu, suoritetaan tässä sisennetty koodi
elif EHTO2:
    jos EHTO1 ei toteudu, mutta EHTO2 toteutuu, suoritetaan tässä sisennetty koodi
else:
    jos EHTO1 tai EHTO2 ei toteudu, suoritetaan tässä sisennetty koodi
```
:::{admonition} Huom! Sisennykset
:class: note
Pythonissa sisennykset ovat tärkeässä roolissa ja yllä olevat ehtolauseet eivät toimi, jos niitä ei ole sisennetty oikein.
:::
Käydään ensin läpi ehtolauseissa käytettyjä vertailuoperaattoreita, jonka jälkeen siirrytään käytännön esimerkkeihin.
## Vertailuoperaattorit
Ehtolauseissa käytetään hyvin usein vertailuoperaattoreita:
| Operaattori | Vertailuoperaattorin merkitys | Esimerkkejä ehtolauseessa |
| :---: | :---: | :---:|
| == | Yhtä suuri kuin | if numero == 1000:  TAI  if nimi == "Tytti": |
| != | Erisuuri kuin | if hinta != 10:  TAI  if vierailija != "Loiri": |
| > | Suurempi kuin | if massa > 55.5: |
| < | Pienempi kuin | if lampotila < 0.0: |
| >= | Suurempi tai yhtä suuri kuin | if paine >= 32: |
| <= | Pienempi tai yhtä suuri kuin | if tilavuus <= 24: |
## if-else
Tarkastellaan esimerkkiohjelmaa:
``` ipython3
luku = int(input("Anna kokonaisluku:\n"))
if luku >= 0:
    print("Antamasi luku on suurempi tai yhtä suuri kuin nolla")
else:
    print("Antamasi luku on pienempi kuin nolla")
```
Esimerkkisuoritus:
```
Anna kokonaisluku:
> 5
Antamasi luku on suurempi tai yhtä suuri kuin nolla
```
Toinen esimerkkisuoritus eri syötteellä:
```
Anna kokonaisluku:
> -222
Antamasi luku on pienempi kuin nolla
```

Esimerkki, jossa selvitetään kokonaislukujen jaollisuutta jakojäännösoperaattorin `%` avulla:
``` ipython3
luku = int(input("Anna kokonaisluku:\n"))
jakaja = int(input("Anna jakaja (kokonaisluku):\n"))
if luku % jakaja == 0:
    print("Luku", luku, "on jaollinen luvulla", jakaja)
else:
    print("Luku", luku, "ei ole jaollinen luvulla", jakaja)
```
Esimerkkisuoritus:
```
Anna kokonaisluku:
> 48
Anna jakaja (kokonaisluku) :
> 8
Luku 48 on jaollinen luvulla 8
```

if-ehtolauseita voi olla useita sisäkkäin. Huomaa sisennysten käyttö tässä esimerkkiohjelmassa:
``` ipython3
luku = int(input("Anna kokonaisluku:\n"))
if luku >= 0:
    print("Antamasi luku on suurempi tai yhtä suuri kuin nolla")
    if luku > 1000:
        print("Se on jopa suurempi kuin 1000")
    else:
        print("Se on kuitenkin enintään 1000")
else:
    print("Antamasi luku on pienempi kuin nolla")
```
Esimerkkisuoritus:
```
Anna kokonaisluku:
> 999
Antamasi luku on suurempi tai yhtä suuri kuin nolla
Se on kuitenkin enintään 1000
```
:::{admonition} Vinkki
:class: tip
Ensimmäinen ehto `luku >= 0` siis toteutui, mutta ensimmäisen ehtolauseen sisällä oleva ehto `luku > 1000` ei toteutunut.
:::

## if-elif-else
Ehtolauseeseen voi myös lisätä mielivaltaisen määrän lisäehtoja elif-käskyllä:
``` ipython3
luku = int(input("Anna kokonaisluku: "))
if luku > 1000:
    print("Antamasi luku on suurempi kuin tuhat")
elif luku > 100:
    print("Antamasi luku on suurempi kuin sata")
elif luku > 10:
    print("Antamasi luku on suurempi kuin kymmenen")
elif luku >= 0:
    print("Antamasi luku on välillä 0..10")
else:
    print("Antamasi luku on pienempi kuin nolla")
```
else-osio ei ole pakollinen:
``` ipython3
kuukausi = input("Mikä kuukausi nyt on?\n")
if kuukausi == "joulukuu":
    print("Joulu tulla jolkottaa")
elif kuukausi == "elokuu":
    print("Vielä on kesää jäljellä")
```
## Lisätietoja: liukulukujen yhtäsuuruuden vertailu
:::{admonition} Huom!
:class: note
Liukulukujen yhtäsuuruuden vertailun kanssa pitää olla tarkkana! Yhtäsuuruuden vertailu on parasta tehdä
*math.isclose*-funktiolla. Palaamme tähän asiaan [luvussa *Funktiot ja moduulit*](../funktiot/math.md).
:::
### Tehtävä
Täydennä if-elif-else -lause vetämällä samat oikeille paikoilleen. Vaithoehtoja tyhjiin kohtiin: `elif`, `if`, `elif`, `else`.
```{code-cell} ipython3
:tags: ["auto-execute-page"]
paine = float("2.57") # bar
TÄYDENNÄ paine <= 0.0:
  print("Virheelinen paine")
TÄYDENNÄ paine <= 5.0:
  print("Turvallinen paine")
TÄYDENNÄ paine <= 7.0:
  print("Rajoilla ollaan")
TÄYDENNÄ:
  print("Rengas räjähti")
```
:::::{card} Tehtävä
Tehtäviin liittyvä ohjelma:
``` ipython3
konsentraatio = float(input("Anna konsentraatio (mol):\n"))
if konsentraatio <= 0:
  print("Virheellinen konsentraatio")
elif konsentraatio < 0.1:
  print("Laimea")
elif konsentraatio < 0.5:
  print("Keskivahva")
else:
  print("Väkevä")
```
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä koodi tulostaa, kun käyttäjä antaa arvon 0.25?
---
[x] Keskivahva
> Oikein!
[ ] Laimea
> Yritä uudelleen!
[ ] Ei mitään
> Yritä uudelleen!
[ ] Väkevä
> Yritä uudelleen!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä koodi tulostaa, kun käyttäjä antaa arvon 4.0?
---
[ ] Ei mitään
> Yritä uudelleen!
[ ] Keskivahva
> Yritä uudelleen!
[x] Väkevä
> Oikein!
[ ] Laimea
> Yritä uudelleen!
---
::::
:::::
