---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.17.3
kernelspec:
  display_name: base
  language: python
  name: python3
---

# Johdanto
Käydään ensin läpi yleisiä tietoja oppimateriaalista ja ohjelmointitehtävien tekemisestä.

## 1. Spyder-ohjelmointiympäristön asentaminen
Ohjelmointitehtävien tekemiseksi tarvitset esimerkiksi Spyder-ohjelmointiympäristön, joka sisältää myös Python-kehitysympäristön. Oppimateriaalin Lisämateriaali-luku sisältää [Spyderin asennusohjeen](lisamateriaali/spyder-asennus.md) ja [Spyderin käyttöohjeita](lisamateriaali/spyder-kaytto.md).

## 2. Oppimateriaalin lukuohje
Kun oppimateriaalissa esitetään Python-koodia, se näyttää tältä:
```ipython3
print("Nyt lasketaan!")
print("11*11 on", 11*11)
```
Osan oppimateriaalin koodiesimerkeistä voi ajaa suoraan selaimessa painamalla koodin alapuolella olevaa `run`-painiketta. Koodia voi myös muokata suoraan koodilaatikossa tai voit halutessasi lisätä uuden tyhjän koodilaatikon `add cell` -painikkeesta. Tekemäsi muutokset eivät tallennu oppimateriaaliin. 

Kokeile ajamista alla olevalla koodilla.
```{code-cell} ipython3
:tags: ["auto-execute-page"]
print("Nyt lasketaan!")
print("11*11 on", 11*11)
```
Välillä koodin tulostus näytetään laatikossa heti koodin alapuolella. Esimerkiksi koodi:
```ipython3
print("Nyt lasketaan!")
print("11*11 on", 11*11)
```
tulostaisi seuraavat rivit:
```
Nyt lasketaan!
11*11 on 121!
```

## 3. Oppimateriaalin esimerkkiohjelmien kokeileminen itse
- Kopioi esimerkkiohjelman koodi Spyder-editoriin.
- Aja koodi painamalla Spyderissä vihreää "Run"-painiketta tai F5-nappia.

````{admonition} Vinkki
:class: tip
Esimerkkiohjelmien **kokeileminen ja muokkaaminen on erittäin suositeltavaa**, koska se helpottaa merkittävästi esimerkkien ymmärtämistä.
````

## 4. Ohjelmakoodin kommentointi
Ohjelmien huolellinen kommentointi on ensiarvoisen tärkeää, jotta:
- muut ymmärtävät, mitä kirjoittamasi koodi tekee
- muistat itse, mitä kirjoittamasi koodi tekee!

Ohjelmakoodiin voi lisätä kommentteja `#`-merkin jälkeen:
```{code-cell} ipython3
#Aloitetaan!
print("Eka ohjelmani")
#Jatketaan!
print("Moi!") #Rivin loppuun voi myös lisätä kommentteja
```
Kokeile tulostaa yllä oleva koodi. Huomaa, että kommentit eivät tulostuneet.

Monirivisiä kommentteja voi kirjoittaa """"*kommentti*"""" -merkinnällä:
```{code-cell} ipython3
print("Eka ohjelmani")
"""
Olipa hieno kokemus!
Tämä on kolmerivinen välikommentti.
Sitten jatketaan!
"""
print("Moi!")
```
## 5. Muita Python-oppimateriaaleja
Lisämateriaalin [Python-verkkomateriaaleja](lisamateriaali/verkko-mat.md) -kappaleessa on listattu  hyviä verkosta 
löytyviä oppimateriaaleja, joita voi myös hyödyntää Python-ohjelmoinnin opettelussa. Jos pidät opiskelusta 
videomateriaalien avulla, sivulta löytyy linkkejä videomuotoisiin oppimateriaaleihin.

## 6. Jos olet aiemmin osallistunut kurssille *Ohjelmoinnin peruskurssi Y1*
Jos olet aiemmin osallistunut Aallon yleiselle Python-kurssille, tutustuthan lisämateriaalin kappaleeseen 
[*main*-funktio](lisamateriaali/main-funktio.md) ennen kuin aloitat tämän kurssin tehtävien tekemisen.

## 7. Oppimateriaalin sisältämät tehtävät
Oppimateriaali sisältää myös erilaisia tehtäviä, joilla voit tarkistaa, kuinka hyvin olet sisäistänyt oppimateriaalissa käsitellyt asiat.

Oppaassa olevien tehtävien tarkoitus on tukea oppimista, ne eivät vaikuta kurssin arvosteluun!

Alla on kaksi esimerkkiä oppimateriaalin tehtävätyypeistä.

:::::{card} Tehtävä
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä ohjelmointikieltä tällä kurssilla opetellaan?
---
[ ] Perl
[x] Python
> Oikein!
[ ] INTERCAL
[ ] Cobra
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Minkä perusteella kurssin arvosana määräytyy?
---
[ ] Läsnäolon
[ ] Kysymysten esittämisen
[x] MyCourses-tehtävien pisteiden
> Oikein!
---
::::
:::::
### Tehtävä
Täydennä koodi niin, että ohjelma tulostaa:
```
Yksi
Kaksi
Kolme
```
```{code-cell} ipython3
print("Yksi")
TÄYDENNÄ("Kaksi")
pint("Kolme")
```
