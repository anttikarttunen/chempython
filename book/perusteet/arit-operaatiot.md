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
# Aritmeettiset perusoperaatiot
Laskutoimituksia varten Python tarjoaa mm. seuraavat operaatiot:
| Operaattori | Operaatio | Kokeile Python-konsolissa |
| :---: | :---: | :---: |
| + | Yhteenlasku | 5 + 5 |
| - | Vähennyslasku | 1000 - 4 |
| * | Kertolasku | 11 * 11 |
| / | Jakolasku | 11 / 5 (tulos = 2.2, eli **float**) |
| // | Katkaiseva jakolasku | 11 // 5 (tulos = 2 eli **int**) |
| % | Jakojäännös | 11 % 5 (tulos =1 eli **int**) |
| ** | Potenssiin korotus | 2 ** 4 |
| abs(x) | Itseisarvo | abs(4 - 16) |
## Laskujärjestyksen säätäminen sulkumerkeillä
Laskujärjestystä voi säätää kaarisulkeilla:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
print(2 ** (2 + 2))
print(2 ** 2 + 2)
```
## Merkkijonojen yhdistäminen toisiinsa
Merkkijonoja voi yhdistää yhteenlaskuoperaattorilla:
```{code-cell} ipython3
print("Lappeen" + "ranta")
```
## Merkkijonojen kertominen kokonaisluvuilla
Merkkijonon (string) saa kertoa kokonaisluvulla (int):
```{code-cell} ipython3
print("tip tap " * 5)
```

## Lyhennetyt laskuoperaatiot
Pythonissa voi käyttää myös lyhennettyjä laskuoperaatioita `+=`, `-=`, `*=` ja `/=`
``` ipython3
# Annetaan muuttujalle n alkuarvo
n = 10

# Sama kuin: n = n + 1 (eli n on nyt 11)
n += 1

# Sama kuin: n = n - 1 (eli n on nyt 10)
n -= 1

# Sama kuin: n = n * 2 (eli n on nyt 20)
n *= 2

# Sama kuin: n = n / 2 (eli n on nyt 10.0)
n /= 2
```
On puhdas makuasia, kumpaa muotoa haluaa käyttää, pitkää vai lyhyttä. Pitkä on aloittelijalle selkeämpi valinta. 

:::::{card} Tehtävä
::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Paljonko on 55 // 11?
---
[ ] 5.0
> Yritä uudelleen!
[ ] 0
> Yritä uudelleen!
[ ]1
> Yritä uudelleen!
[x] 5
> Oikein!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Paljonko on 12 % 9?
---
[ ] 1.3333...
> Yritä uudelleen!
[ ] 1
> Yritä uudelleen!
[ ] 0
> Yritä uudelleen!
[x] 3
> Oikein!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Paljonko on 3 ** (17 // 8)?
---
[ ] Epäkelpo laskutoimitus
> Yritä uudelleen!
[ ] 10.32
> Yritä uudelleen!
[ ] 243
> Yritä uudelleen!
[x] 9
> Oikein!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Paljonko on 2 ** (abs(1 - 2))?
---
[x] 2
> Oikein!
[ ] 1
> Yritä uudelleen!
[ ] $\sqrt{2}$
> Yritä uudelleen!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mikä on muuttujan *luku* arvo alla olevan ohjelman lopussa?
``` ipython3
luku = 28
luku += 15
luku -= 10
```
---
[ ] 28
> Yritä uudelleen!
[x] 33
> Oikein!
[ ] 15
> Yritä uudelleen!
[ ] 10
> Yritä uudelleen!
---
::::

::::{question}
:type: multiple-choice
:variant: single-select
:nocaption:
:columns: 1

Mikä on muuttujan *luku* arvo alla olevan ohjelman lopussa?
``` ipython3
luku = 5
luku *= 5
luku /= 10
```
---
[x] 2.5
> Oikein!
[ ] 0
> Yritä uudelleen!
[ ] 10
> Yritä uudelleen!
[ ] 10.0
> Yritä uudelleen!
---
::::
:::::
