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
# Datan lukeminen ja kirjoittaminen
Luodaan tiedosto *halogeenit.txt*, joka sisältää halogeenien symbolit. Voimme kirjoittaa tiedostoon käyttämällä *write()*-funktiota:
```{code-cell} ipython3
halogeenit = ['F', 'Cl', 'Br', 'I']
# Avataan uusi tiedosto kirjoittamista varten
tiedosto = open("halogeenit.txt", "w")
# Käydään halogeenit-lista läpi for-silmukan avulla
for halogeeni in halogeenit:
    # Kirjoitetaan jokainen listan alkio omalle rivilleen (\n on rivinvaihto)
    # Kirjoittamiseen käytetään write()-funktiota
    tiedosto.write(halogeeni + "\n")
# Lopuksi suljetaan tiedosto!
tiedosto.close()
```
```{code-cell} ipython3
:tags: ["thebe-remove-input-init"]
halogeenit = ['F', 'Cl', 'Br', 'I']
tiedosto = open("halogeenit.txt", "w")
for halogeeni in halogeenit:
    tiedosto.write(halogeeni + "\n")
tiedosto.close()
```
Luetaan seuraavaksi juuri luomamme tiedoston sisältö rivi kerrallaan. Hyödynnetään **for**-silmukkaa:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
halogeenit1 = []
halogeenit2 = []
tiedosto = open("halogeenit.txt", "r")
# Seuraava for-silmukka lukee tiedostosta rivin kerrallaan.
# Silmukkamuuttuja "rivi" päivittyy jokaisella silmukan kierroksella kunnes 
# kaikki tiedoston rivit on luettu
for rivi in tiedosto:
    halogeenit1.append(rivi)
    # str.rstrip()-funktio poistaa rivinvaihdon rivin lopusta
    halogeenit2.append(rivi.rstrip())

# Suljetaan tiedosto!
tiedosto.close()
    
print(halogeenit1)
print(halogeenit2)
```
Eli [*str.strip*](https://docs.python.org/3/library/stdtypes.html#str.rstrip)-funktiolla päästin eroon tiedostossa olleista rivinvaihtomerkistä, jotka Python sisällyttää lukemiinsa riveihin.
## str.split-funktion ja f-merkkijonojen hyödyntäminen
Luodaan tiedosto *neliot.txt*, joka sisältää numerot 1-100 ja niiden neliöt välilyönnillä erotettuna. Tiedoston rakenne on siis (kolme ensimmäistä riviä):
``` ipython3
1 1
2 4
3 9
```
Huomaa, miten f-merkkijonoja voidaan hyödyntää myös tiedostoon kirjoitettaessa:
```{code-cell} ipython3
tiedosto = open("neliot.txt", "w")
for i in range(1, 101):
    tiedosto.write(f"{i:d} {(i * i):d}\n")
tiedosto.close()
```
Avataan luotu tiedosto lukemista varten ja hyödynnetään aiemmin kierroksella 3 mainittua [*str.split*](../Kierros3/s3_8.md)
-funktiota:
```{code-cell} ipython3
:tags: ["thebe-remove-input-init"]
tiedosto = open("neliot.txt", "w")
for i in range(1, 101):
    tiedosto.write(f"{i:d} {(i * i):d}\n")
tiedosto.close()
```
```{code-cell} ipython3
tiedosto = open("neliot.txt", "r")
for rivi in tiedosto:
    # rivi on siis merkkijono, esim. "3 9\n". Funktio str.split() palauttaa 
    # listan, johon merkkijonon sanat on pilkottu alkioiksi.
    # Jos siis rivi on "3 9\n", rivi.split() palauttaa listan ["3", "9"]
    # str.split-funktio siivoaa myös rivinvaihdot (\n) pois
    # Funktion palauttamat arvot voi lukea suoraan muuttujiin:
    luku, nelio = rivi.split()
    
    # Toinen vaihtoehto olisi lukea arvot listaan ja poimia ne sieltä:
    # datat = rivi.split() 
    # luku = datat[0] 
    # nelio = datat[1]

    # Luvut ovat nyt edelleen merkkijonoina. Ne voisi muuntaa 
    # kokonaisluvuiksi int()-funktiolla, mutta nyt riittää tulostus
    print("Luvun", luku, "nelio on", nelio)
tiedosto.close()
```
## Numeroarvojen lukeminen tiedostosta
Meilä on käytössämme datatiedosto [moolimassat.txt](./moolimassat.txt), 
joka sisältää kullakin rivillä yhdisteen nimen, moolimassan (g/mol) ja massan (g) välilyönneillä erotettuna. 
Tiedoston kaksi ensimmäistä riviä näyttävät tältä:
``` ipython3
H2O  18.015 2.3
NaCl 58.44  4.5
```
Luetaan nyt tiedoston sisältö niin, että voimme hyödyntää lukuarvoja laskennassa
```{code-cell} ipython3
tiedosto = open("moolimassat.txt", "r")
for rivi in tiedosto:
    datat = rivi.split()
    # datat on nyt kolmen merkkijonon lista, esim.: ["H2O", "18.015", "2.3"]
    nimi = datat[0]
    moolimassa = float(datat[1])
    massa = float(datat[2])
    ainemaara = massa / moolimassa
    print(f"Yhdisteen {nimi} ainemaara on {ainemaara:4.3f} mol")

# Lopuksi suljetaan tiedosto
tiedosto.close()
```
## Toinen esimerkki numeroarvojen lukemisesta
Meillä on käytössämme datatiedosto [temps.txt](./temps.txt), joka sisältää kullakin rivillä alkuaineen
symbolin, nimen, sulamispisteen (°C) ja kiehumispisteen (°C). Tiedoston kaksi ensimmäistä riviä näyttävät tältä:
``` ipython3
Sc, skandium   , 1541.0 ,2830
Ti  , titaani  , 1668.0,3287
```
**Huomaa**, että tiedot ovat nyt pilkulla eroteltuna ja sisältävät ylimääräisiä välilyöntejä. Luetaan nyt tiedoston sisältö hyödyntämällä [*str.split*](../tietorakenteet/str-listana.md)-funktion *sep*-parametriä, jolla voi määrätä datapisteiden 
välisen erottimen. Lisäksi tarvitsemme [*str.strip*](https://docs.python.org/3/library/stdtypes.html#str.strip)-funktiota 
ylimääräisten välilyöntien poistamiseen.
```{code-cell} ipython3
metallit = []
tiedosto = open("temps.txt", "r")
for rivi in tiedosto:
    datat = rivi.split(sep = ',')
    # datat on nyt neljän merkkijonon lista, esim.: ["Sc", " skandium   ", "1541.0 ", "2830"]
    # Käytetään lisäksi str.strip()-funktiota, joka karsii tyhjät merkit 
    # (välilyönnit, rivinvaihdot) merkkijonon vasemmalta ja oikealta puolelta. 
    # Esimerkiksi "  testi  \n".strip() palauttaa "testi"
    symboli = datat[0].strip()
    nimi = datat[1].strip()
    # sulamispiste ja kiehumispiste liukulukuina. str.strip()-funktiota ei tarvita, 
    # float osaa jättää ylimääräiset välilyönnit huomioimatta
    sulamispiste = float(datat[2])
    kiehumispiste = float(datat[3])
    
    print(f"Alkuaineen {symboli:2s} sulamispiste on {sulamispiste:4.0f} C ja kiehumispiste {kiehumispiste:4.0f} C")

# Lopuksi suljetaan tiedosto!
tiedosto.close()
```
### Tehtävä
Täydennä koodi niin, että lähtöarvojen perusteella laskettu data tallennetaan uuteen tiedostoon.\
Vaihtoehtoja tyhjiin kohtiin: `close`, `open`, `strip`, `close`, `split`, `write`, `open`
```{code-cell} ipython3
reaktionopeusvakiot = []
#Tiedosto sisältää lähtöarvot reaktionopeusvakioiden laskemiseen.
tiedosto = TÄYDENNÄ("lahtoarvot.txt", "r")
for rivi in tiedosto:
    datat = rivi.TÄYDENNÄ(sep = ',')
    r = float(datat[0].strip())
    c = float(datat[1].strip())
    T = float(datat[2].TÄYDENNÄ())
    print(f"Reaktionopeus lampotilassa {T} on {r/c}")
    reaktionopeusvakiot.append(r/c)
    reaktionopeusvakiot.append(T)
tiedosto.TÄYDENNÄ()
#i on indeksi
i = 0
tiedosto = TÄYDENNÄ("tulokset.txt", "w")
while i < len(reaktionopeusvakiot):
    tiedosto.TÄYDENNÄ(f"{reaktionopeusvakiot[i]}, {reaktionopeusvakiot[i+1]}\n")
    i += 2
tiedosto.TÄYDENNÄ()
```
