# Sessió 3: Algorísmes Numèrics

## Objectius
+ Resoldre de forma eficient problemes en els que intervenen conceptes simples de teoria de nombres: factors, primers, aritmètica, etc.
+ Usar de forma natural les *comprehensions* de Python
+ Mesurar empíricament el temps de càlcul d'un algorísme.

## Introducció a les comprensions de les llistes en Python. 

Les comprensions de les llistes són una eina per transformar una llista (qualsevol iterable en realitat) en una altra llista. Durant aquesta transformació, els elements es poden incloure de manera condicional a la nova llista i cada element es pot transformar segons sigui necessari.

Cada comprensió es pot reescriure com un bucle sobre la lista, però no tot bucle es pot reescriure com a comprensió de la llista.

Començant pel cas més senzill, una comprensió de llista com aquesta:

```python
a = [func(element) for element in sequence]
```

és equivalent a:

```python
a = []
for element in sequence:
    a.append(func(element))
```

De la mateixa manera que podeu afegir `for` addicionals als bucles i condicions `if` dins dels bucles, també podeu afegir-les a la comprensió.

La clau a entendre és que l'ordre d'esquerra a dreta en la comprensió assigna el mateix ordre als bucles explícits:

```python
a = [func(element) for subseq in seq2d for element in subseq if pred(element)]

a = []
for subseq in seq2d:
    for element in subseq:
        if pred(element):
            a.append(func(element))
```

## Mesura empírica del cost computacional.

`timeit` és un mòdul python que ens permet mesurar de forma aproximada el temps de procés d'unes linies de codi:

```pyton
import timeit

start_time = timeit.default_timer()
func1()
print(timeit.default_timer() - start_time)

start_time = timeit.default_timer()
func2()
print(timeit.default_timer() - start_time)
``` 

Si treballem en un notebook de Jupyter podem fer servir la instrucció `%timeit` per calcular el temps de càlcul d'un línia de codi:

```python
def f(x):
    return x*x

%timeit for x in range(100): f(x)

> 100000 loops, best of 3: 20.3 µs per loop
```

Si poseu `%%timeit` al principi d'una cel·la calculareu el temps de càlcul de tota la cel·la.

```python
%%timeit 
l = []
for i in range(1000):
    l.append(i**2)

> 1000 loops, best of 3: 340 µs per loop
```
## Complexitat de les operacions més habituals de Python

L'assignació d'un valor a una variable (que s'implementa mitjançant la còpia d'una referència) és `O(1)`. 

Els operadors simples (`+`, `*`, etc.) sobre enters petits (menors de 12 dígits) són `O(1)`.

Els operadors sobre col·leccions de dades de longitud `N`, `N = len(data-type)` són:

### Lists:
                               
Operació      | Exemple      | Complexitat     | Notes
--------------|--------------|---------------|-------------------------------
Index         | l[i]         | O(1)	     |
Store         | l[i] = 0     | O(1)	     |
Length        | len(l)       | O(1)	     |
Append        | l.append(5)  | O(1)	     |
Pop	          | l.pop()      | O(1)	     | equivalent a l.pop(-1)
Clear         | l.clear()    | O(1)	     | equivalent a l = []
Slice         | l[a:b]       | O(b-a)	 | O(len(l)-0)=O(N)
check ==, !=  | l1 == l2     | O(N)      |
Insert        | l[a:b] = ... | O(N)	     |
Delete        | del l[i]     | O(N)	     | 
Containment   | x in/not in l| O(N)	     | cerca a la llista
Copy          | l.copy()     | O(N)	     | equivalent a l[:] que és O(N)
Remove        | l.remove(...)| O(N)	     | 
Pop	          | l.pop(i)     | O(N)	     | 
Extreme value | min(l)/max(l)| O(N)	     | cerca a la llista
Reverse	      | l.reverse()  | O(N)	     |
Iteration     | for v in l:  | O(N)          |
Sort          | l.sort()     | O(N Log N)    | 

### Sets

Operació      | Exemple      | Complexitat     | Notes
--------------|--------------|---------------|-------------------------------
Length        | len(s)       | O(1)	     |
Add           | s.add(5)     | O(1)	     |
Containment   | x in/not in s| O(1)	     | 
Remove        | s.remove(..) | O(1)	     | 
Discard       | s.discard(..)| O(1)	     | 
Pop           | s.pop()      | O(1)	     |
Clear         | s.clear()    | O(1)	     | equivalent a s = set()
check ==, !=  | s != t       | O(len(s))     | 
<=/<          | s <= t       | O(len(s))     | issubset
\>=/>         | s >= t       | O(len(t))     | issuperset 
Union         | s l t        | O(len(s)+len(t)) |
Intersection  | s & t        | O(len(s)+len(t)) |
Difference    | s - t        | O(len(s)+len(t)) |
Symmetric Diff| s ^ t        | O(len(s)+len(t)) |
Iteration     | for v in s:  | O(N)          |
Copy          | s.copy()     | O(N)	     |

### Dictionaries
                             
Operació      | Exemple      | Complexitat     | Notes
--------------|--------------|---------------|-------------------------------
Index         | d[k]         | O(1)	     |
Store         | d[k] = v     | O(1)	     |
Length        | len(d)       | O(1)	     |
Delete        | del d[k]     | O(1)	     |
get/setdefault| d.method     | O(1)	     |
Pop           | d.pop(k)     | O(1)	     |
Pop item      | d.popitem()  | O(1)	     |
Clear         | d.clear()    | O(1)	     | equivalent a s = {} o = dict()
View          | d.keys()     | O(1)	     | el mateix que d.values()
Iteration     | for k in d:  | O(N)      | totes les formes: keys, values, items
