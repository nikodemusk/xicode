+++
title = "Plotta med Python, del 1"
date = "2019-07-22"
author = "Nikodemus Karlsson"
cover = "https://cloudheaven.se/~nikodemus/shared/plottamedpython/smakprov.png"
tags = ["python", "grafer i python", "matematik"]
description = "Varför är det bra att kunna rita grafer med hjälp av programmering?"
showFullContent = false
draft = true
+++
# Inledning
Det är berättigat att fråga sig varför det kan vara motiverat att lära sig
"programmera" en graf istället för att enkelt rita upp den i ett färdigt
program, som t.e.x [Desmos](https://www.desmos.com/calculator).
När jag började min lärarkarriär var jag hänvisad till att kopiera grafer, t.e.x
för prov, ur läromedlens lärarhandledningar. Det gjorde att jag kunde känna mig
styrd över hur en uppgift skulle vara utformad, alternativt göra en egen dålig
graf i något program som inte var primärt designat för detta.

Till saken hör också att jag är lite "pettimetrig", kinkig helt enkelt. Jag
vill att det jag gör ska vara så bra som möjligt, helst också återanvändbart.
I de här sammanhangen vill jag ha kontroll; behöver jag en detaljerad graf för
en övningsuppgift så vill jag kunna skapa den, behöver jag ha en stor graf som
jag visar på en projektorduk vill jag inte att den ska lida av att vara pixlig,
d.v.s suddig i konturerna p.g.a förstoringen. Dessutom tycker jag att det är
tillfredsställande att kunna skapa något utifrån en kod. Det vill jag sprida
vidare här.

Jag vill vara tydlig med att plotta grafer med Python inte ingår i min
skolundervisning. Det är ett verktyg för mig; om däremot elever frågar så
hänvisar jag gärna till Python och [Matplotlib](https://matplotlib.org).

Då börjar vi 😄

# Utvecklingsmiljön
Det finns en helt färdig miljö jag rekommenderar, nämligen
[Google Colab](https://colab.research.google.com). I denna går det att
programmera och få ut resultat och grafer direkt i webbläsaren. Det finns andra
miljöer också, t ex [repl.it](https://repl.it/), men där är det svårare att
spara graferna för sin användning (även om det går). Det här inlägget
fokuserar på hur grafer skapas utifrån ett program, hur Colab fungerar finns
det instruktioner om på deras webbplats.

# Koordinaterna
Har du någon gång skapat en funktionsgraf i ett kalkylprogram? Då vet du att
programmet plottar grafen med hjälp av $x-$ och $y-$koordinater. $x-$koordinaten löper i ett intervall och $y-$koordinaten beräknas från respektive $x-$värde.
Ju tätare värdena ligger desto bättre blir grafen. Så fungerar det i ett
kalkylprogram, och så fungerar det även med Python och Matplotlib. I ett
kalkylprogram är det väldigt tydligt med celler som fylls i och markeras, när
grafer tas fram programmatiskt så syns inte cellerna; de är en abstraktion ur
en **lista**.

Om jag vill ha en lista med 11 värden som går från 0 till 5 i jämna intervall (det blir i sammanhanget stora steg) så skrivs följande:

```py
import numpy as np # Detta är ett bibliotek med funktioner som behövs
x = np.linspace(0, 5, 11) # Här är nu våra x-värden
```
Det behövs naturligtvis även $y-$värden, låt oss säga att det är funktionen
$y=5-2x$ som ska modellera. Därefter vill vi titta på värdena. Koden fortsätter:

```py
y = 5 - 2*x # Tilldelar ett y-värde för respektive x-värde
print(f"x-värden: {x}") # Skriver ut x-värdena...
print(f"y-värden: {y}") # och y-värdena
```
Det ger utmatningen:
```
x-värden: [0.  0.5 1.  1.5 2.  2.5 3.  3.5 4.  4.5 5. ]
y-värden: [ 5.  4.  3.  2.  1.  0. -1. -2. -3. -4. -5.]
```
Här har vi alltså koordinater som Matplotlib kan använda för att rita
en graf.

# Plottning av grafen
