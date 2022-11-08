# Matplotlib


```python
import matplotlib.pyplot as plt
import numpy as np
```

## `plot`

$f(x) = x$


```python
x = np.arange(-10, 10, 0.5)
y = x

plt.plot(x, y)
plt.show()
```


    
![png](matplotlib_files/matplotlib_4_0.png)
    



```python
x = np.arange(-10, 10, 0.5)
y = (x ** 3) - 50

plt.figure(figsize=(10, 10))
plt.plot(x, y, 'o-')
# plt.xlim(-5, 5)
plt.show()
```


    
![png](matplotlib_files/matplotlib_5_0.png)
    


## `imshow`


```python
a = np.reshape(np.linspace(0, 1, 4), (2, 2))

a
```




    array([[0.        , 0.33333333],
           [0.66666667, 1.        ]])




```python
plt.imshow(a, cmap='gray') # cmap: color-map
plt.show()
```


    
![png](matplotlib_files/matplotlib_8_0.png)
    



```python
a = np.reshape(np.linspace(0, 1, 400), (20, 20))

# a
```


```python
plt.imshow(a, cmap='gray') # cmap: color-map
# plt.axis('off')
plt.show()
```


    
![png](matplotlib_files/matplotlib_10_0.png)
    


## Achsenbeschriftung

siehe: [MIDI-Pitch - Frequenz](/topics/freq_midi.md#^e45f90)


```python
# plt.xlabel('xlabel')
# plt.ylabel('ylabel')
```

## Plot-x-y

siehe: [MIDI-Pitch - Frequenz](/topics/freq_midi.md#^7159a7)

```python
x = np.linspace(-10, 10, 200)
y = x ** 2

# plt.plot(y) # x-range von ? 0-200 ?
plt.plot(x, y) # richtig: x-range von -10 - 10
plt.show()
```


    
![png](matplotlib_files/matplotlib_15_0.png)
    

