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
width: 250
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
width: 280
name: aaltoai
align: center
---
Aalto AI Assistant, valittuna GPT 5.5 -kielimalli (lokakuu 2026).
```

### Ensimmäinen yritys

Pyydetään kielimallia kirjoittamaan meille haluamamme funktio:

    Kirjoita Python-funktio, joka laskee kiteisen aineen alkeiskopin tilavuuden. 
    Funktio saa parametreinä yksikkökopin sivujen pituudet a,b,c ja niiden väliset 
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
width: 500
name: aaltoai-esim1
align: center
---
Kuvakaappus mallin tulosteesta (kaavan muotoilu menee pieleen, koska kertomerkit muuttuvat pallukoiksi).
```
