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
# Tiedostojen avaaminen with-lausekkeella
Pythonissa on kätevä **with**-lauseke, joka kutsuu automaattisesti *close*-funktiota kun tiedoston käyttö lopetetaan.
Luetaan tiedosto [moolimassat.txt](./moolimassat.txt)
käyttäen **with**-lauseketta:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
with open("moolimassat.txt", "r") as mmtiedosto:
    # Yllä oleva rivi avaa tiedoston "moolimassat.txt", jonka jälkeen
    # se on käytettävissä "mmtiedosto"-nimisenä tiedosto-oliona
    # sisennetyn rakenteen sisällä
    rivi1 = mmtiedosto.readline()

# Tässä kohti ohjelma poistuu with-lausekkeesta (huomaa sisennyksen muutos)
# with-lauseke sulkee automaattisesti tiedosto-olion "mmtiedosto"
print(rivi1)
```
## with-lauseke ja virheenkäsittely
Virheenkäsittelyn näkökulmasta **with**-lauseke korvaa siis seuraavan **try-finally** -rakenteen:
``` ipython3
mmtiedosto = open("moolimassat.txt", "r")
try:
    rivi1 = mmtiedosto.readline()
    print(rivi1)
finally:
    # Tämä osio suoritetaan aina
    mmtiedosto.close()
```
Koska myös *open*-funktion mahdolliset virheet on tärkeää käsitellä, **with**-lausekkeesta on parasta käyttää seuraavaa muotoa:
```{code-cell} ipython3
try:
    with open("moolimassat.txt", "r") as mmtiedosto:
        rivi1 = mmtiedosto.readline()
        print(rivi1)
except OSError:
    print("Tiedoston moolimassat.txt avaaminen epaonnistui!")
```
Tämä viimeinen esimerkki on **minimivaatimus** virheenkäsittelylle tiedostoja avattaessa!
:::::{card} Tehtävä
::::{question}
:type: multiple-choice
:variant: multiple-select
:nocaption:
:columns: 1

Valitse oikeat väitteet.
---
[ ] with-lausekkeen kanssa ei tarvitse käyttää open-funktion virhetarkastelua.
> Yritä uudelleen!
[x] with-lauseke kutsuu automaattisesti close-funktiota.
> Oikein!
[x] with-lauseke korvaa try-finally-rakenteen.
> Oikein!
[ ] with-lausekkeen oikea muoto: open with("tiedosto.txt", "r") as datat:
> Yritä uudelleen!
[x] with-lausekkeen oikea muoto: with open("tiedosto.txt", "r") as datat:
> Oikein!
---
::::
:::::
