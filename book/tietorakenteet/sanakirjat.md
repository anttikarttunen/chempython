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
# Sanakirjat
Sanakirjassa alkiot määritellään **avain:arvo** -pareina. Määrittelyn jälkeen avainta vastaavan arvon voi noutaa näin:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
print("Hiilen atomipaino on", atomipainot["C"])
```
:::{admonition} Huom!
:class: note
Määrittelyssä käytetään siis kaarisulkeita, mutta kun arvoihin viitataan avaimella, käytetään hakasulkeita.
:::
## Tyhjän sanakirjan luominen
``` ipython3
uusi_sanakirja = {}
```
## Arvojen lisääminen sanakirjaan
Arvojen lisääminen sanakirjaan on helppoa: annetaan vain uusi avain ja arvo:
```{code-cell} ipython3
# Luodaan tyhjä sanakirja ja lisätään kolme avain:arvo -paria
atomipainot = {}
atomipainot["H"] = 1.008
atomipainot["C"] = 12.011
atomipainot["O"] = 15.999
print(atomipainot)
```
Sanakirjan voi myös määritellä ensin tiettyjen *avain:arvo* parien kanssa ja lisätä siihen myöhemmin lisää pareja:
```{code-cell} ipython3
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
atomipainot["P"] = 30.973
print(atomipainot)
```
Python tulostaa sanakirjojen avaimet aina yksinkertaisia lainausmerkkejä käyttäen.
## Arvon lisääminen sanakirjaan muuttujan avulla
Arvoja voi lisätä sanakirjaan myös käyttämällä avaimena olemassa olevan muuttujan sisältöä:
``` ipython3
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}

# Kysytään käyttäjältä uusi alkuaine ja atomipaino sanakirjaan
alkuaine = input("Anna alkuainesymboli\n")
atomipaino = float(input("Anna atomipaino\n"))
# alkuaine on nyt merkkijonomuuttuja, esimerkiksi "P"
# atomipaino on nyt liukuluku, esimerkiksi 30.973
atomipainot[alkuaine] = atomipaino

# Tulostetaan sanakirjan sisältö
print("Atomipainot:", atomipainot)
```
Esimerkkitulostus:
```
Anna alkuainesymboli
> P
Anna atomipaino
> 30.973
Atomipainot: {'H': 1.008, 'C': 12.011, 'O': 15.999, 'P': 30.973}
```
Kurssin aikana käytämme lukuisia kertoja merkintää `sanakirja[muuttuja] = arvo`, kun haluamme lisätä
**avain:arvo**-pareja sanakirjaan.
## Arvon poimiminen sanakirjasta muuttujan avulla
Arvoja voi poimia sanakirjasta myös käyttämällä avaimena olemassa olevan muuttujan sisältöä:
``` ipython3
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
# Kysytään käyttäjältä alkuaine
alkuaine = input("Anna alkuainesymboli, niin tulostan atomipainon:\n")
# alkuaine on nyt merkkijonomuuttuja, esimerkiksi "C"
print(atomipainot[alkuaine])
```
Esimerkkitulostus:
```
Anna alkuainesymboli, niin tulostan atomipainon:
> C
12.011
```
Kurssin aikana käytämme lukuisia kertoja merkintää `arvo = sanakirja[muuttuja]`, kun haluamme poimia tietyn arvon sanakirjasta.
## Arvojen poistaminen sanakirjasta
Arvojen poistaminen sanakirjasta onnistuu *del*-avainsanalla:
```{code-cell} ipython3
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
del atomipainot["C"]
print(atomipainot)
```
## Avaimen olemassaolon tarkistaminen sanakirjasta
*in*-avainsana toimii samaan tapaan kuin listojen kanssa:
```{code-cell} ipython3
# in-avainsanalla voi testata, onko avain sanakirjassa:
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
if "C" in atomipainot:
    print("Hiilen atomipaino on", atomipainot["C"])
```
## Sanakirjan läpikäyminen, *items()*
Sanakirjan *items()*-funktio antaa arvot läpikäyntiä varten:
```{code-cell} ipython3
atomipainot = {"H":  1.008, "C": 12.011, "O": 15.999}
for alkuaine, atomipaino in atomipainot.items():
    print(f"Alkuaineen {alkuaine:s} atomipaino on {atomipaino:.3f} g/mol")
```
Yleinen muoto on siis
``` ipython3
for AVAIN, ARVO in SANAKIRJA.items():
    print(AVAIN, ARVO) # Silmukassa voimme käyttää avaimia ja arvoja kuten haluamme.
```
## Sanakirjan lajitteleminen
*sorted()*-funktiolla voi tulostaa avaimet aakkosjärjestyksessä tai arvot järjestyksessä (sanakirjan *values*-funktio):
```{code-cell} ipython3
atomipainot = {"P": 30.973, "C": 12.011, "O": 15.999}
print(sorted(atomipainot))
print(sorted(atomipainot.values()))
```
Huomaa kuitenkin, että alkuperäisen sanakirjan (*atomipainot*) järjestys ei muutu, vaikka kutsuisit *sorted*-funktiota.
:::{admonition} Huom!
:class: note
Pythonin versiosta 3.6 alkaen sanakirjan **avain:arvo** parit ovat oletuksena siinä järjestyksessä, missä ne on lisätty sanakirjaan.
:::
### Tehtävä
Täydennä alla oleva koodi ohjeiden mukaisesti
```{code-cell} ipython3
# Määrittele sanakirja moolimassat, jossa on avaimet XeF2, XeF4 ja XeF6
moolimassat = {"TÄYDENNÄ": 169.29, "TÄYDENNÄ": 207.28, "TÄYDENNÄ": 245.3}

# Tulosta sanakirjan sisältö
for yhdiste, moolimassa in moolimassat.TÄYDENNÄ:
    print(f"Yhdisteen {TÄYDENNÄ:s} moolimassa on {TÄYDENNÄ:.2f} g/mol")
   
# Poista XeF4 sanakirjasta
TÄYDENNÄ moolimassat["XeF4"]

# Muuta yhdisteen XeF6 moolimassaksi 245.28
moolimassat[TÄYDENNÄ] = 245.28
```
