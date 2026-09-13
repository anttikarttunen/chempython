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
hiilivedyt = {
              "Metaani": {"moolimassa": 16.04, "sulamispiste_C": -182},
              "Etaani": {"moolimassa": 30.07, "sulamispiste_C": -183},
              "Propaani": {"moolimassa": 44.10, "sulamispiste_C": -188}
             }
print(hiilivedyt["Propaani"]["sulamispiste_C"])
```
---
[ ] -182
> Yritä uudelleen!
[ ] -183
> Yritä uudelleen!
[ ] 44.10
> Yritä uudelleen!
[x] -188
> Oikein!
---
::::
:::::
