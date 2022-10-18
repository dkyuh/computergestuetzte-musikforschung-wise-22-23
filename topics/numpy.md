# Numpy


```python
import numpy as np
```

## Numpy-Arrays vs. Listen

### elementweise Operationen

```python
# liste
l = [5, 2, 50, 1]
# np-array
a = np.array([5, 2, 50, 1])
```

```python
# `append`
l + [40, 100, 398, 4]
```

    [5, 2, 50, 1, 40, 100, 398, 4]


```python
# elementweise
a + np.array([40, 100, 398, 4])

# a + np.array([40, 100, 398, 4, 10]) # wirft einen error wegen ungleicher anzahl an elementen
```

    array([ 45, 102, 448,   5])


```python
# weitere elementweise operationen
print(a)

print(a - np.array([40, 100, 398, 4]))
print(a * np.array([40, 100, 398, 4]))
print(a / np.array([40, 100, 398, 4]))
print(a * 20)
print(a > 4)
print(np.logical_xor(a > 4, np.array([False, True, True, False])))
```

    [ 5  2 50  1]
    [ -35  -98 -348   -3]
    [  200   200 19900     4]
    [0.125      0.02       0.12562814 0.25      ]
    [ 100   40 1000   20]
    [ True False  True False]
    [ True  True False False]

```python
# listen elementweise (mehrere moeglichkeiten):
num = 20

for i, el in enumerate(l):
    l[i] = el * num

l
```

    [100, 40, 1000, 20]


```python
for i, el in enumerate(l): # --> enumerate in topic Python
    print(i, el)
```

    0 100
    1 40
    2 1000
    3 20

(Siehe auch: [`enumerate`](/topics/python.md#`enumerate`))


```python
l_1 = [1, 2, 3]
l_2 = [10, 20, 30]

for el_1, el_2 in zip(l_1, l_2): 
    print(el_1, el_2)
```

    1 10
    2 20
    3 30

(Siehe auch: [`zip`](/topics/python.md#`zip`))


```python
# list-comprehensions
[a * b for a, b in zip(l, [40, 100, 398, 4])]
```

    [4000, 4000, 398000, 80]

(Siehe auch: [List comprehensions](topics/python.md#List%20comprehensions))


```python
for a, b in zip(l, [40, 100, 398, 4]): 
    print(a * b)
```

    4000
    4000
    398000
    80


### Datentypen

In Listen bleiben die Datentypen aller Elemente erhalten.

```python
[0.1, 0, 'a', True]
```

    [0.1, 0, 'a', True]


Bei NumPy-Arrays werden die Datentypen der Elemente aneinander angeglichen.

```python
print(np.array([0.1, 0, 'a', True]))

print(np.array([0.1, 0, True]))

print(np.array([0, True]))

print(np.array([True]))
```

    ['0.1' '0' 'a' 'True']
    [0.1 0.  1. ]
    [0 1]
    [ True]


### Recheneffizienz

```python
size = 10e7

a_1 = np.linspace(10, 59, int(size))
a_2 = np.linspace(100, 59, int(size))
```

```python
%timeit a_1 * a_2
```

    21.4 ms ± 184 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)


```python
l_1 = a_1.tolist()
l_2 = a_2.tolist()
```

```python
%timeit [a * b for a, b in zip(l_1, l_2)]
```

    1.06 s ± 11.7 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)


## Arrays erstellen

```python
np.array([1, 2, 3, 4])
```

    array([1, 2, 3, 4])


```python
np.arange(10, 100, 3) # for (i = 10; i < 100; i += 3)
```

    array([10, 13, 16, 19, 22, 25, 28, 31, 34, 37, 40, 43, 46, 49, 52, 55, 58,
           61, 64, 67, 70, 73, 76, 79, 82, 85, 88, 91, 94, 97])


```python
np.linspace(10, 100, 30)
```

    array([ 10.        ,  13.10344828,  16.20689655,  19.31034483,
            22.4137931 ,  25.51724138,  28.62068966,  31.72413793,
            34.82758621,  37.93103448,  41.03448276,  44.13793103,
            47.24137931,  50.34482759,  53.44827586,  56.55172414,
            59.65517241,  62.75862069,  65.86206897,  68.96551724,
            72.06896552,  75.17241379,  78.27586207,  81.37931034,
            84.48275862,  87.5862069 ,  90.68965517,  93.79310345,
            96.89655172, 100.        ])


```python
np.geomspace(1, 10, 5)
```

    array([ 1.        ,  1.77827941,  3.16227766,  5.62341325, 10.        ])


## Multidimensionale Arrays

```python
newshape = (5, 4)

np.reshape(np.linspace(10, 100, newshape[0] * newshape[1]), newshape)
```

    array([[ 10.        ,  14.73684211,  19.47368421,  24.21052632],
           [ 28.94736842,  33.68421053,  38.42105263,  43.15789474],
           [ 47.89473684,  52.63157895,  57.36842105,  62.10526316],
           [ 66.84210526,  71.57894737,  76.31578947,  81.05263158],
           [ 85.78947368,  90.52631579,  95.26315789, 100.        ]])


## shapes

```python
l = [1, 2, 3, 4]
```

```python
len(l)
```

    4


```python
a = np.array([1, 2, 3, 4])
```

```python
len(a)
```

    4


```python
a.shape
```

    (4,)


```python
newshape = (5, 4)

a = np.reshape(np.linspace(10, 100, newshape[0] * newshape[1]), newshape)

a.shape
```

    (5, 4)


## Auf Elemente zugreifen

### Element-Zugriff bei eindimensionalen Arrays

```python
a = np.arange(30, 400, 4)

print(a)

print(a[4])

# auch auf strings anwendbar, da auch iterabler datentyp!

print(a[4:10]) # auf bereich zugreifen [start : stop[

print(a[:10])

print(a[4:])

print(a[:])

print(a[:-3])

print(a[4:10:2])

print(a[4::2])

print(a[::-1])

print(a[::-2])
```

    [ 30  34  38  42  46  50  54  58  62  66  70  74  78  82  86  90  94  98
     102 106 110 114 118 122 126 130 134 138 142 146 150 154 158 162 166 170
     174 178 182 186 190 194 198 202 206 210 214 218 222 226 230 234 238 242
     246 250 254 258 262 266 270 274 278 282 286 290 294 298 302 306 310 314
     318 322 326 330 334 338 342 346 350 354 358 362 366 370 374 378 382 386
     390 394 398]
    46
    [46 50 54 58 62 66]
    [30 34 38 42 46 50 54 58 62 66]
    [ 46  50  54  58  62  66  70  74  78  82  86  90  94  98 102 106 110 114
     118 122 126 130 134 138 142 146 150 154 158 162 166 170 174 178 182 186
     190 194 198 202 206 210 214 218 222 226 230 234 238 242 246 250 254 258
     262 266 270 274 278 282 286 290 294 298 302 306 310 314 318 322 326 330
     334 338 342 346 350 354 358 362 366 370 374 378 382 386 390 394 398]
    [ 30  34  38  42  46  50  54  58  62  66  70  74  78  82  86  90  94  98
     102 106 110 114 118 122 126 130 134 138 142 146 150 154 158 162 166 170
     174 178 182 186 190 194 198 202 206 210 214 218 222 226 230 234 238 242
     246 250 254 258 262 266 270 274 278 282 286 290 294 298 302 306 310 314
     318 322 326 330 334 338 342 346 350 354 358 362 366 370 374 378 382 386
     390 394 398]
    [ 30  34  38  42  46  50  54  58  62  66  70  74  78  82  86  90  94  98
     102 106 110 114 118 122 126 130 134 138 142 146 150 154 158 162 166 170
     174 178 182 186 190 194 198 202 206 210 214 218 222 226 230 234 238 242
     246 250 254 258 262 266 270 274 278 282 286 290 294 298 302 306 310 314
     318 322 326 330 334 338 342 346 350 354 358 362 366 370 374 378 382 386]
    [46 54 62]
    [ 46  54  62  70  78  86  94 102 110 118 126 134 142 150 158 166 174 182
     190 198 206 214 222 230 238 246 254 262 270 278 286 294 302 310 318 326
     334 342 350 358 366 374 382 390 398]
    [398 394 390 386 382 378 374 370 366 362 358 354 350 346 342 338 334 330
     326 322 318 314 310 306 302 298 294 290 286 282 278 274 270 266 262 258
     254 250 246 242 238 234 230 226 222 218 214 210 206 202 198 194 190 186
     182 178 174 170 166 162 158 154 150 146 142 138 134 130 126 122 118 114
     110 106 102  98  94  90  86  82  78  74  70  66  62  58  54  50  46  42
      38  34  30]
    [398 390 382 374 366 358 350 342 334 326 318 310 302 294 286 278 270 262
     254 246 238 230 222 214 206 198 190 182 174 166 158 150 142 134 126 118
     110 102  94  86  78  70  62  54  46  38  30]


### Element-Zugriff bei multidimensionalen Arrays

```python
# auf bereiche zugreifen
```

### egal wie viele Dimensionen

```python
# boolsche Indizes
```
