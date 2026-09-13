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

## Sisäkkäiset sanakirjat
Sanakirjoja voi laittaa sisäkkäin:
```{code-cell} ipython3
tietokanta = {
              "C2H6": {"moolimassa": 30.07, "tiheys": 1.36},
              "NaCl": {"moolimassa": 58.44, "tiheys": 2.16}
             }
print("Etaanin tiheys on:", tietokanta["C2H6"]["tiheys"], "g/cm^3")
print("Ruokasuolan moolimassa on:", tietokanta["NaCl"]["moolimassa"], "g/mol")
```

## Listat sanakirjojen sisällä
Sanakirjan arvot voivat olla myös listoja. Alla olevassa esimerkissä sanakirjan avain on yhdisteen kemiallinen kaava ja sanakirjan arvo on lista, joka sisältää järjestyksessä yhdisteen jokaisen alkuaineen ja sen määrän kokonaislukuna.
```{code-cell} ipython3
yhdisteet = {"C2H6": ["C",  2,  "H", 6],
             "NaCl": ["Na", 1, "Cl", 1]
          # indeksi:   0    1    2   3
            }
print(yhdisteet["C2H6"])
print("Yhdisteessa C2H6 on", yhdisteet["C2H6"][3], "vetyatomia")
```

:::::{card} Tehtävä
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä alla oleva ohjelma tulostaa?
``` ipython3
G12 = [["H", "Li", "Na", "K", "Rb", "Cs"]
       ["Be", "Mg", "Ca", "Sr", "Ba"]]
print(G12[1])
```
---
[ ] Li
> Yritä uudelleen!
[ ] ['H', 'Li', 'Na', 'K', 'Rb', 'Cs']
> Yritä uudelleen!
[ ] Mg
> Yritä uudelleen!
[x] ['Be', 'Mg', 'Ca', 'Sr', 'Ba']
> Oikein!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä alla oleva ohjelma tulostaa?
``` ipython3
G12 = [["H", "Li", "Na", "K", "Rb", "Cs"]
       ["Be", "Mg", "Ca", "Sr", "Ba"]]
print(G12[1][1])
```
---
[ ] Virheellinen indeksi
> Yritä uudelleen!
[ ] [['Li'], ['Mg']]
> Yritä uudelleen!
[ ] Li
> Yritä uudelleen!
[x] Mg
> Oikein!
---
::::
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mitä alla oleva ohjelma tulostaa?
``` ipython3
G12 = [["H", "Li", "Na", "K", "Rb", "Cs"]
       ["Be", "Mg", "Ca", "Sr", "Ba"]]
print(G12[0][:3])
 ```
---
[ ] [['H'], ['Be', 'Mg', 'Ca']]
> Yritä uudelleen!
[ ] ['Be', 'Mg', 'Ca']
> Yritä uudelleen!
[x] ['H', 'Li', 'Na']
> Oikein!
[ ] ['H', 'Li', 'Na', 'K']
> Yritä uudelleen!
---
::::
:::::
