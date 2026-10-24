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
# Kuvaajien luominen datapisteistä

Olemme tällä kurssilla opetelleet kuvaajien piirtämistä Matplotlib-kirjaston avulla. Kuvaajien piirtäminen on varsin suoraviivaista ja mekaanista. Jos sinulla on datatiedosto, jonka haluat visualisoida nopeasti, kielimallilla voi varsin kätevästi generoida koodin, joka luo datatiedostosta kuvaajan.

## Titrauskäyrän piirtäminen

Otetaan käytännön esimerkki, jossa käytetään datatiedostoa [titraus.csv](./titraus.csv). Tiedoston sisältö näyttää tältä:
```
# 50.0 mL 0.100 M HCl titrataan 0.200 M NaOH-liuoksella
#V_NaOH_ml,pH
0.00,1.00
5.00,1.14
10.0,1.30
15.0,1.51
20.0,1.85
22.0,2.08
24.0,2.57
25.0,7.00
26.0,11.42
28.0,11.89
30.0,12.10
35.0,12.37
40.0,12.52
45.0,12.62
50.0,12.70

```

Tiedosto sisältää siis 15 datapistettä koejärjestelystä, jossa 50.0 mL 0.100 M HCl titrataan 0.200 M NaOH-liuoksella. Jokaisesta datapisteestä on kirjattu tiedostoon käytetty NaOH-liuoksen määrä millilitroina ja liuoksen pH. Tiedot on erotettu toisistaan pilkulla, eli kyseessä on ns. CSV-tiedosto (Comma-Separated Values)

Pyydetään kielimallia luomaan tiedostosta kuvaaja (Aalto AI Assistant / GPT 5.5, lokakuu 2026):

    Liitteenä oleva CSV-muotoinen tiedosto titraus.csv sisältää datat kokeesta, jossa 50.0 mL 0.100 M HCl 
    titrataan 0.200 M NaOH-liuoksella. Kirjoita Python-skripti, joka lataa datat tiedostosta 
    np.loadtxt-funktiolla ja piirtää kuvaajan, jossa on x-akselilla v(NaOH) yksiköissä ml ja y-akselilla pH. 
    Merkitse datapisteet mustilla palloilla.

Kielimalli tuotti alla olevan koodin. Näet kuvaajan ajamalla koodin.

```{code-cell} ipython3
:tags: ["auto-execute-page"]
import numpy as np
import matplotlib.pyplot as plt

# Ladataan data CSV-tiedostosta
# comments="#" ohittaa kommenttirivit ja otsikkorivin
data = np.loadtxt("titraus.csv", delimiter=",", comments="#")

# Erotetaan sarakkeet
v_naoh = data[:, 0]  # NaOH:n tilavuus, ml
ph = data[:, 1]      # pH

# Piirretään kuvaaja
plt.plot(v_naoh, ph, "ko", label="Mittauspisteet")

# Akselien nimet
plt.xlabel("V(NaOH) / ml")
plt.ylabel("pH")

# Otsikko ja ruudukko
plt.title("HCl:n titraus NaOH-liuoksella")
plt.grid(True)

# Näytetään kuvaaja
plt.show()
```

Kielimallin generoima koodi on varsin selkeä. Jos kokeilit koodin generointia itse, sait todennäköisesti tuloksena vähän erilaisen koodin. Kielimallit saattavat esimerkiksi käyttää `np.loadtxt`-funktion `skiprows`-parametria kommenttirivien ohittamiseen, vaikka `comments`-parametri on järkevämpi valinta. 

Pyydetään kuitenkin kielimallia muokkaamaan koodia:

    - Lisää kuvaajaan ohut punainen viiva, joka yhdistää pisteet.
    - Lisää kuvaajan otsikkoon titrauksen yksityiskohdat liuoksista. 
    - Siirrä piste (0,0) kuvaajan vasempaan alakulmaan. 
    - Älä piirrä ristikkoa taustalle.

Kielimalli tuottaa alla olevan koodin. Näet kuvaajan ajamalla koodin.

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

# Ladataan data CSV-tiedostosta
# Tiedostossa: 50.0 mL 0.100 M HCl titrataan 0.200 M NaOH-liuoksella [1]
data = np.loadtxt("titraus.csv", delimiter=",", comments="#")

# Erotetaan sarakkeet
v_naoh = data[:, 0]  # NaOH:n tilavuus, ml
ph = data[:, 1]      # pH

# Piirretään ohut punainen viiva pisteiden väliin
plt.plot(v_naoh, ph, color="red", linewidth=0.8)

# Merkitään datapisteet mustilla palloilla
plt.plot(v_naoh, ph, "ko")

# Akselien nimet
plt.xlabel("V(NaOH) / ml")
plt.ylabel("pH")

# Otsikko titrauksen yksityiskohdilla
plt.title("50.0 mL 0.100 M HCl titrataan 0.200 M NaOH-liuoksella")

# Siirretään piste (0,0) kuvaajan vasempaan alakulmaan
plt.xlim(left=0)
plt.ylim(bottom=0)

# Ei piirretä taustaristikkoa
plt.grid(False)

# Näytetään kuvaaja
plt.show()
```

Kuvaaja näyttää asialliselta, mutta kokeillaan vielä korvata punainen pisteitä yhdistävä viiva ideaalin näköisellä titrauskäyrällä:

    Tee punaisesta viivasta ideaalin titrauskäyrän näköinen. Lisää myös selite (legend).

Nyt koodi pitenee merkittävästi, koska kielimalli lisäsi koodiin osuuden, joka laskee ideaalin titrauskäyrän. Näet kuvaajan ajamalla koodin.

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

# Ladataan kokeellinen data tiedostosta
data = np.loadtxt("titraus.csv", delimiter=",", comments="#")

# Erotetaan sarakkeet
v_naoh_data = data[:, 0]  # ml
ph_data = data[:, 1]

# Titrauksen lähtötiedot
V_hcl = 50.0e-3   # l
c_hcl = 0.100     # mol/l
c_naoh = 0.200    # mol/l

# Ainemäärä HCl
n_hcl = c_hcl * V_hcl

# Teoreettista käyrää varten tiheä tilavuusasteikko
v_naoh_ml = np.linspace(0, 50.0, 1000)
v_naoh_l = v_naoh_ml * 1e-3

# NaOH:n ainemäärä
n_naoh = c_naoh * v_naoh_l

# Kokonaistilavuus
V_total = V_hcl + v_naoh_l

# Lasketaan ideaalinen pH
ph_ideal = np.zeros_like(v_naoh_ml)

for i in range(len(v_naoh_ml)):
    if n_naoh[i] < n_hcl:
        h_conc = (n_hcl - n_naoh[i]) / V_total[i]
        ph_ideal[i] = -np.log10(h_conc)
    elif n_naoh[i] > n_hcl:
        oh_conc = (n_naoh[i] - n_hcl) / V_total[i]
        poh = -np.log10(oh_conc)
        ph_ideal[i] = 14.0 - poh
    else:
        ph_ideal[i] = 7.0

# Piirretään ideaalinen titrauskäyrä ohuella punaisella viivalla
plt.plot(
    v_naoh_ml,
    ph_ideal,
    color="red",
    linewidth=0.8,
    label="Ideaalinen titrauskäyrä"
)

# Merkitään kokeelliset datapisteet mustilla palloilla
plt.plot(
    v_naoh_data,
    ph_data,
    "ko",
    label="Kokeelliset datapisteet"
)

# Akselien nimet
plt.xlabel("V(NaOH) / ml")
plt.ylabel("pH")

# Otsikko titrauksen yksityiskohdilla
plt.title("50.0 mL 0.100 M HCl titrataan 0.200 M NaOH-liuoksella")

# Piste (0,0) vasempaan alakulmaan
plt.xlim(left=0)
plt.ylim(bottom=0)

# Ei taustaristikkoa
plt.grid(False)

# Lisätään selite
plt.legend()

# Näytetään kuvaaja
plt.show()
```

Kielimallin generoimassa koodissa olisi tiivistämisen varaa, mutta ideaali titrauskäyrä on sinänsä OK.

Kannattiko kuvaaja sitten tässä tapauksessa luoda kielimallilla? Kielimalli loi asiallisen kuvaajan parilla pyynnöllä, mutta todennäköisesti kopioimalla jonkin vanhan mallipohjan ja muokkaamalla sitä koodin olisi saanut luotua varsin nopeasti. Ideaalin titrauskäyrän luominen sujui kielimallilta varsin näppärästi.

:::{admonition} Huomio!
:class: attention
Kannattaa  huomioida, että titrausdatat lähetettiin kielimallin kehittäjän palvelimelle (OpenAI). Eli jos kyseessä olisi ollut jokin tärkeä tutkimusdata, nyt data olisi myös OpenAI:n hallussa. 
:::

## Datapisteiden poimiminen kuvaajasta

Kielimalleihin on kytketty myös työkaluja, jotka pystyvät lukemaan kuvia ja poimimaan niistä dataa. Käytetään esimerkkinä seuraavaa [Wikipediasta](https://en.wikipedia.org/wiki/Titration_curve) löytyvää kuvaa:

```{figure} ../figures/ai_titraus_kuva.png
---
width: 500
name: ai_titraus
align: center
---
Heikon hapon titraaminen vahvalla emäksellä (Kuva: [Wikimedia Commons](https://commons.wikimedia.org/w/index.php?curid=3967359) / JWSchmidt, CC BY-SA 3.0.
```

Annetaan kielimallille seuraava komento ja liitetään kuva mukaan (Aalto AI Assistant / GPT 5.5, lokakuu 2026):

    Poimi datapisteet oheisesta kuvaajasta. Kirjoita Python-koodi, joka piirtää 
    näistä datapisteistä titrauskäyrän. Käytä Numpy- ja Matplotlib-kirjastoja. 
    Älä käytä Pandas-kirjastoa.

Kielsin Pandas-kirjaston, koska ensimmäisissä testeissäni kielimalli tunki sitä koko ajan mukaan. Kielimalli sai luettua datapisteet kuvaajasta ja liitti mukaan myös varoituksen:

	Alla on kuvaajasta likimääräisesti poimitut datapisteet oksaalihapon titraukselle NaOH:lla. 
    Pisteet eivät ole alkuperäistä mittausdataa, vaan kuvaajasta arvioituja arvoja.

Tuloksena on alla oleva koodi, jonka ajamalla näet kuvaajan

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

# Kuvaajasta likimääräisesti poimitut datapisteet
# x = lisätyn NaOH:n tilavuus millilitroina
# y = pH

volume_ml = np.array([
    0, 2, 4, 6, 8, 10, 12, 13, 14, 15,
    16, 17, 18, 19, 20, 21, 22, 23, 24, 25,
    26, 27, 28, 29, 29.3, 29.5, 29.7, 29.8, 29.9,
    30.0, 30.05, 30.1, 30.2, 30.4, 30.6, 31,
    32, 33, 34, 35, 36, 38, 40, 42
])

ph = np.array([
    1.1, 1.2, 1.25, 1.35, 1.5, 1.7, 1.95, 2.1, 2.4, 2.65,
    2.85, 3.05, 3.25, 3.4, 3.45, 3.55, 3.75, 3.85, 3.95, 4.1,
    4.25, 4.45, 4.65, 4.9, 5.2, 5.6, 6.3, 7.1, 8.5,
    10.0, 10.9, 11.3, 11.6, 11.8, 11.95, 12.1,
    12.3, 12.4, 12.5, 12.55, 12.65, 12.8, 12.9, 12.9
])

# Piirretään titrauskäyrä
plt.figure(figsize=(8, 6))

plt.plot(volume_ml, ph, marker='o', linestyle='-', color='darkgreen',
         markersize=4, linewidth=1.8, label='Poimitut datapisteet')

plt.title('Titrauskäyrä: oksaalihappo / NaOH')
plt.xlabel('Lisätyn NaOH:n tilavuus (ml)')
plt.ylabel('pH')

plt.xlim(0, 45)
plt.ylim(0, 14)

plt.grid(True, linestyle='--', alpha=0.5)
plt.legend()

plt.show()
```

Kuvaajan ulkonäköä voi muuttaa antamalla lisää komentoja. Esimerkiksi:

	Merkitse datapisteet vähän isommilla mustilla ympyröillä. Piirrä viiva punaisella.

Tuloksena on alla oleva koodi, jonka ajamalla näet kuvaajan

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

# Kuvaajasta likimääräisesti poimitut datapisteet
volume_ml = np.array([
    0, 2, 4, 6, 8, 10, 12, 13, 14, 15,
    16, 17, 18, 19, 20, 21, 22, 23, 24, 25,
    26, 27, 28, 29, 29.3, 29.5, 29.7, 29.8, 29.9,
    30.0, 30.05, 30.1, 30.2, 30.4, 30.6, 31,
    32, 33, 34, 35, 36, 38, 40, 42
])

ph = np.array([
    1.1, 1.2, 1.25, 1.35, 1.5, 1.7, 1.95, 2.1, 2.4, 2.65,
    2.85, 3.05, 3.25, 3.4, 3.45, 3.55, 3.75, 3.85, 3.95, 4.1,
    4.25, 4.45, 4.65, 4.9, 5.2, 5.6, 6.3, 7.1, 8.5,
    10.0, 10.9, 11.3, 11.6, 11.8, 11.95, 12.1,
    12.3, 12.4, 12.5, 12.55, 12.65, 12.8, 12.9, 12.9
])

# Piirretään titrauskäyrä
plt.figure(figsize=(8, 6))

plt.plot(
    volume_ml,
    ph,
    color='red',
    linestyle='-',
    linewidth=1.8,
    marker='o',
    markersize=7,
    markerfacecolor='black',
    markeredgecolor='black',
    label='Poimitut datapisteet'
)

plt.title('Titrauskäyrä: oksaalihappo / NaOH')
plt.xlabel('Lisätyn NaOH:n tilavuus (ml)')
plt.ylabel('pH')

plt.xlim(0, 45)
plt.ylim(0, 14)

plt.grid(True, linestyle='--', alpha=0.5)
plt.legend()

plt.show()
```

Kielimalli sai siis poimittua datat kuvatiedostosta ja nyt niistä voi piirtää helposti uusia kuvaajia. Nyt olisi myös helppoa lisätä tämä data toiseen kuvaajaan, jossa olisi esimerkiksi omat mittaustuloksesi samalle kokeelle. Näin voisit verrata omia tuloksiasi toisten tuloksiin.

:::{admonition} Huomio!
:class: attention
Datojen poimimiseen kuvista liittyy sama huomio kuin edelliseen esimerkkiin: tiedot menevät myös kielimallin kehittäjän palvelimelle. Älä siis anna kielimallille kuvatiedostoja, joiden levittämiseen sinulla ei ole oikeuksia. Tässä tapauksessa kuva oli Wikipediasta ja avoimella lisessillä, joten kuva on takuuvarmasti jo kielimallin koulutusaineistossa.

Kielimallin poimimat datapisteet pitää myös tarkistaa erittäin huolellisesti vertaamalla alkuperäiseen kuvaan!
:::
