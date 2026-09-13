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
# scipy.stats
[scipy.stats](https://docs.scipy.org/doc/scipy/reference/stats.html)-moduuli sisältää valtavan määrän erilaisia tilastollisia
funktioita ja jakaumafunktioita. Tämän kurssin puitteissa tutustumme vain *scipy.stats.linregress*-funktioon, jolla voi tehdä
[lineaarisen regressioanalyysin](https://fi.wikipedia.org/wiki/Lineaarinen_regressioanalyysi) esimerkiksi mittausdatoille. 
Käytännössähän kyse on samasta suoran yhtälön sovituksesta, mitä olemme jo tehneet 
[numpy.polyfit](../numpy/polynomit.md)-funktion avulla 1. asteen polynomeille. 
*linregress*-funktio on kuitenkin suunniteltu juuri lineaariseen regressioon ja se myös palauttaa enemmän tietoja sovituksesta, esimerkiksi korrelaatiokertoimen ja keskivirheen. Lisäksi *linregress* on laskennallisesti tehokkaampi hyvin suurille datajoukoille.

## Esimerkki
Tutustutaan *linregress*-funktioon esimerkin avulla. Meillä on käytössämme tiedosto 
[T-p-data.txt](./T-p-data.txt), 
jossa on esitetty painelämpötilan funktiona kaasumaiselle yhdisteelle (*n* = 0.65 mol). Mittausolosuhteet ovat sellaiset, 
että voimme odottaa ideaalikaasulain olevan voimassa. Tehtävänä on ratkaista astian tilavuus *V*.  
- *pV = nRT*, joten *p = nRT / V*
- Kun paine esitetään lämpötilan funktiona ja mittausdatat sovitetaan suoran yhtälöön, sovitussuoran kulmakerroin on *nR/V*.
  Eli *V = nR / kulmakerroin*.
- Luetaan siis datat tiedostosta, tehdään niille lineaarinen regressio *linregress*-funktiolla ja ratkaistaan tilavuus *V*.
```{code-cell} ipython3
:tags: ["auto-execute-page"]
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import linregress
from scipy.constants import R

n = 0.65 # mol
try:
    T_p_datat = np.loadtxt("T-p-data.txt")   # Luetaan datat tiedostosta
except OSError:
    print("Tiedoston T-p-data.txt avaaminen epaonnistui")
else:
    # Lukeminen onnistui, luodaan kaksi yksiulotteista taulukkoa
    T = T_p_datat[:, 0]
    p = T_p_datat[:, 1]
    
    # Lineaarinen regressio. T == x, p == y
    slope, intercept, r_value, p_value, std_err = linregress(T, p)
    
    # Sovitussuoran yhtälö: y = slope * x + intercept
    p_sovitetut = slope * T + intercept   # Lasketaan sovitussuoran arvot mitatuille x-arvoille (taulukko T)
  
    # Piirretään mittausdatat ja sovitussuora
    plt.plot(T, p, '.', color = 'red', label = 'Mittaukset (T, p)')
    # r_value on korrelaatiokerroin
    teksti = "Sovitus (R$^2$ = {:.3f})".format(r_value**2)
    plt.plot(T, p_sovitetut, '-', color = 'black', label = teksti)
    
    plt.xlim(300, 400)  # Kuvaajan akselit ja muut asetukset.
    plt.ylim(100000, 150000)
    plt.xticks(np.arange(300, 401, 20))
    plt.yticks(np.arange(100000, 150001, 10000))
    plt.xlabel('T (K)')
    plt.ylabel('p (Pa)')
    plt.legend(loc = 'upper left')
    plt.show()

    # Ratkaistaan V == n * R / slope
    # Tulostetaan V ja kulmakertoimen keskivirhe std_err
    print("V: {:.3f} m^3".format(n * R / slope))
    print("Kulmakertoimen keskivirhe: {:.1f}".format(std_err))
```
### Tehtävä
Täytä puuttuvat kohdat niin, että koodi toimisi.\
Vaihtoehdot tyhjiin kohtiin: `linregress`, `std_err`, `scipy.stats`, `intercept`, `slope`, `p_value`\
Esimerkkitulostus:
```
Sovituksen kulmakerroin: 0.8, vakiotermi: 0.1
Kulmakertoimen keskivirhe: 0.3
```
```{code-cell} ipython3
import numpy as np
from TÄYDENNÄ import TÄYDENNÄ

np.random.seed(12345)  #Luodaan random dataa
x = np.random.random(10)
y = np.random.random(10)

TÄYDENNÄ, TÄYDENNÄ, r_value, TÄYDENNÄ, std_err = linregress(x, y)

print(f"Sovituksen kulmakerroin: {slope:.1f}, vakiotermi: {intercept:.1f}")
print(f"Kulmakertoimen keskivirhe: {TÄYDENNÄ:.1f}")
```
