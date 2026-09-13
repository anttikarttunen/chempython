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
# Sisäkkäiset listat
Pythonin erilaisia tietorakenteita voi käyttää myös sisäkkäin. Tutustutaan ensiksi listoja sisältäviin listoihin.

## Lista, jonka jokainen alkio on toinen lista:
```{code-cell} ipython3
:tags: ["auto-execute-page"]
# Määritellään lista, jossa kaksi alkiota. Kukin alkio on kolmen alkion lista.
lista = [[10, 20, 30], [1, 2, 3]]
print(lista[0][0])
print(lista[1][2])
```
Eli merkinnässä `lista[1][2]` ensimmäinen indeksi [1] viittaa ulomman listan toiseen alkioon [1, 2, 3] (indeksointi alkaa
nollasta!). Toinen indeksi [2] viittaa sisemmän listan kolmanteen alkioon (indeksointi alkaa nollasta!).

Otetaan käytännöllisempi esimerkki. Kuvataan kemiallista yhdistettä listalla:
- Listan jokainen alkio on toinen lista
- Tämä lista sisältää alkuaineen symbolin ja sen määrän yhdisteessä
```{code-cell} ipython3
yhdiste_1 = [['C', 2], ['H', 6]]
yhdiste_2 = [['Ca', 1], ['Cl', 2]]

# Lisätään nyt kaikki yhdisteet yhteen listaan ja tulostetaan
yhdisteet = [yhdiste_1, yhdiste_2]
print(yhdisteet)
```
### Laajempi esimerkki
```{code-cell} ipython3
# Käydään läpi yhdisteet, tulostetaan ne ja etsitään hiilivedyt
yhdisteet = [[['C', 2], ['H', 6]], [['Ca', 1], ['Cl', 2]]]
for yhdiste in yhdisteet: 
    # "yhdiste" on nyt esim. [['C', 2], ['H', 6]]    
    # Alustetaan muuttujat ennen sisempää for-silmukkaa
    yhdisteen_kaava = ""
    on_hiili = on_vety = False 
    # Käydään läpi kaikki yhdisteen alkuaineet
    for alkuaine in yhdiste: 
        # "alkuaine" on nyt esim. ['C', 2]
        # Tulostetaan määrä vain, jos se on > 1
        if alkuaine[1] > 1:
            maara = str(alkuaine[1])
        else:
            maara = ""
        yhdisteen_kaava += alkuaine[0] + maara

        # Tarkistetaan, onko alkuaine hiili tai vety
        if alkuaine[0] == 'C':
            on_hiili = True
        elif alkuaine[0] == 'H':
            on_vety = True

    # Tulostetaan yhdisteen molekyylikaava
    if len(yhdiste) == 2 and on_hiili and on_vety:
        hiilivety_str = "on hiilivety"
    else:
        hiilivety_str = ""
    print("Yhdiste:", yhdisteen_kaava, hiilivety_str)
```
## Matriisit listojen avulla
Sisäkkäisillä listoilla voisi periaatteessa kuvata matriiseja:
```{code-cell} ipython3
matriisi = [[2, 4], 
            [5, 6]]
# Tulostetaan 1. rivin 2. alkio (indeksointi nollasta!)        
print(matriisi[0][1])
```
Käytännössä matriisilaskentaan käytetään kuitenkin *NumPy*-kirjaston *array*-tyyppiä, johon tutustutaan luvussa *NumPy ja Matplotlib*.

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
