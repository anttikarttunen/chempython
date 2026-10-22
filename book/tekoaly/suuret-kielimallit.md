---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
---

# Suuret kielimallit

Suuret kielimallit (_Large Language Models, LLM_), ovat tällä hetkellä tärkeimpiä ohjelmoinnissa hyödynnettäviä tekoälyjärjestelmiä. Erittäin rajusti yksinkertaistettuna suuret kielimallit ovat tilastollisia malleja, joille voidaan antaa syötteenä tekstiä ja ne ennustavat, miten teksti jatkuu. Kielimallit on koulutettu valtavilla tekstiaineistoilla, ja yksittäisen kielimallin koulutuksessa voidaan käyttää jopa biljoonia parametrejä. 

Koulutusaineistot sisältävät myös valtavia määriä ohjelmakoodia, joten kielimalli voi luonnollisten kielten lisäksi generoida **ohjelmakoodia** kuten Python-koodia. Jos haluat oppia kielimalleista hieman enemmän, Turun yliopiston tutkija Sampo Pyysalo kertoo Arno Solinin ja Eric Malmin vetämässä [Aalto-yliopiston tekoälypodcastissä](https://www.youtube.com/watch?v=aAMQ0iQ7Gkc) kielimallien toiminnasta. 

Kielimallit ovat kehittyneet vuodesta 2017 lähtien huimalla nopeudella. Syitä tähän on useita, mutta ratkaisevassa roolissa ovat olleet uusien algoritmien kehittäminen, valtavien tietoaineistojen saatavuus (esim. internetin sisältö) ja ennen kaikkea laskentakapasiteetin kehittyminen (osoittautui, että tietokonepelaamiseen kehitetyt grafiikkakiihdyttimet ovatkin erinomaisia työkaluja myös tekoälyjärjestelmien kouluttamisessa ja käytössä).

Suurten kielimallien käyttö kasvoi räjähdysmäisesti, kun OpenAI toi loppuvuodesta 2022 saataville ChatGPT-palvelun, jolla tekoälyjärjestelmää pystyi käyttämään yksinkertaisen web-käyttöliittymän kautta. Nykyisin erilaisia kielimalleja on saatavilla lukuisia. Osa niistä on kaupallisia, kuten OpenAI:n ChatGPT ja Anthropicin Claude. Näitä malleja on mahdollista käyttää vain kyseisten yritysten hallinnoimien palvelimien avulla. 

Suljettujen, kaupallisten mallien lisäksi on olemassa myös useita avoimia kielimalleja, joita voi käyttää joko web-selaimen kautta tai vaikka ladata omalle tietokoneelle. Omalla tietokoneella toimivia, ns. paikallisia kielimalleja käytettäessä kielimallille antamasi tiedot eivät päädy seuraavan kielimallin koulutusaineistoksi. Toisaalta laadukkaat kielimallit vaativat ainakin toistaiseksi varsin tehokkaan tietokoneen toimiakseen riittävän nopeasti.

Tämän kurssin esimerkeissä käytämme suuria kielimalleja vain web-käyttöliittymän kautta, emmekä tutustu esimerkiksi ns. tekoälyagenttien hyödyntämiseen. Jos haluat asentaa omalle koneellesi edistyneemmän, tekoälyagentteja hyödyntävän ohjelmointiympäristön, vaihtoehtoja on useita:
- Yksi avoimesti saatavilla oleva ohjelmisto on [OpenCode](https://opencode.ai/). Sen voi yhdistää kaupallisten palveluntarjoajien kielimalleihin tai kielimallia voi ajaa myös omalla tietokoneella.
- [Visual Studio Code](https://code.visualstudio.com/) on toinen avoimen koodin ohjelmointiympäristö tekoälytyökaluilla.
- Jos et tarvitse edistyneitä työkaluja mutta haluat kokeilla kielimallien ajamista omalla tietokoneellasi, [Ollama](https://ollama.com/) on yksi helppokäyttöinen avoimen koodin ohjelmisto. 

:::{admonition} Huomio!
:class: attention
Jos käytät mitä tahansa verkossa pilvipalveluna toimivaa kielimallia, huomioi, että kielimallille antamasi tiedot päätyvät suurella todennäköisyydellä kielimallin seuraavien versioiden koulutusaineistoksi. Älä siis ikinä syötä verkossa toimiville kielimalleille esimerkiksi **ihmisten henkilötietoja** tai **työnantajan yrityssalaisuuksia**. Jos et halua julkistaa jotain tietoa koko maailmalle, **älä kerro sitä verkossa toimivalle kielimallille**.
:::

:::{admonition} Huomio!
:class: attention
Kielimallit vaativat ainakin toistaiseksi huomattavia määriä laskentatehoa. Tämän vuoksi etenkin verkossa toimivat kielimallit käyttävät valtavia määriä sähköä ja luonnonvaroja. **Vältä kielimallien turhaa käyttöä!**
:::
