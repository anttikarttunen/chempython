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
# Totuusmuuttujat
Ehtolauseissa hyödynnetään usein totuusmuuttujia (`bool`). Totuusmuuttujan arvo on joko `True` tai `False`, joten
totuusmuuttujaan on kätevä tallentaa tieto siitä, onko joku ehto täyttynyt ja testata tätä ehtoa myöhemmin:
``` ipython3
paine = float(input("Anna paine reaktorissa (bar):\n"))
# Jos paine on yli 1 bar, tallennetaan tieto totuusmuuttujaan ylipaine
if paine > 1.0:
    ylipaine = True
else:
    ylipaine = False

T = float(input("Anna lämpötila (K):\n"))
if T > 385.0:
    if ylipaine:
        print("Varoitus! Reaktorissa ylipaine ja korkea lämpötila")
else:
    print("Olosuhteet OK")
```
Huomaa, miten totuusmuuttujaa ylipaine voi käyttää if-ehtolauseessa yksinkertaisesti muodossa
``` ipython3
if ylipaine:
```
eikä tarvitse siis kirjoittaa
``` ipython3
if ylipaine == True:
```
Tämä johtuu siitä, että if-ehtolauseen testin arvo on aina `True` tai `False`, joten totuusmuuttujan voi laittaa
suoraan ehtolauseen testiksi.
### Tehtävä
Täydennä koodi niin, että if-ehtolause on kemiallisesti mielekäs. Vaihtoehdot `TÄYDENNÄ`-kohtiin: `True` tai `False`. 
Voit kokeilla eri kemiallisia kaavoja muuttujaan *yhdiste*.
```{code-cell} ipython3
:tags: ["auto-execute-page"]
yhdiste = "H2SO4"
if yhdiste == "HCl":
  happo = TÄYDENNÄ
elif yhdiste == "H2SO4":
  happo = TÄYDENNÄ
else:
  happo = TÄYDENNÄ

if happo:
  print("Varoitus, happoa!")
```
