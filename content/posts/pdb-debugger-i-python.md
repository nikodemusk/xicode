+++
title = "pdb - Debugger i Python"
date = "2019-07-26"
author = "Nikodemus Karlsson"
cover = "https://cloudheaven.se/~nikodemus/shared/pythonstuff/binary-code-475664_1280_cropped.jpeg"
tags = ["python"]
description = " Ett exempel på användning av Pythons debugger"
showFullContent = false
draft = false
+++
Jag installerade just Python 3.7.4. Från och med generation 3.7 kan Pythons
debugger, `pdb`, aktiveras utan att importera något bibliotek.
Det är funktionen `breakpoint()` som gör att programmet stannar och debuggern
aktiveras.

Nedan är en funktion som ska dividera två tal med varandra. Men även om den
anropas med talen 6 och 3 så avbryts körningen med ett fel som säger att det
har skett en division med noll. Programmet debuggas med `breakpoint()`.
(Och ja, programmet är enbart nonsens, det illustrerar enbart principen.)

```python

def divide(x, y):
   breakpoint()  # Denna läggs till efter misslyckad körning

   # Gör något mycket oövertänkt med y
   # (fanns i programmet som kraschade)
   y = y/y - 1   
   breakpoint()  # Denna läggs också till efter misslyckad körning

   return (x/y)

print(divide(6, 3))
```
Körningen ger nu:
```
(Pdb) p(y)  # Kollar y      
3           # y = 3, det var det som funktionen anropades med!
(Pdb) c     # Fortsätter körning
(Pdb) p(y)  # Kollar y igen                                                                            
0.0         # Aha! y = 0. Nu vet vi att felet måste ligga
            # mellan de båda brytpunkterna.
(Pdb) c     # Körningen fortsätts mot det oundvikliga slutet...
ZeroDivisionError: float division by zero
```

Här användes kommandona `p` (print) och `c` (continue). Det finns flera
kommandon till `pdb`.

Det går även bra att vid `pdb`-promten skriva `y = 1`, så ställs värdet på
variabeln om. Det är bra när saker ska testas.
#### Några vanliga kommandon
Nedanstående tabell är hämtad från ett [inlägg på Digital Ocean's Community](https://www.digitalocean.com
community/tutorials/how-to-use-the-python-debugger).
Cred. till [Lisa Tagliaferri](https://www.digitalocean.com/community/users/ltagliaferri)
som skapade detta inlägg under CC-licens!

| **Command**      | **Short form** | **What it does**                                                                     |
|------------------|----------------|--------------------------------------------------------------------------------------|
| `args`           | `a`            | Print the argument list of the current function                                      |
| `break`          | `b`            | Creates a breakpoint (requires parameters) in the program execution                  |
| `continue`       | `c` or `cont`  | Continues program execution                                                          |
| `help`           | `h`            | Provides list of commands or help for a specified command                            |
| `jump`           | `j`            | Set the next line to be executed                                                     |
| `list`           | `l`            | Print the source code around the current line                                        |
| `next`           | `n`            | Continue execution until the next line in the current function is reached or returns |
| `step`           | `s`            | Execute the current line, stopping at first possible occasion                        |
| `pp`             | `pp`           | Pretty-prints the value of the expression                                            |
| `quit` or `exit` | `q`            | Aborts the program                                                                   |
| `return`         | `r`            | Continue execution until the current function returns                                |

# Referenser
* [Officiell dokumentation av pdb](https://docs.python.org/3/library/pdb.html)
* [Tutorial på Digital Ocean's community](https://www.digitalocean.com
community/tutorials/how-to-use-the-python-debugger)
* [Försättsbild från pixaby.com](https://pixabay.com/sv/illustrations/binär-kod-binära-binärt-system-byte-475664/)

Som en "meta-referens" anger jag även [denna tabellgenerator](https://www.tablesgenerator.com/markdown_tables)
som enkelt skapar tabeller i Markdown-språket, vilket används för inlägg på
denna sajt :smile:
