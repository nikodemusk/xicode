+++
title = "Grunderna i matplotlib"
date = "2019-07-23"
author = "Nikodemus Karlsson"
cover = ""
tags = ["matplotlib", "plotta med python", "python"]
description = "Under två år har jag använt `matplotlib` för att rita grafer i Python. Jag trodde att jag behärskade det någorlunda, men ack som jag bedrog mig."
showFullContent = false
draft = true
+++
# Bakgrund
Att få upp en funktionsgraf i Python med hjälp av `matplotlib` är inte svårt.
Med lite googlande går det också att anpassa grafen på det som önskas. Ett
problem för mig är att jag är en ganska sporadisk användare. Det gör att jag
hinner glömma bort syntax och detaljer mellan gångerna. En reflektion som jag
gjort är att koden ser lite annorlunda ut från gång till gång, trots att jag gör
ungefär samma sak. Det var upprinnelsen till att jag började sätta mig in i
biblioteket snarare än att googla från gång till gång för att hitta en snabb
lösning till en akut uppgift.

# Anatomin i matplotlib
I det stora perspektivet är det viktigt att vara klar över anatomin och
terminologin i `matplotlib`. Jag hittade en förklarande figur på deras
webbplats.
{{< figure src="https://cloudheaven.se/~nikodemus/shared/plottamedpython/anatomy_of_a_figure.png" alt="Anatomy of a figure" position="left" style="border-radius: 8px;" caption="Ingående element i en figur från matplotlib" captionPosition="left" captionStyle="color: red;" >}}

Bilden finns på [`matplotlib`:s FAQ-sida](https://matplotlib.org/faq/usage_faq.html) med [källkod från denna sida](https://matplotlib.org/3.1.0/gallery/showcase/anatomy.html) (vilket gjorde att jag kunde modifiera
den till mörk bakgrund).

För mig var det bl.a begreppen Axes och Axis som ställde till det tidigare, för
att inte tala om Figure. I `matplotlib`:s objektorienterade design så gäller
att `Figure` är klassen för hela bilden. Den måste finnas, men ofta görs inte
så mycket med den. Storleken kan ställas in med hjälp av denna klass, liksom
att den kan användas då en bild ska sparas. Men själva grafen och
koordinatsystemet är en instans av klassen `Axes`. Med den görs det mesta
som har med grafen att göra. En eller flera ´Axes´ läggs till i en `Figure`,
som då alltså kan innehålla flera diagram.
Klassen `Axes` ska inte förväxlas med metoden `axis()`, som har med själva
koordinataxlarna att göra (som kan styras genom `Axes`).

# Exempel

```python
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure()
ax = fig.add_axes(0, 0, 1, 1)
```

Här erhålls nu ett diagram:

![](https://cloudheaven.se/~nikodemus/shared/plottamedpython/diagramram.png)

eller iallafall ramen till ett diagram. När vi ska lägga till data görs det
med hjälp av variablen `ax` enligt:

```python
line = ax.plot([-2, -1, 0, 1, 2], [7, 6, 5, 4, 3])
points = ax.plot([-2, -1, 0, 1, 2], [7, 6, 5, 4, 3], "o")
```

![](https://cloudheaven.se/~nikodemus/shared/plottamedpython/diagram_1.png)

Jag lade alltså till en lista med x-värden och en annan med y-värden (tråkigt med en rät linje, det ska bli roligare exempel senare).
Dessutom så plottade jag värdena två gånger: den översta raden för att få
linjen och den snarlika undre raden för att få punkterna utmarkerade.

Fördelen med det här exemplet är att det blir tydligt vad som görs. Vi lägger
till en figur, varpå diagrammet läggs i figuren, varpå grafen plottas i
diagrammet. Nackdelen med exemplet är att det inte är så här som det brukar
lösas; det är vanligt att vara mer generell på bekostnad av tydligheten.

# Ett mer generellt exempel
