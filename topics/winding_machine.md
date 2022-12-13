```python
import numpy as np
import matplotlib.pyplot as plt
```


```python
t = np.linspace(0, 1, 100)
freq1, freq2 = 2, 5
x = (np.sin(t * 2 * np.pi * freq1) * 0.5) + (np.sin(t * 2 * np.pi * freq2) * 0.5)

winding_freqs = np.linspace(0, 7, 100)
cems = np.zeros_like(winding_freqs, dtype=complex)

for i, winding_freq in enumerate(winding_freqs):
    e_ = np.exp(t * 2 * np.pi * -1j * winding_freq)
    prod = e_ * x
    cems[i] = np.mean(prod) # center of mass

    
    ##############################################################################
    # plot
    ##############################################################################

    plt.figure(figsize=(5 * 3, 5 * 1))
    p1 = plt.subplot(1, 3, 1)
    p2 = plt.subplot(1, 3, 2)
    p3 = plt.subplot(1, 3, 3)
    cm = plt.get_cmap('viridis')

    for prodx, tx, color in zip(prod, t, cm(t)):
        p1.plot(prodx.real, prodx.imag, 'o', color=color)
    p1.set_xlim(-1, 1)
    p1.set_ylim(-1, 1)
    p1.plot([0, cems[i].real], [0, cems[i].imag], color=[1, 0, 0, 1])

    p2.plot(t, x, 'o-')
    p2.plot(t, np.cos(t * 2 * np.pi * winding_freq + np.angle(cems[i])))
    p2.set_ylim(-1, 1)

    p3.plot(winding_freqs, np.abs(cems))

    plt.tight_layout()
#     plt.savefig('./winding_render/wr_%03i.png' % (i))
    plt.show()
```
