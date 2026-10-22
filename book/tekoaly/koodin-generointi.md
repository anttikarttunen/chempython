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

def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma, asteina=True):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a, b, c : float
            Yksikkökopin särmien pituudet.
        alpha, beta, gamma : float
            Särmien väliset kulmat.
        asteina : bool
            Jos True, kulmat annetaan asteina. Jos False, radiaaneina.

    Palauttaa:
        float
            Alkeiskopin tilavuus.
    """

    if asteina:
        alpha = math.radians(alpha)
        beta = math.radians(beta)
        gamma = math.radians(gamma)

    tilavuus = a * b * c * math.sqrt(
        1
        + 2 * math.cos(alpha) * math.cos(beta) * math.cos(gamma)
        - math.cos(alpha) ** 2
        - math.cos(beta) ** 2
        - math.cos(gamma) ** 2
    )

    return tilavuus
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

Jos kokeilet esimerkkiä itse, saamasi koodi voi näyttää erilaiselta kuin yllä! Kielimallit ovat tilastollisia malleja, joten samalla komennolla voi saada erilaisen tuloksen. Näin voi käydä varsinkin, jos tehtävänanto on avoimesti määritelty.

Vastaus voi riippua myös käytetystä kielestä. Jos saat suomen- tai ruotsinkielisillä käskyillä omituisia tuloksia, kannattaa yrittää englanniksi. Mallit sisältävät kaikkein eniten englanninkielistä koulutusaineistoa. Tässä tapauksessa toki tärkein kieli on Python.

Funktion ensimmäinen versio näyttää melko asialliselta. Malli lisäsi funktion alkuun dokumentaation funktion tarkoituksesta, parametreistä ja paluuarvosta. Malli käytti tilavuuden laskemiseen oikeaa kaavaa, vaikka emme määritelleet sitä. Yksi merkittävä ongelma tässä ensimmäisessä versiossa on, että funktio ei lainkaan tarkasta, että sille annetut parametrit ovat kelvollisia. Toisaalta emme tätä pyytäneetkään.

Meidän pitää luonnollisesti tarkistaa vielä testeillä, että funktio toimii oikein. Ennen sitä on kuitenkin hyvä  lisää tarkistukset epäfysikaalisten parametrien varalta ja selventää koodia. 

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
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a (float): Yksikkökopin särmän a pituus.
        b (float): Yksikkökopin särmän b pituus.
        c (float): Yksikkökopin särmän c pituus.
        alpha (float): Särmien b ja c välinen kulma asteina.
        beta (float): Särmien a ja c välinen kulma asteina.
        gamma (float): Särmien a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samoissa pituusyksiköissä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: särmien pituuksien täytyy olla positiivisia.")
        return -1

    if alpha <= 0 or beta <= 0 or gamma <= 0:
        print("Virhe: kulmien täytyy olla positiivisia.")
        return -1

    if alpha >= 180 or beta >= 180 or gamma >= 180:
        print("Virhe: kulmien täytyy olla pienempiä kuin 180 astetta.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    lauseke = (
        1
        + 2 * math.cos(alpha_rad) * math.cos(beta_rad) * math.cos(gamma_rad)
        - math.cos(alpha_rad) ** 2
        - math.cos(beta_rad) ** 2
        - math.cos(gamma_rad) ** 2
    )

    if lauseke <= 0:
        print("Virhe: annetut särmät ja kulmat eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(lauseke)
```

### Kolmas versio

Tiivistetään vielä funktiota. Annetaan seuraava komento samassa keskustelussa (malli muistaa aiemman keskustelun, jos et ole sulkenut keskustelua):

    Älä tarkista kulmien kelvollisuutta funktion alussa. Riittää, kun
    tarkistat, että neliöjuuren sisällä oleva lauseke on suurempi kuin 0.

Lopptulos on hieman lyhyempi funktio:

```
import math

def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a (float): Yksikkökopin särmän a pituus.
        b (float): Yksikkökopin särmän b pituus.
        c (float): Yksikkökopin särmän c pituus.
        alpha (float): Särmien b ja c välinen kulma asteina.
        beta (float): Särmien a ja c välinen kulma asteina.
        gamma (float): Särmien a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samoissa pituusyksiköissä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: särmien pituuksien täytyy olla positiivisia.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    lauseke = (
        1
        + 2 * math.cos(alpha_rad) * math.cos(beta_rad) * math.cos(gamma_rad)
        - math.cos(alpha_rad) ** 2
        - math.cos(beta_rad) ** 2
        - math.cos(gamma_rad) ** 2
    )

    if lauseke <= 0:
        print("Virhe: annetut särmät ja kulmat eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(lauseke)
```

Yhteenvetona voidaan todeta, että tässä esimerkissä käytetty malli GPT 5.5 tuotti asiallisen koodin jo varsin vähäisillä ohjeilla, mutta toisaalta käyttäjän piti ottaa vastuuta ja esimerkiksi vaatia virhetarkastelun lisäämistä. Koodissa oli myös jonkin verran lyhentämisen varaa.

### Testien generoiminen

Lopuksi on vuorossa vielä erittäin tärkeä vaihe, eli luodaan testejä, joilla funktion toimintaa voidaan tarkastella. Tässä esimerkissä testejä on vain kaksi, mutta hyvä minimi voisi olla, että jokaiselle kidesysteemille on yksi testi ja lisäksi varmistetaan, että erilaiset virhetilanteet hoituvat oikein. Testeissä käytetyt kiderakenteiden tiedot tulevat kokeellisesti mitatuista kiderakenteista, jotka olen noutanut kiderakennetietokannasta.

    Kirjoita funktiolle testit kahdelle kiteiselle aineelle: 
    1) Cu2O alkeiskopin särmien pituudet ovat a=b=c=4.267 Å ja kaikki kulmat ovat 
       90 astetta. Alkeiskopin tilavuus on 77.69 Å^3.
    2) Violetin fosforin alkeiskopin särmien pituudet ovat a = 9.21 Å, b = 9.15 Å, 
       c = 22.6 Å. Kulmat ovat alpha = 90, beta = 106.1, gamma = 90. Alkeiskopin 
       tilavuus on 1829.84 Å^3.

    Kirjoita myös kaksi testiä virheellisille parametreille:
    1) Yhden särmän pituus on negatiivinen.
    2) Kulmat eivät muodosta kelvollista yksikkökoppia.
    
Malli luo neljä testiä, jotka se lisää funktion määritelmän jälkeen. Huomaa, että testeissä käytetään `assert`-avainsanaa, jota emme tällä kurssilla ole hyödyntäneet. Tämä on standardi tapa testata koodia. Jos `assert`-avainsanan jälkeen kirjoitettu lauseke kuten `tilavuus == -1` ei toteudu, Python heittää poikkeuksen ja koodin suoritus keskeytyy

```
import math

def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a (float): Yksikkökopin särmän a pituus.
        b (float): Yksikkökopin särmän b pituus.
        c (float): Yksikkökopin särmän c pituus.
        alpha (float): Särmien b ja c välinen kulma asteina.
        beta (float): Särmien a ja c välinen kulma asteina.
        gamma (float): Särmien a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samoissa pituusyksiköissä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: särmien pituuksien täytyy olla positiivisia.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    lauseke = (
        1
        + 2 * math.cos(alpha_rad) * math.cos(beta_rad) * math.cos(gamma_rad)
        - math.cos(alpha_rad) ** 2
        - math.cos(beta_rad) ** 2
        - math.cos(gamma_rad) ** 2
    )

    if lauseke <= 0:
        print("Virhe: annetut särmät ja kulmat eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(lauseke)


def test_alkeiskopin_tilavuus():
    # 1) Cu2O: a = b = c = 4.267 Å, alpha = beta = gamma = 90°
    tilavuus = alkeiskopin_tilavuus(4.267, 4.267, 4.267, 90.0, 90.0, 90.0)
    assert round(tilavuus, 2) == 77.69

    # 2) Violetti fosfori:
    # a = 9.21 Å, b = 9.15 Å, c = 22.6 Å
    # alpha = 90°, beta = 106.1°, gamma = 90°
    tilavuus = alkeiskopin_tilavuus(9.21, 9.15, 22.6, 90.0, 106.1, 90.0)
    assert round(tilavuus, 2) == 1829.84

    # 3) Virheellinen parametri: yhden särmän pituus on negatiivinen
    tilavuus = alkeiskopin_tilavuus(-4.267, 4.267, 4.267, 90.0, 90.0, 90.0)
    assert tilavuus == -1

    # 4) Virheellinen parametri: kulmat eivät muodosta kelvollista yksikkökoppia
    # Näillä kulmilla neliöjuuren sisällä oleva lauseke on <= 0.
    tilavuus = alkeiskopin_tilavuus(1.0, 1.0, 1.0, 0.0, 90.0, 90.0)
    assert tilavuus == -1


test_alkeiskopin_tilavuus()
print("Kaikki testit läpäisty.")
```

Testit näyttävät melko järkeviltä, mutta kurssin aikana olemme oppineet, että liukulukujen yhtäsuuruutta pitää testata esimerkksi `math.isclose`-funktiolla eikä yhtäsuuruuden (`==`) avulla. Pyydetään mallia korjaamaan asia:

    Käytä tilavuuksien testaamiseen math.isclose-funktiota

Lopputulos on alla. Nyt voit myös ajaa koko koodin selaimessa (tai Spyderissä).

```{code-cell} ipython3
import math

def alkeiskopin_tilavuus(a, b, c, alpha, beta, gamma):
    """
    Laskee kiteisen aineen alkeiskopin tilavuuden.

    Parametrit:
        a (float): Yksikkökopin särmän a pituus.
        b (float): Yksikkökopin särmän b pituus.
        c (float): Yksikkökopin särmän c pituus.
        alpha (float): Särmien b ja c välinen kulma asteina.
        beta (float): Särmien a ja c välinen kulma asteina.
        gamma (float): Särmien a ja b välinen kulma asteina.

    Paluuarvo:
        float: Alkeiskopin tilavuus samoissa pituusyksiköissä kuutioituna.
               Jos annetut arvot eivät muodosta kelvollista alkeiskoppia,
               funktio tulostaa virheilmoituksen ja palauttaa arvon -1.
    """

    if a <= 0 or b <= 0 or c <= 0:
        print("Virhe: särmien pituuksien täytyy olla positiivisia.")
        return -1

    alpha_rad = math.radians(alpha)
    beta_rad = math.radians(beta)
    gamma_rad = math.radians(gamma)

    lauseke = (
        1
        + 2 * math.cos(alpha_rad) * math.cos(beta_rad) * math.cos(gamma_rad)
        - math.cos(alpha_rad) ** 2
        - math.cos(beta_rad) ** 2
        - math.cos(gamma_rad) ** 2
    )

    if lauseke <= 0:
        print("Virhe: annetut särmät ja kulmat eivät muodosta kelvollista alkeiskoppia.")
        return -1

    return a * b * c * math.sqrt(lauseke)


def test_alkeiskopin_tilavuus():
    # 1) Cu2O: a = b = c = 4.267 Å, alpha = beta = gamma = 90°
    tilavuus = alkeiskopin_tilavuus(4.267, 4.267, 4.267, 90.0, 90.0, 90.0)
    assert math.isclose(tilavuus, 77.69, abs_tol=0.01)

    # 2) Violetti fosfori:
    # a = 9.21 Å, b = 9.15 Å, c = 22.6 Å
    # alpha = 90°, beta = 106.1°, gamma = 90°
    tilavuus = alkeiskopin_tilavuus(9.21, 9.15, 22.6, 90.0, 106.1, 90.0)
    assert math.isclose(tilavuus, 1829.84, abs_tol=0.01)

    # 3) Virheellinen parametri: yhden särmän pituus on negatiivinen
    tilavuus = alkeiskopin_tilavuus(-4.267, 4.267, 4.267, 90.0, 90.0, 90.0)
    assert tilavuus == -1

    # 4) Virheellinen parametri: kulmat eivät muodosta kelvollista yksikkökoppia
    # Näillä kulmilla neliöjuuren sisällä oleva lauseke on <= 0.
    tilavuus = alkeiskopin_tilavuus(1.0, 1.0, 1.0, 0.0, 90.0, 90.0)
    assert tilavuus == -1


test_alkeiskopin_tilavuus()
print("Kaikki testit läpäisty.")
```

Malli sisällytti myös alkuperäisen funktion tulostukseen. Funktion koodi ei muuttunut testien luomisen yhteydessä.

### Yhteenveto

Suuret kielimallit kuten GPT 5.5 pystyvät luomaan asiallista ohjelmakoodia. Varsinkin teknistieteellisessä työskentelyssä on tärkeää luoda koodia hallitusti yksi selkeä kokonaisuus kerrallaan. Yksittäisen funktion luominen on tästä hyvä konkreettinen esimerkki. Luotu koodi pitää aina ymmärtää ja tarkistaa testeillä, ettei sinne jää loogisia virheitä, laskuvirheitä tai yksikkövirheitä. Vaikka koodi olisi luotu kielimallilla, koodin luonut ihminen on lopulta vastuussa, jos joku menisi pieleen. Tekoäly-yhtiöt eivät ota vastuuta mallien generoimasta koodista.

:::{admonition} Huomio!
:class: attention
Oma ohjelmointiosaaminen on lähtökohta sille, että pystyt  luomaan laadukasta ja toimivaa koodia tekoälyjärjestelmillä. Generoitu koodi on aina testattava huolellisesti ja kattavasti, ettei sinne jää esimerkiksi vääriä yhtälöitä tai laskutoimituksia.
:::
