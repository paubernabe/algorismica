# Sessió 4: Text

## Expressions regulars

Les expressions regulars representen cadenes de caràcters que han de trobar-se en un text. Per a substituir o declarar certs caràcters i conjunts de caràcters semblants s'empren els *metacaràcters*. Una expressió regular es declara, com les cadenes de caràcters, dins de cometes simples o dobles.

Els *metacaràcters* són: ``. ^ $ * + ? { } [ ] \ | ( )``

Tots els altres són caràcters normals. 

Un *metacaràcter* es transforma en caràcter normal si s'escriu precedit d'un caràcter d'escapada ``\``.  Així ``\$`` s'interpreta com el caràcter normal ``$``. Per transformar en caràcter normal el ``\``, cal escriure'n dos de seguits, així ``\\`` s'interpreta com el caràcter normal ``\``.

Si una expressió regular està formada només per caràcters normals, la única cadena que hi encaixa és la pròpia cadena en què consisteix l'expressió regular, així l'expressió regular ``Hola`` defineix un conjunt de cadenes amb un únic element que és la cadena ``Hola``, o l'expressió regular ``Preu = 500\$`` defineix un conjunt de cadenes amb un únic element que és la cadena ``Preu = 500$``.

```python
import re
text = ["Preu = 500$", "Preu = 333$", "Preu = 500€"]
for t in text:
    if re.search(r"Preu = 500\$",t):  # re.search és un objecte
        print(t)
>>> Preu = 500$
```

L'avantatge de les expressions regulars és que a més de poder definir cadenes permet dues característiques més: 
+ que un caràcter de la cadena pertanyi a un conjunt i 
+ que un caràcter o tota una expressió regular es pugui repetir. 

Amb aquestes dues característiques addicionals les expressions regulars es converteixen en una eina molt potent a l'hora de definir conjunts de cadenes per a cercar en un text.

## Conjunts de caràcters

Si en una expressió regular hi ha el metacaracter ``.`` hi encaixen totes les cadenes que encaixin en la resta de l'expressió regular independentment del caràcter que tinguin el la posició on hi ha el punt (excepte el caràcter “salt de línia”). 

Per exemple l'expressió regular ``.`` defineix el conjunt de totes les cadenes de un únic caràcter (tret del salt de línia), l'expressió regular ``.ala`` defineix el conjunt de totes les cadenes de 4 caràcters que tinguin els caràcters “ala” en les posicions segona, tercera i quarta independentment de quin sigui el caràcter que tinguin en la posició primera

```python
import re
text = ["Preu = 530$", "Preu = 333$", "Preu = 500€"]
for t in text:
    if re.search(r"Preu = 5.0.",t):  # re.search és un objecte
        print(t)
>>> Preu = 530$
>>> Preu = 500€
```

Els metacaracters ``[`` i ``]`` es fan servir per definir conjunts de caràcters. Si en una expressió regular apareix un conjunt de caràcters en una posició determinada, en aquella posició hi encaixa qualsevol caràcter que pertanyi a aquell conjunt. Una manera de fer servir aquests metacaràcters per definir un conjunt és ficar-los encerclant una cadena, per exemple ``[abc]`` defineix el conjunt format pels caràcters ``a``, ``b`` i ``c`` . Per exemple l'expressió regular ``[b p]ala`` defineix el conjunt de cadenes de 4 caràcters tals que el seu primer caràcter és un membre del conjunt definit per ``[b p]`` i els caràcters segon tercer i quart són respectivament ``a``, ``l``, i ``a`` per tant, defineix el conjunt de cadenes els elements del qual són: ``bala``, `` ala`` i ``pala`` i no forma part d'aquest conjunt la cadena ``%ala``.

Els metacaràcters ``^``,``-`` i ``\`` tenen un significat especial dins de la definició d'un conjunt de caràcters.

El metacaràcter ``–`` serveix per definir conjunts de caràcters que estan seguits en el codi ASCII sense haver-los d'escriure un per un, només escrivint el primer i l'últim, així el conjunt definit per ``[abcdef]`` és el mateix que el definit per ``[a-f]`` (compte que les vocals accentuades i lletres com la ``ç`` no estan per ordre alfabètic en el codi ASCII).

El matacaràcter ``^`` si es coloca al començament de la cadena serveix per definir el complementari d'un conjunt (en qualsevol altre lloc simplement s'interpreta com el caràcter ``^``). Per exemple, el conjunt ``[^ ]`` és el conjunt de tots el caràcters tret de l'espai en blanc.

El matacaràcter ``\`` davant de certes lletres serveix per designar certs conjunts de caràcters predefinits: 
+ ``\d`` dígits decimals: ``\D`` tot tret dels dígits decimals. 
+ ``\s`` espai blanc . 
+ ``\n`` salt de linia.
+ ``\S`` Tot tret dels caràcters tipus espai blanc. 
+ ``\w`` qualsevol caràcter alfanumèric.
+ ``\W`` tot tret dels caràcters alfanumèrics.

Tot això es pot combinar, per exemple, l'expressió regular: ``a[\s.]b[a-v\d]c`` defineix el conjunt de cadenes de 5 caràcters tals que els seus caràcters primer tercer i cinquè són respectivament ``a``, ``b`` i ``c`` i els seus caràcters segon i quart pertanyen respectivament als conjunts definits per ``[\s.]`` i ``[a-v\d]``, on el conjunt definit per ``[\s.]`` és o bé un caràcter de tipus espai blanc o bé qualsevol caràcter tret del salt de línia (que és el que indica el ``.``). Per tant és qualsevol caràcter incloent-hi el salt de línia. El conjunt definit per ``[a-v\d]`` és qualsevol lletra minúscual de la ``a`` a la ``v`` ambdues incloses o un dígit decimal. Per tant les cadenes ``a%b3c`` i ``abbvd`` pertanyen al conjunt mentre que les cadenes ``abbxd`` i ``b%b3c`` no.

## Repeticions

Els metacaràcters ``+``, ``*``, ``?`` i ``{``, ``}`` es fan servir per indicar repeticions de l'objecte **precedent** que pot ser un caràcter o una expressió regular. ``+`` indica 1 vegada o més, ``*`` cap o més, ``?`` cap o una i ``{n,m}`` entre n i m repeticions totes dues incloses.

Per exemple les expressions regulars:

+ ``ab?c`` defineix el conjunt de cadenes amb els elments: ``abc`` i ``ac``; la primera cadena “encaixa” perquè el caracter “b” es repeteix una vegada i la segona ”encaixa” perquè no es repeteix cap vegada.

+ ``ab{2,5}c`` defineix el conjunt de cadenes que té els elements: ``abbc``, ``abbbc``, ``abbbbc`` i ``abbbbc`` que encaixen perquè en totes elles el caràcter “b” es repeteix entre 2 i 5 vegades, però no conté la cadena “abc” ni la cadena “abbbbbbc” perque en el primer cas el caracter “b” només es repeteix una vegada i en el segon es repeteix 6 vegades.

+ ``ab*c`` defineix el conjunt de cadenes amb infinits elements (en la pràctica el màxim són 2 bilions de repeticions) que conté els elements: “ac”, “abc”, “abbc”, “abbbc”... Cal tenir en compte que 0 repeticions, és a dir la absència del caràcter, encaixa.

+ ``ab+c`` defineix el conjunt de cadenes amb infinits elements (en la pràctica el màxim són 2 bilions de repeticions) que conté els elements: “abc”, “abbc”, “abbbc”... Ara no s'admet 0 repeticions, és a dir la absència del caràcter, no encaixa.

A l'esquerra dels metacaràcters de repetició també hi pot haver un conjunt. Per exemple l'expressió regular ``a[1-3]?b`` defineix el conjunt de cadenes amb els elements: “ab”, “a1b”, “a2b” i “a3b” el primer perquè té 0 repeticions i els tres següents perquè hi ha una repetició d'elements que pertanyen al conjunt definit per [1-3]. Per exemple l'expressió regular ``a[12]{1,2}b`` defineix el conjunt format per les cadenes: “a1b”, “a2b”, “a11b”, “a12b”, “a21b” i “a22b” les dues primeres perquè tenen una repetició d'algun dels elements del conjunt de caràcters definit per ``[12]`` i les quatre últimes perquè en tenen dues.

A l'esquerra dels metacaràcters de repetició també hi pot haver una expressió regular, el resultat és el mateix que l'expressió regular que s'obtindria repetint la cadena que defineix l'expressió regular prèvia el nombre de vegades indicat pels metacaràcters de repetició. 

Per exemple l'expressió regular: ``(ab){2,3}`` defineix el conjunt de cadenes obtingut per la unió dels conjunts de cadenes que defineixen l'expressió regular “abab” i “ababab” en la primer hi ha dues repeticions i en la segona tres, la primera defineix el conjunt de cadenes amb un únic element, la cadena “abab” i la segona el conjunt amb l'únic element “ababab” i la unió dels dos és el conjunt amb els elements “abab” i “ababab”. 

Per exemple l'expressió regular: ``(a[bc]){1,2}`` defineix el conjunt de cadenes obtingut per la unió dels conjunts de cadenes que defineixen l'expressió regular “a[bc]” i “a[bc]a[bc]” en la primer hi ha una repetició i en la segona dues repeticions, la primera defineix el conjunt de cadenes que té per elements “ab” i “ac” i la segona el conjunt amb els elements “abab”, “abac”, “acab” i “acac” i la unió dels dos és el conjunt amb els elements “ab”, “ac”, “abab”, “abac”, “acab” i “acac”.

![alt text](reg.png "Xuleta RegExp")


## Expressions regulars en PYTHON

En Python, el primer que hem de fer és compilar l'expressió d'interès:

L'expressió
```python
import re
p = re.compile('ab*')
p
>>> re.compile(r'ab*', re.UNICODE)
```
produeix una expressió compilada que pot ser usada amb els mètodes de les expressions regulars:

Method/Attribute | 	Purpose
------------ | -------------
match() | 	Determine if the RE matches at the beginning of the string.
search()	 | Scan through a string, looking for any location where this RE matches.
findall()	 | Find all substrings where the RE matches, and returns them as a list.
finditer()	 | Find all substrings where the RE matches, and returns them as an iterator.

### match

```python
import re
p = re.compile('[a-z]+')
p.match("")
print(p.match(""))
>>> None
m = p.match('tempo')
m
>>> <_sre.SRE_Match object; span=(0, 5), match='tempo'>
```
que ens retorna un objecte ```match```sobre el que podem fer preguntes:

Method/Attribute | Purpose
------------ | -------------
group()	 | Return the string matched by the RE
start()	 | Return the starting position of the match
end()	 | Return the ending position of the match
span()	 | Return a tuple containing the (start, end) positions of the match

```python
m.group()
>>> 'tempo'
m.start(), m.end()
>>> (0, 5)
m.span()
>>> (0, 5)
```
### search

```python

import re

line = "Cats are smarter than dogs";
searchObj = re.search( r'(.*) are (.*?) .*', line)

if searchObj:
   print "searchObj.group() : ", searchObj.group()
   print "searchObj.group(1) : ", searchObj.group(1)
   print "searchObj.group(2) : ", searchObj.group(2)
else:
   print "Nothing found!!"

>>> searchObj.group() :  Cats are smarter than dogs
>>> searchObj.group(1) :  Cats
>>> searchObj.group(2) :  smarter
```

### find

```python
p = re.compile('\d+')
p.findall('12 drummers drumming, 11 pipers piping, 10 lords a-leaping')
>>> ['12', '11', '10']
```

```python
text = "He was carefully disguised but captured quickly by police."
re.findall(r"\w+ly", text)
>>> ['carefully', 'quickly']
```

```python
text = "He was carefully disguised but captured quickly by police."
for m in re.finditer(r"\w+ly", text):
     print('%02d-%02d: %s' % (m.start(), m.end(), m.group(0)))
>>> 07-16: carefully
>>> 40-47: quickly
``` 
