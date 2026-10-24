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
# Virheiden etsiminen

Jokainen ohjelmoija tekee koodia kirjoittaessaan virheitä. Kielioppivirheet kuten unohtunut sulku tai lainausmerkki on yleensä helppo löytää Python-editorin avustuksella. Usein käy kuitenkin niin, että ohjelma on kieliopillisesti virheetön, mutta toimii silti väärin. Tällaisten ongelmien selvittämiseen voi kulua paljonkin aikaa.

Ohjelmakoodissa olevia virheitä voi yrittää etsiä tekoälyjärjestelmän avulla. Tarkastellaan käytännön esimerkkiä, jossa lyhyen Python-koodin tarkoituksena olisi piirtää kaksi suoraa:

```
import numpy as np
import matplotlib.pyplot as plt

# Luodaan kahdet XY-datat
X1 = np.linspace(1, 100, 100)
Y1 = X1 * 2
X2 = np.linspace(1, 100, 100)
Y2 = X2 * 4

# Luodaan kaksi kuvaajaa
plt.plot(X1, Y1, 'b-', label = 'f(x) = 2x')
plt.plot(X2, Y2, 'r--', label = 'f(x) = 4x')

# Asetetaan akselien rajat ja luodaan selite
plt.xlim = [0, 100]
plt.ylim = [0, 600]
plt.legend(loc = 'upper left')

# Näytetään kuvaajat
plt.show()
```

Koodi tuottaa alla olevan näköisen kuvaajan:

```{figure} ../figures/ai_plot_wrong.png
---
width: 400
name: ai_plot_wrong
align: center
---
Virheellisen koodin generoima kuvaaja, jossa akselien rajat ovat väärin.
```

Akselien piti olla välillä x = [0, 100] ja y = [0, 600], mutta näin ei ole.

Kysytään kielimallilta, mikä koodissa voisi olla vialla (Aalto AI Assistant / GPT 5.5, lokakuu 2026):

    Miksi tämä Python-koodi piirtää kuvaajan väärin? Akselien rajat ovat väärin.

(*kysymykseen liitettäisiin ohjelmakoodi joko tekstinä tai liitetiedostona*)
	
Kielimallin vastaus:

    Ongelma on näissä riveissä:	  
	plt.xlim = [0, 100]
	plt.ylim = [0, 600]
	  
	Tässä et kutsu Matplotlibin funktioita, vaan korvaat plt.xlim- ja plt.ylim-funktiot listoilla. 
    Siksi akselien rajat eivät asetu oikein, ja lisäksi myöhemmät plt.xlim(...)-kutsut 
    voivat lakata toimimasta samassa Python-istunnossa.
	
	Käytä sen sijaan funktiokutsua:
	plt.xlim(0, 100)
	plt.ylim(0, 600)
	      
No näinhän ne akselit tosiaan asetettiinkin, olipas päässyt unohtumaan! Lisäksi kielimalli tulostaa valmiiksi korjatun koodin ja oikeasti hyödyllisen ohjeen:
	
    Jos olet jo ajanut alkuperäisen koodin esimerkiksi Jupyter Notebookissa, plt.xlim ja plt.ylim 
    ovat voineet mennä rikki kyseisessä istunnossa. Tällöin helpoin ratkaisu on käynnistää Python-istunto 
    uudelleen ja ajaa korjattu koodi.
	
Esimerkiksi Spyderissä pitäisi käynnistää konsoli uudestaan, jos `plt.xlim`- ja `plt.ylim`-funktiot olisi vahingossa rikottu yllä olevalla tavalla (ei mitenkään harvinainen virhe!).

Alla on toimiva koodi, jonka kielimalli korjasi. Voit kokeilla ajaa sen ja huomaat, että akselit ovat kuten pitääkin.

```{code-cell} ipython3
:tags: ["auto-execute-page"]
import numpy as np
import matplotlib.pyplot as plt

# Luodaan kahdet XY-datat
X1 = np.linspace(1, 100, 100)
Y1 = X1 * 2

X2 = np.linspace(1, 100, 100)
Y2 = X2 * 4

# Luodaan kaksi kuvaajaa
plt.plot(X1, Y1, 'b-', label='f(x) = 2x')
plt.plot(X2, Y2, 'r--', label='f(x) = 4x')

# Asetetaan akselien rajat ja luodaan selite
plt.xlim(0, 100)
plt.ylim(0, 600)
plt.legend(loc='upper left')

# Näytetään kuvaajat
plt.show()
```

Tämä oli hyvin yksinkertainen esimerkki ja monimutkaisemmissa ongelmatapauksissa kielimalli voi olla täysin pihalla tai antaa virheellisiäkin neuvoja. Noudata siis neuvojen osalta samaa harkintaa kuin koodin generoinnissa. Usein omille ohjelmointivirheille tulee kuitenkin sokeaksi ja ulkopuoliset neuvot voivat ratkaista tilanteen helpommin.
