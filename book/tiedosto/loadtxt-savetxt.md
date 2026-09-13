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
# Tiedostojen helppo käsittely NumPy:llä
NumPy-kirjasto sisältää käteviä funktioita [tiedostojen käsittelyyn](https://docs.scipy.org/doc/numpy/reference/routines.io.html).
Nämä ovat hyödyllisiä etenkin numeerista dataa luettaessa. Tekstitiedostoja voi lukea ja kirjoittaa
[*numpy.loadtxt*](https://docs.scipy.org/doc/numpy/reference/generated/numpy.loadtxt.html)- ja [*numpy.savetxt*](https://docs.scipy.org/doc/numpy/reference/generated/numpy.savetxt.html)-funktioilla.
Tarkastellaan esimerkkiä, jossa meillä on tilavuus- ja painedataa tiedostossa [painedata.txt](./painedata.txt)
seuraavassa muodossa (kommenttirivi ja kolme ensimmäistä datariviä näkyvissä):
``` ipython3
# V (dm^3)    p (Pa)
0.21          1856455
0.31          1176944
0.41          838490
```
Esimerkki, kuinka tiedoston voi lukea *numpy.loadtxt*-funktiolla ja tulokset voi kirjoittaa tiedostoon *numpy.savetxt*-funktiolla:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
import numpy as np

Vp_data = np.loadtxt("painedata.txt")
# Vp_data on nyt NumPy-taulukko, jossa on kaksi saraketta: V ja p
R = 8.314462618          # J K^-1 mol ^-1
n = 0.05                 # mol
V = Vp_data[:, 0] / 1000 # 1. sarake (V, dm^3). Muunnetaan dm^3 -> m^3
p = Vp_data[:, 1]        # 2. sarake (p, Pa)
T = V * p / (n * R)      # K
np.savetxt("T.txt", T, fmt="%.3f", header = "T (K)")
```
*loadtxt* osaa automaattisesti jättää tiedoston alussa olevan, #-merkillä alkavan kommenttirivin lukematta. 
Tiedostoja ei tarvitse avata ja sulkea, koska *loadtxt* ja *savetxt* tekevät sen puolestasi.
```{code-cell} ipython3
:tags: ["thebe-remove-input-init"]
import numpy as np
Vp_data = np.loadtxt("painedata.txt")
R = 8.314462618
n = 0.05
V = Vp_data[:, 0] / 1000
p = Vp_data[:, 1]
T = V * p / (n * R)
np.savetxt("T.txt", T, fmt="%.3f", header = "T (K)")
```
Tulostiedoston *T.txt* neljä ensimmäistä riviä näyttävät tältä (aja koodi):
 ```{code-cell} ipython3
Tulos_T = open("T.txt", "r")
i = 0
for rivi in Tulos_T:
  print(rivi)
  i = i + 1
  if i > 3:
    break
Tulos_T.close()
```
*savetxt*-funktion *header*-parametrin arvo tulee siis tiedoston alkuun kommenttiriviksi. *fmt*-parametrin rakenne on periaatteessa sama kuin *str.format*-funktiolla, mutta kaarisulut korvautuvat `%`-merkillä, eikä `:`-merkkiä käytetä. Lisätietoja [numpy.savetxt](https://docs.scipy.org/doc/numpy/reference/generated/numpy.savetxt.html)-funktion ohjeesta.
:::{admonition} Huom!
:class: warning
Jos tarkastelet *savetxt*-tiedoston luomaa tiedostoa Windowsissa, rivinvaihdot eivät välttämättä näy oikein. Tämä johtuu siitä, etteivät monet Windows-ohjelmat ymmärrä \n-rivinvaihtoa oikealla tavalla. Tiedosto näkyy oikein esim. Spyderissä.
:::
## numpy.column_stack
Kun sinulla on useita yksiulotteisia taulukoita, jotka haluat tallentaa sarakkeina tiedostoon, [*numpy.column_stack*](https://docs.scipy.org/doc/numpy/reference/generated/numpy.column_stack.html) on hyvin hyödyllinen funktio. Laajennetaan yllä olevaa esimerkkiä niin, että tallennamme tulostiedostoon myös alkuperäiset tilavuus- ja painedatat.
```{code-cell} ipython3
import numpy as np

Vp_data = np.loadtxt("painedata.txt")
R = 8.314462618          # J K^-1 mol ^-1
n = 0.05                 # mol
V = Vp_data[:, 0] / 1000 # 1. sarake (V, dm^3). Muunnetaan dm^3 -> m^3
p = Vp_data[:, 1]        # 2. sarake (p, Pa)
T = V * p / (n * R)      # K
# Käytetään np.column_stack -funktiota, jolla yksiulotteiset
# NumPy-taulukot voi liittää yhteen kaksiulotteisen taulukon sarakkeiksi
VpT_data = np.column_stack([V * 1000, p, T]) # Tilavuudet m^3 -> dm^3
np.savetxt("VpT.txt", VpT_data, fmt="%10.3f %10.0f %10.1f", 
           header = "V (dm^3)    p (Pa)       T (K)")
```
**Huomaa**, miten *fmt*-parametrille annetaan oma muotoiluparametri jokaiselle sarakkeelle. Tiedoston *VpT.txt* neljä ensimmäistä riviä näyttävät tältä:
``` ipython3
# V (dm^3)     p (Pa)       T (K)
     0.210     1856455      937.8
     0.310     1176944      877.6
     0.410      838490      826.9
```
### Tehtävä
Täydennä niin, että tiedoston c.txt neljä ensimmäistä riviä olisivat:
``` ipython3
#c (mol\dm^3)
0.05
0.91
0.121
```
```{code-cell} ipython3
import numpy as np

nV_data = np.TÄYDENNÄ("nV.txt")
# nV_data on nyt kuvitteellinen NumPy-taulukko, jossa on kaksi saraketta: n ja V. 
n = nV_data[:, 0]
V = nV_data[:, 1]       
c = n/V           
np.TÄYDENNÄ("c.txt", c, fmt=TÄYDENNÄ, header = "c (mol/dm^3)")
konsentraatiot = open("c.txt", "r")
for rivi in konsentraatiot:
 print(rivi)
konsentraatiot.close()
```
