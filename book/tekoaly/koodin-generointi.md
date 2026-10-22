---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
---

# Koodin generoiminen

Tämän osion esimerkeissä käytetään GPT 5.5 -mallia, joka on lokakuussa 2026 edistynein saatavilla oleva suuri kielimalli [Aalto AI Assistant](https://ai.aalto.fi/) -palvelussa. Palvelu on Aalto-yliopiston opiskelijoiden ja henkilökunnan käytettävissä. Esimerkit toimivat todennäköisesti yhtä hyvin OpenAI:n ChatGPT-palvelussa tai millä tahansa vuoden 2025 jälkeen julkistetulla suurella kielimallilla.

## Kiteisen aineen yksikkökopin tilavuuden laskeminen

Pyydetään ensimmäisessä esimerkissä kielimallia kirjoittamaan Python-funktio, joka laskee kiteisen aineen alkeiskopin tilavuuden. Alkeiskoppi on pienin toistuva yksikkö, josta [kiderakenne](https://fi.wikipedia.org/wiki/Kiderakenne) muodostuu. Alkeiskopin synonyyminä käytetään usein yksikkökoppia, mutta ne eivät ole tarkkaan ottaen sama asia (englanniksi kyseessä on käsitteiden *primitive cell* ja *unit cell* ero). Tässä esimerkissä meille kuitenkin riittää tieto, että kaikkien seitsemän kidesysteemin alkeiskoppi on muodoltaan alla olevassa kuvassa esitetty suuntaissärmiö (engl. parallelepiped). 

```{figure} ../figures/sarmio.svg
---
width: 300
name: sarmio
align: center
---
Suuntaissärmiö (Kuva: [Wikimedia Commons](https://commons.wikimedia.org/w/index.php?curid=119762942) / Ag2gaeh, CC BY-SA 4.0.
```

Suuntaissärmiön muotoisen alkeiskopin tilavuus voidaan laskea [kaavalla](https://en.wikipedia.org/wiki/Parallelepiped)

$$
V=abc \sqrt{1 + 2\cos(\alpha)\cos(\beta)\cos(\gamma) - \cos^2(\alpha)-\cos^2(\beta) - \cos^2(\gamma)},
$$

missä $a$, $b$ ja $c$ ovat alkeiskopin särmien pituudet ja $\alpha$, $\beta$ ja $\gamma$ ovat särmien väliset kulmat.

Avataan [Aalto AI Assistant](https://ai.aalto.fi/) ja valitaan käyttöön GPT 5.5 -kielimalli:

```{figure} ../figures/aaltoai.png
---
width: 750
name: aaltoai
align: center
---
Aalto AI Assistant, valittuna GPT 5.5 -kielimalli (lokakuu 2026).
```

### Ensimmäinen versio

Pyydetään kielimallia kirjoittamaan meille haluamamme funktio:

    Kirjoita Python-funktio, joka laskee kiteisen aineen alkeiskopin tilavuuden. 
    Funktio saa parametreinä yksikkökopin särmien pituudet a,b,c ja niiden väliset 
    kulmat alpha, beta ja gamma. 

Olisimme voineet määritellä ohjeet huomattavasti tarkemminkin, mutta katsotaan, mikä on lopputulos näillä ohjeilla:

```
import math

def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma, degrees=True):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a, b, c : float
            Yksikkökopin sivujen pituudet.
        alpha, beta, gamma : float
            Sivujen väliset kulmat. Oletuksena asteina.
        degrees : bool
            Jos True, kulmat annetaan asteina.
            Jos False, kulmat annetaan radiaaneina.

    Palauttaa:
        float
            Alkeiskopin tilavuus.
    """

    if degrees:
        alpha = math.radians(alpha)
        beta = math.radians(beta)
        gamma = math.radians(gamma)

    termi = (
        1
        + 2 * math.cos(alpha) * math.cos(beta) * math.cos(gamma)
        - math.cos(alpha) ** 2
        - math.cos(beta) ** 2
        - math.cos(gamma) ** 2
    )

    return a * b * c * math.sqrt(termi)
```

Lisäksi malli antaa esimerkin funktion käytöstä ja kertoo, mitä kaavaa se käytti tilavuuden laskemiseen:
```{figure} ../figures/esim1.png
---
width: 700
name: aaltoai-esim1
align: center
---
Kuvakaappus mallin tulosteesta (kaavan muotoilu menee pieleen, koska kertomerkit muuttuvat pallukoiksi).
```

Funktion ensimmäinen versio näyttää asialliselta. Malli lisäsi funktion alkuun dokumentaation funktion tarkoituksesta, parametreistä ja paluuarvosta. Malli käytti tilavuuden laskemiseen oikeaa kaavaa, vaikka emme määritelleet kaavaa. Yksi merkittävä ongelma tässä ensimmäisessä versiossa on, että funktio ei lainkaan tarkasta, että sille annetut parametrit ovat kelvollisia. Toisaalta emme tätä pyytäneetkään, joten malli jätti sen tekemättä.

Meidän pitää luonnollisesti tarkistaa vielä testeillä, että funktio toimii oikein. Ennen sitä on kuitenkin hyvä yksinkertaistaa funktion toimintaa ja toisaalta lisää tarkistukset epäfysikaalisten parametrien varalta. 

### Toinen versio

Tarkennetaan kielimallin ohjeistusta:

    Kirjoita Python-funktio, joka laskee kiteisen aineen alkeiskopin tilavuuden. 
    Funktion tulee täyttää seuraavat vaatimukset:
    1) Funktio saa parametreinä kuusi liukulukua: yksikkökopin särmien pituudet 
       a, b, c ja niiden väliset kulmat alpha, beta, gamma. 
    2) Funktion alussa täytyy olla dokumentaatio, jossa kerrotaan funktion tarkoitus,
       parametrit ja paluuarvo. Määrittele parametrien ja paluuarvon tyyppi 
       dokumentaatiossa, älä lisää tyyppejä funktion määritelmään.
    2) Särmien pituudet voivat olla missä pituusyksikössä tahansa. 
    3) Kulmat pitää antaa asteina.
    4) Funktion täytyy tarkastaa, tuottavatko sille annetut särmien pituudet ja kulmat 
       kelvollisen alkeiskopin. Virhetilanteessa funktio tulostaa sopivan virheilmoituksen 
       ja palauttaa arvon -1.

Voisimme käyttää virhetilanteiden käsittelyyn poikkeuksia, mutta jätetään ne pois tästä esimerkistä.

Lopputulos on paljon ensimmäistä versiota pidempi:

```
import math


def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden annetuista sivujen pituuksista
    ja niiden välisistä kulmista.

    Parametrit:
        a (float): Alkeiskopin sivun a pituus.
        b (float): Alkeiskopin sivun b pituus.
        c (float): Alkeiskopin sivun c pituus.
        alpha (float): Sivujen b ja c välinen kulma asteina.
        beta (float): Sivujen a ja c välinen kulma asteina.
        gamma (float): Sivujen a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samassa pituusyksikössä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: Sivujen pituuksien täytyy olla positiivisia.")
        return -1

    if alpha <= 0 or beta <= 0 or gamma <= 0:
        print("Virhe: Kulmien täytyy olla suurempia kuin 0 astetta.")
        return -1

    if alpha >= 180 or beta >= 180 or gamma >= 180:
        print("Virhe: Kulmien täytyy olla pienempiä kuin 180 astetta.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    cos_alpha = math.cos(alpha_rad)
    cos_beta = math.cos(beta_rad)
    cos_gamma = math.cos(gamma_rad)

    juuri_lauseke = (
        1
        - cos_alpha ** 2
        - cos_beta ** 2
        - cos_gamma ** 2
        + 2 * cos_alpha * cos_beta * cos_gamma
    )

    if juuri_lauseke <= 0:
        print("Virhe: Annetut sivujen pituudet ja kulmat eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(juuri_lauseke)
```
Huomaa, miten neliöjuuren sisällä oleva muuttuja `juuri_lauseke` lasketaan tässä toisessa versiossa eri järjestyksessä kuin ensimmäisessä versiossa oleva muuttuja `termi`. Laskun lopputulos on sama, mutta tällaisia muutoksia koodin eri versioihin voi tulla, jos mallia ei määrää tekemään asioita tietyllä tavalla.

### Kolmas versio

Tiivistetään vielä funktiota. Annetaan seuraava komento samassa keskustelussa (malli muistaa aiemman keskustelun, jos et ole sulkenut keskustelua):

    Älä tarkista kulmien kelvollisuutta funktion alussa. Riittää, kun
    tarkistat, että neliöjuuren sisällä oleva lauseke on suurempi kuin 0.

Lopptulos on hieman lyhyempi funktio:

```
import math


def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden annetuista sivujen pituuksista
    ja niiden välisistä kulmista.

    Parametrit:
        a (float): Alkeiskopin sivun a pituus.
        b (float): Alkeiskopin sivun b pituus.
        c (float): Alkeiskopin sivun c pituus.
        alpha (float): Sivujen b ja c välinen kulma asteina.
        beta (float): Sivujen a ja c välinen kulma asteina.
        gamma (float): Sivujen a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samassa pituusyksikössä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: Sivujen pituuksien täytyy olla positiivisia.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    cos_alpha = math.cos(alpha_rad)
    cos_beta = math.cos(beta_rad)
    cos_gamma = math.cos(gamma_rad)

    juuri_lauseke = (
        1
        - cos_alpha ** 2
        - cos_beta ** 2
        - cos_gamma ** 2
        + 2 * cos_alpha * cos_beta * cos_gamma
    )

    if juuri_lauseke <= 0:
        print("Virhe: Annetut arvot eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(juuri_lauseke)
```

Yhteenvetona voidaan todeta, että tässä esimerkissä käytetty malli GPT 5.5 tuotti asiallisen koodin jo varsin vähäisillä ohjeilla, mutta toisaalta käyttäjän piti olla hereillä ja lisätä esimerkiksi virhetarkastelu. Koodissa oli myös jonkin verran lyhentämisen varaa.

### Testien generoiminen

Lopuksi on vuorossa vielä erittäin tärkeä vaihe, eli luodaan testejä, joilla funktion toimintaa voidaan tarkastella. Tässä esimerkissä testejä on kaksi, mutta hyvä minimi voisi olla, että jokaiselle kidesysteemille on yksi testi ja lisäksi muutama erilainen virhetilanne.

    Kirjoita funktiolle testit kahdelle kiteiselle aineelle: 
    1) Cu2O alkeiskopin särmien pituudet ovat a=b=c=4.267 Å ja kaikki kulmat ovat 
       90 astetta. Alkeiskopin tilavuus on 77.69 Å^3.
    2) Violetin fosforin alkeiskopin särmien pituudet ovat a = 9.21 Å, b = 9.15 Å, 
       c = 22.6 Å. Kulmat ovat alpha = 90, beta = 106.1, gamma = 90. Alkeiskopin 
       tilavuus on 1829.84 Å^3.

    Kirjoita myös kaksi testiä virheellisille parametreille:
    1) Yhden särmän pituus on negatiivinen.
    2) Kulmat eivät muodosta kelvollista yksikkökoppia.
    
