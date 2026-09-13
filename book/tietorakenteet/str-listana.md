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
# Merkkijonojen käsittely listoina
Merkkijonot ovat läheistä sukua listoille. Merkkijonon voi muuntaa suoraan listaksi:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
merkkijono_listana = list('Sana')
print("Merkkijono listana:", merkkijono_listana)
```
Merkkijonon voi siis itsessään ajatella olevan "lista merkkejä". Näin ollen myös merkkijonoja voi indeksoida ja siivuttaa:
```{code-cell} ipython3
teksti =  "Kemisti"
# indeksi: 0123456
print(teksti[0])
print(teksti[0:4])
```
Merkkijonosta voi etsiä toisen merkkijonon sijainnin *str.index*-funktiolla:
```{code-cell} ipython3
merkkijono = "Huomio!!?"
# indeksi:    012345678
print(merkkijono.index("!!"))
```
## Merkkijonofunktiot *str.split* ja *str.join*
Funktio [*str.split*](https://docs.python.org/3/library/stdtypes.html#str.split) pilkkoo merkkijonon listaksi. Esimerkiksi:
```{code-cell} ipython3
teksti = "Sc Ti V Cr Mn Co Fe Ni Cu Zn"
alkuaineet = teksti.split()
print(alkuaineet)
```
*str.split*-funktiota tarvitaan usein, kun halutaan muuttaa tekstimuodossa olevaa dataa numeroiksi, joita halutaan analysoida. Tekstimuotoinen data voi olla peräisin esimerkiksi tiedostosta tai tietokannasta, johon tiedot on alun perin tallennettu tekstimuodossa.

*str.split*-funktiolla luodun listan voi käydä läpi *for*-silmukalla:
```{code-cell} ipython3
def laske_nollat_ja_keskiarvo(teksti):
    # teksti: merkkijono, joka sisältää välillyönnillä erotettuja kokonaislukuja

    # split-funktio palauttaa listan, jonka alkiot ovat merkkijonoja
    numerot = teksti.split()
    # Käydään numerot-lista läpi for-silmukan avulla ja lasketaan keskiarvo
    summa = 0
    nollat = 0
    for alkio in numerot:
        # Muunnetaan jokainen alkio kokonaisluvuksi ja tarkastetaan, onko se nolla
        numero = int(alkio)
        if numero == 0:
            nollat = nollat + 1
        else:
            summa = summa + numero

    print(f"Listassa on {len(numerot)} lukua, joista {nollat} on nollia. Lukujen keskiarvo on {summa / len(numerot):.2f}.")

laske_nollat_ja_keskiarvo("234 5 66 0 0 0 23 99 542 21 53 9 0")
```
Toinen esimerkki, missä merkkijono pilkotaan väliaikaiseksi listaksi, josta poimitaan tarpeelliset tiedot:
```{code-cell} ipython3
def laske_keskiarvo(arvioinnit):
    # arvioinnit: lista, jonka alkiot ovat merkkijonona "opiskelijanumero arvosana"    
    summa = 0    
    for arviointi in arvioinnit:
        tiedot = arviointi.split()
        # tiedot on nyt kahden alkion lista, jonka toinen alkio on arvosana (merkkijonona)
        # Muunnetaan se kokonaisluvuksi
        arvosana = int(tiedot[1])
        summa = summa + arvosana        
        
    print(f"Arvosanoja oli {len(arvioinnit)} kpl ja keskiarvo on {summa / len(arvioinnit):.2f}")

laske_keskiarvo(["997731567 4", "997731527 2", "997731589 2", "997731511 5", "997731562 1", "997731447 3"])
```
Oletuksena merkkijonosta poimitaan välilyönnillä erotetut alkiot. Tätä voi muuttaa *sep*-parametrillä:
```{code-cell} ipython3
teksti = "4, 21, 53, 12, 7, 0"
numerot = teksti.split(sep = ',')
print(numerot)
```
Funktion *str.split* käänteisoperaatio on [*str.join*](https://docs.python.org/3/library/stdtypes.html#str.join). 
Funktiolle annetaan parametrina lista ja se yhdistää listan alkiot merkkijonoksi:
```{code-cell} ipython3
alkuaineet = ['B', 'C', 'N', 'O', 'F', 'Ne']
teksti = " ".join(alkuaineet)
print(teksti)
```
Listan alkioiden väliin lisätään *.join*-funktiokutsua edeltävä merkkijono. Esimerkiksi:
```{code-cell} ipython3
alkuaineet = ['B', 'C', 'N', 'O', 'F', 'Ne']
teksti = ", ".join(alkuaineet)
print(teksti)
```
## Merkkijonon sisällön tutkiminen merkki kerrallaan *for*-silmukan avulla
Pythonin dokumentaatiossa listataan useita 
[merkkijonojen käsittelyyn tarkoitettuja funktioita](https://docs.python.org/3/library/stdtypes.html#string-methods). 
Katsotaan, kuinka merkkijonon sisältöä voi tutkia merkki kerrallaan *for*-silmukan avulla.

Funktiolla *str.isdigit* voi etsiä numeroita:
```{code-cell} ipython3
# Käydään katuosoite läpi merkki kerrallaan ja poimitaan numerot
katuosoite = "Kemistintie 23"
numerot = ""
for merkki in katuosoite:
    if merkki.isdigit():
        numerot = numerot + merkki      
print("Talon numero on", numerot)
```
Funktiolla *str.isalpha* voi etsiä kirjaimia:
```{code-cell} ipython3
# Käydään postinumero läpi merkki kerrallaan ja poimitaan kirjaimet
postinumero = "02150 ESPOO"
kirjaimet = ""
for merkki in postinumero:
    if merkki.isalpha():
        kirjaimet = kirjaimet + merkki

print("Postitoimipaikka on", kirjaimet)
```
Funktioilla *str.isupper* ja *str.islower* voi tutkia, onko merkki iso vai pieni kirjain. *str.isspace* kertoo, onko
merkki "whitespace", eli esimerkiksi välilyönti, tabulaattori tai rivinvaihto:
```{code-cell} ipython3
# Kerätään alkuainesymbolit listaan
teksti = "Sc Ti V Cr Mn Co Fe Ni Cu Zn "
alkuaineet = []
apujono = ""
# Käydään teksti läpi kirjain kerrallaan
for merkki in teksti:
    # Alkuaineen symboli alkaa aina isolla kirjaimella
    if merkki.isupper():
        # Iso kirjain talteen
        apujono = merkki
    elif merkki.islower():
        # Lisätään pieni kirjain ison alkukirjaimen perään
        apujono = apujono + merkki
    elif merkki.isspace():
        # Välilyönti erottaa symbolit, eli apujono sisältää nyt alkuainesymbolin
        # Symboli on joko (a) iso kirjain + pieni kirjain tai (b) vain iso kirjain
        alkuaineet.append(apujono)
        apujono = ""
print(alkuaineet)
```
### Tehtävä
Täydennä alla oleva koodi niin, että se tulostaa:
```
Merkkijono listana: ['R', 'e', 'a', 'k', 't', 'o', 'r', 'i']
```
```{code-cell} ipython3
merkkijono_listana = TÄYDENNÄ('Reaktori')
print("Merkkijono listana:", TÄYDENNÄ)
```
