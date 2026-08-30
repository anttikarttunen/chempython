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

# Tulostaminen (print) ja syötteen lukeminen (input)
## Tulostaminen *print*-funktiolla
Pythonissa voi tulostaa tietoa ruudulle *print*-funktiolla:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
# Tulostetaan merkkijono "Terve!"
print("Terve!")
```
````{admonition} Funktiot
:class: note
Funktioiden toimintaperiaatteisiin perehdymme tarkemmin oppimateriaalin luvussa *Funktiot ja moduulit*. Nyt ensimmäisessa luvussa hyödynnämme vain muutamia Pythonin sisäänrakennettuja funktioita, joiden käyttö on yhtä suoraviivaista kuin print-funktion käyttö.
````

Otetaan toinen esimerkki, jossa *print*-funktiolle annetaan useita eri arvoja pilkulla erotettuna. Se tulostaa molemmat arvot niin, että niiden välissä on välilyönti.
```{code-cell} ipython3
# Näin voimme tulostaa laskutoimitusten tuloksia
print("11*11 on", 11*11)
```
**Laskutoimituksista**: Halutessasi voi tehdä laskutoimituksia myös suoraan Spyderin Python-konsolissa. Kokeile kirjoittaa konsoliin esimerkiksi 5*5 ja paina `Enter`.
## Isot ja pienet kirjaimet
Pythonissa isot ja pienet kirjaimet ovat merkitseviä. Käsky **print** on siis eri asia kuin **Print** tai **PRINT**.
## Käyttäjän syötteen lukeminen *input*-funktiolla
Käyttäjältä voi kysyä tietoja **input**-funktiolla:
``` ipython3
#Kysytään käyttäjän nimeä
nimi = input("Mikä nimesi on?")
print("Hieno nimi sinulla", nimi)
```
Jos kopioit yllä olevan koodin Spyderiin ja ajat sen, Spyder odottaa sinun vastaavan kysymykseen oikean alareunan konsoliruudussa. Esimerkkituloste käyttäisi tältä (käyttäjä syöttää vastauksen `Marsu`):
```
Mikä nimesi on?Marsu
Hieno nimi sinulla Marsu
```
:::{admonition} Huom!
:class: note
Esimerkissä siis *input*-funktiolla kysytään käyttäjältä nimeä ja käyttäjän antama merkkijono tallennetaan **muuttujaan** *nimi*. Sen jälkeen muuttujan arvo voidaan tulostaa *print*-funktion avulla. Muuttujiin voidaan säilöä tietoa ja niistä kerrotaan lisää seuraavassa luvussa.
:::
Kysymys ja vastaus tulostuvat hieman selkeämmin, jos lisätään välilyönti merkkijonon loppuun:
```ipython3
nimi = input("Mikä nimesi on? ")
print("Hieno nimi sinulla", nimi)
```
Käyttäjä vastaa kysymykseen jälleen `Marsu` (huomaa, miten kysymysmerkin jälkeen on nyt välilyönti):
```
Mikä nimesi on? Marsu
Hieno nimi sinulla Marsu
```
Kaikkein selkeintä on yleensä käyttää rivinvaihtoa `\n` kysymyksen lopussa
``` ipython3
nimi = input("Mikä nimesi on?\n")
print("Hieno nimi sinulla", nimi)
```
Tästä lähtien  oppimateriaalissa käytetään `>`-merkkiä, kun näytetään, mitä käyttäjä antaa syötteenä input-funktiolle:
```
Mikä nimesi on?
> Marsu
Hieno nimi sinulla Marsu
```
Kolmas esimerkki, jossa kysytään kaksi eri tietoa ja tulostetaan ne molemmat:
``` ipython3
nimi = input("Mikä nimesi on?\n")
kaveri = input("Mikä kaverisi nimi on?\n")
print("Mukava tavata", nimi, "ja", kaveri)
```
Käyttäjä vastaa kysymyksiin `Marsu` ja `Jomppa`:
```
Mikä nimesi on?
> Marsu
Mikä kaverisi nimi on?
> Jomppa
Mukava tavata Marsu ja Jomppa
```
## Tärkeää: input-funktio palauttaa aina merkkijonon
*input*-funktio lukee käyttäjältä aina ns. *merkkijonon* (engl. string). Tämä koodi:
``` ipython3
luku = input("Anna luku niin kerron sen kahdella:\n")
print("Antamasi luku", luku, "kerrottuna kahdella on", 2 * luku)
```
**ei** siis annakaan odotettua lopputulosta:
```
Annan luku niin kerron sen kahdella
> 5
Antamasi luku 5 kerrottuna kahdella on 55
```
:::{admonition} Vinkki
:class: tip
Tämä ongelma ratkeaa seuraavassa luvussa, jossa opimme käsitteet *muuttuja* ja muuttujan *tyyppi*.
:::
## input-funktio CodeRunner-tehtävissä
CodeRunner-tehtävissä *input*-funktion kysymystä (esim. "Anna nimi:\n") ei tarkasteta, 
mutta kannattaa käyttää selkeitä kysymyksiä, jotta kirjoittamasi koodi on selkeää ja luettavaa.
## Lisätietoa print-funktiosta: Rivinvaihdot ja end-parametri
*print*-funktio lisää tekstin loppuun oletuksena rivinvaihdon "\n". Niitä voi myös tulostaa itse lisää:
```{code-cell} ipython3
#Tulostetaan kaksi alkuainesymbolia ja kolme rivinvaihtoa ("\n")
print("Jaloja kaasuja: He ja Ne\n\n\n")
#Tulostetaan pari kaasua lisää
print("Ja lisäksi: Ar ja Kr")
```
Rivinvaihdon voi muuttaa joksikin muuksi merkiksi *print*-funktion *end*-parametrillä:
```{code-cell} ipython3
print("Rivi 1.")
print("Rivi 2. Rivien väliin tuli rivinvaihto.")
print("Teksti.", end = " ")
print("Teksti 2. Tekstien väliin tuli välilyönti.")
```
### Tehtävä
Täydennä alla oleva koodi niin, että se tulostaa:
```
Hiilimonoksidin (CO) moolimassa on 28.01 g/mol
0.5 mol hiilidioksidia painaa siis 14.005 grammaa
```
Tarkista koodi ajamalla se `run`-painikkeesta.
```{code-cell} ipython3
TÄYDENNÄ("Hiilimonoksidin (CO) moolimassa on 28.01 g/mol")
print("0.5 mol hiilimonoksidia painaa siis",TÄYDENNÄ/2, "grammaa")
```
:::::{card} Tehtävä
Täydennä tyhjät kentät riveittäin niin, että ohjelma tulostaa (">" tarkoittaa käyttäjän syötettä):
```
Mitä opiskelet?
> Kemian tekniikkaa
Missä opiskelet?
> Aalto-yliopistossa
Kemian tekniikkaa voi opiskella Aalto-yliopistossa
```
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

``` ipython3
ala = TÄYDENNÄ("Mitä opiskelet?\n")
```
---
[ ] print
> Yritä uudelleen!
[x] input
> Oikein!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

``` ipython3
paikka = TÄYDENNÄ("Missä opiskelet?\n")
```
---
[ ] print
> Yritä uudelleen!
[x] input
> Oikein!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

``` ipython3
TÄYDENNÄ(ala, "voi opiskella", paikka)
```
---
[x] print
> Oikein!
[ ] input
> Yritä uudelleen!
---
::::
:::::
