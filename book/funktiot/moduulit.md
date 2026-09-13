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
# Moduulit
Suuremmat ohjelmakokonaisuudet on aina parasta jakaa *moduuleiksi*. Moduulien avulla ohjelman rakenne pysyy paremmin
hallinnassa ja moduuleja voi käyttää helposti uudelleen toisissa ohjelmissa.

Käytetään esimerkkinä moduulia *ideaalikaasu*, joka käytännössä olisi siis alla oleva koodi tallennettuna tiedostoon
[*ideaalikaasu.py*](./ideaalikaasu.py):
```
# Moduuli ideaalikaasu:
# Apufunktioita ideaalikaasulle
# pV = nRT

# Moduuli määrittelee myös kaasuvakion R
# Lähde NIST CODATA2018: https://physics.nist.gov/cgi-bin/cuu/Value?r
R = 8.314462618 # J K^-1 mol^-1 

# Moduuli määrittelee neljä funktiota
def ratkaise_paine(V, n, T):
    return n * R * T / V
    
def ratkaise_tilavuus(p, n, T):
    return n * R * T / p

def ratkaise_ainemaara(p, V, T):
    return p * V / (R * T)

def ratkaise_lampotila(p, V, n):
    return p * V / (n * R)
```
Luodaan moduulin [*ideaalikaasu.py*](https://github.com/elina-ruha/CHEM-ohjelmointikurssikirja-test/blob/main/book/funktiot/ideaalikaasu.py) kanssa samaan hakemistoon tiedosto 
[*testi.py*](https://github.com/elina-ruha/CHEM-ohjelmointikurssikirja-test/blob/main/book/funktiot/testi.py), jossa hyödynnämme *ideaalikaasu*-moduulia **import**-avainsanan avulla:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
# Tuodaan koko ideaalikaasu-moduuli ohjelman testi.py käyttöön
import ideaalikaasu
# ideaalikaasu-moduulin funktioiden eteen pitää lisätä viittaus "ideaalikaasu."
p = ideaalikaasu.ratkaise_paine(0.002, 0.01, 300) # Parametrit V, n, T
print(f"Paine: {p:.3f} Pa")
```
Toinen tapa on tuoda *ideaalikaasu*-moduulista vain tietyt funktiot ja muuttujat [*testi.py*](https://github.com/elina-ruha/CHEM-ohjelmointikurssikirja-test/blob/main/book/funktiot/testi.py)-ohjelman
käyttöön. Tähän käytetään käskyä **from** MODUULI **import** FUNKTIOT
```{code-cell} ipython3
# Tuodaan tietyt funktiot (ja/tai muuttujat) ohjelman testi.py käyttöön
from ideaalikaasu import ratkaise_paine, ratkaise_tilavuus, R
# Nyt meidän ei tarvitse käyttää "ideaalikaasu."-viittausta
p = ratkaise_paine(0.002, 0.01, 300) # Parametrit V, n, T
V = ratkaise_tilavuus(101325, 0.01, 300) # Parametrit p, n, T
print(f"Paine: {p:.3f} Pa")
print(f"Tilavuus: {V:.5f} m^3")
print(f"Kaasuvakion R arvo on {R:.8f} J/mol K")
```
Vähänkin laajemissa ohjelmakokonaisuuksissa kannattaa miettiä ohjelman pilkkomista helpommin ylläpidettäviin ja 
uudelleenkäytettäviin moduuleihin.

**import**-käskyyn voi yhdistää **as**-avainsanan, jolloin ohjelmaan tuotavan moduulin nimeä voi vaikkapa lyhentää. 
Käsky on tällöin **import** MODUULI **as** LYHENNE:
```{code-cell} ipython3
import ideaalikaasu as ik
p = ik.ratkaise_paine(0.002, 0.01, 300) # Parametrit V, n, T
print(p)
```
:::::{card} Tehtävä
Täydennetään puutuvat kohdat koodista rivi riviltä niin, että 
  1) ohjelmaan tuodaan moduuli *hiilivety* ja käytetään sieltä funktiota *laske_CO2*
  2) phjelmaan tuodaan funktio *kysy_suure* moduulista *apufunktiot* ja käytetään kyseistä funktiota.
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Rivi 1:
``` ipython3
import TÄYDENNÄ
```
---
[ ] math
> Yritä uudelleen!
[ ] laske_CO2
> Yritä uudelleen!
[x] hiilivety
> Oikein!
[ ] kysy_suure
> Yritä uudelleen!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Rivi 2:
``` ipython3
from TÄYDENNÄ import TÄYDENNÄ
```
---
[ ] hiilivety ja laske_CO2
> Yritä uudelleen!
[ ] ideaalikaasu ja ratkaise_paine
> Yritä uudelleen!
[ ] hiilivety ja apufunktiot
> Yritä uudelleen!
[x] kysy_suure ja apufunktiot
> Oikein!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Rivi 3:
``` ipython3
m_CH4 = TÄYDENNÄ("Anna poltettavan metaanin massa (g):")
```
---
[x] kysy_suure
> Oikein!
[ ] hiilivety
> Yritä uudelleen!
[ ] lakse_CO2
> Yritä uudelleen!
[ ] apufunktiot
> Yritä uudelleen!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Rivi 4:
``` ipython3
m_CO2 = TÄYDENNÄ.laske_CO2(m_CH4)
```
---
[ ] apufunktiot
> Yritä uudelleen!
[x] hiilivety
> Oikein!
[ ] math
> Yritä uudelleen!
[ ] kysy_suure
> Yritä uudelleen!
---
::::
:::::
