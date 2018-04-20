# Sessió 2. Python 2: Estil programació, descomposició en funcions i estructures de control

## Objectius
+ Aprendre bones pràctiques en la denominació de funcions i variables i d'ús dels comentaris
+ Saber descomposar funcions en blocs reutilitzables
+ Conèixer el codi de les iteracions ``for`` i ``while``

## Estil de programació

Els programes sovint es comparteixen entre diferents programadors o es modifiquen al cap d'un temps.

Per això és important que estiguin escrits de forma clara i seguint unes convencions d'estil per fer-los més llegibles.

Cada llenguatge sol tenir unes directrius d'estil. A Python s'usen les directrius [PEP8](https://www.python.org/dev/peps/pep-0008/)

Spyder ens ajuda a seguir aquestes directrius si configurem l'editor per a què ens avisi. Això es fa amb ``Herramientas - Preferencias - Editor - Análisis de estilo del código en el Editor``.

Amb això Spyder ja ens avisarà si no seguim les convencions bàsiques de PEP8.

### Comentaris

Inicieu les funcions amb unes línies de comentaris delimitades per `"""` que indiquin l'objectiu de la funció. Incloeu una línia de comentari pels paràmetres, i una línia pel què retorna.

Incloeu comentaris breus addicionals entre línies amb # per explicar algun detall del codi en particular que no quedi prou clar.

```python
# Exemple

def primerDarrer8(llista):
    """
    Aquesta funció, donada una llista d’enters,
    retorna True si 8 és el primer o el darrer element de la llista,
    retorna False altrament
    :param llista una llista d'enters
    :return: True si 8 és a l'inici o final, False altrament
    """
    if llista[0]==8 or llista[-1]==8: # Amb -1 comencem pel darrera
        return True
    else:
        return False
```		


### Noms de funcions i de variables
Useu noms en minúscules per les funcions i variables. Si són compostes per dues o més paraules, inicieu la segona i següents amb majúscules.

```python
a = 5
meuCotxe = "Toyota"
valorAproximat = 3.567
def calculSuma(a,b):
    pass
```
Ara bé, per a les (falses) constants useu majúscules:

```python
MAXIM = 9999999
```

### Identació
Useu 4 espais per marcar els diferents nivells de blocs.

Si el codi d'una funció ocupa dues línies, identeu-lo per a què siguin consistents.
```python
def funcio():
    print("les instruccions comencen 4 espais a la dreta")
    for i in range(2):
        print("per cada nou bloc, 4 espais més")
		print("pero si vull posar moltes coses en un print",
              "i no m'hi caben, idento per a què sigui",
              "consistent")
```

### Llargada de les línies
Una línia de codi ha d'ocupar com a màxim 79 caràcters.
Si una línia no hi cap en 79 caràcters, la puc continuar amb el caràcter \

```python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    pass
```
 El caràcter \ no cal si la continuació és dintre el mateix parèntesi que la línia anterior

```python
print('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r',
      's', 't', 'u', 'v', 'x', 'y', 'z')
```

### Línies en blanc
Les funcions han d'anar precedides i seguides de dues línies en blanc.

### Espais en blanc
Deixeu espais en blanc davant i darrera dels operadors. Deixeu un espai en blanc darrera de la coma. No poseu espais en blanc al final de les línies de codi. Acabeu sempre les funcions amb un salt de línia.

```python
a = b + c
llista = ['a', 'b', 'c']
```

### Import
Posar cada import en una línia diferent. Situar-los al principi de tot.

```python
import math
import string


def funcio():
    pass
```

## Descomposició en funcions

En cursos més avançats realitzareu funcions força complexes que consistiran en molts passos. I en l'entorn laboral sovint aquestes funcions complexes repeteixen codi ja fet.

Per tal de facilitar la reutilització del codi, i facilitar el manteniment i llegibilitat, es recomana descomposar les funcions en parts petites amb significat.

Quan us enfronteu amb un problema, heu de mirar d'identificar aquelles parts del codi que resolen un problema i separar-les del codi principal.
Finalment, hi haurà una funció principal, que anirà cridant aquestes funcions més petites de forma ordenada, per resoldre el problema gran.

## Iteracions: `for` i `while`

Per conèixer més en detall el funcionament de les estructures de control, consulteu si-us-plau els apunts de l'assignatura sobre estructures de control:

-  [Estructures de control](apunts/control.ipynb)

## Codificació de caràcters

Per saber com es representen els caràcters a l'ordinador, consulteu si-us-plau els apunts de l'assignatura sobre codificació de caràcters:

-  [Caràcters](apunts/caracters.ipynb)
