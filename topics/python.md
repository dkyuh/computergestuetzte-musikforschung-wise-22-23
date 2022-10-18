# Python

## Nützliche Funktionen für `for`-loops

### `enumerate`

```python
l = [100, 40, 1000, 20]

for i, el in enumerate(l): # ueber liste iterieren und index erhalten
    print(i, el)
```

    0 100
    1 40
    2 1000
    3 20

### `zip`

```python
l_1 = [1, 2, 3]
l_2 = [10, 20, 30]

for el_1, el_2 in zip(l_1, l_2): 
    print(el_1, el_2)
```

    1 10
    2 20
    3 30

## List comprehensions

List comprehensions bieten eine einfache Syntax, wie eine Abkürzung von `for`-Loops.

Beispielsweise, anstatt eines klassischen `for`-Loops

```python
l = [2, 54, 34, 12, 22, 21, 7, 46]
new_l = []

for el in l:
    if el > 20:
        new_l.append(el)

new_l
```

	[54, 34, 22, 21, 46]


können wir folgendes schreiben:

```python
l = [2, 54, 34, 12, 22, 21, 7, 46]
new_l = [el for el in l if el > 20]

new_l
```

	[54, 34, 22, 21, 46]


Interessanter Artikel, ob list comprehensions schneller sind als for loops: ^[[List Comprehensions vs. For Loops: It is not what you think | Towards Data Science](https://towardsdatascience.com/list-comprehensions-vs-for-loops-it-is-not-what-you-think-34071d4d8207)]

