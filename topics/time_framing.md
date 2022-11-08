```python
import numpy as np
import matplotlib.pyplot as plt
import librosa as lr
from IPython.display import Audio
```

## Time Framing / Windowing


```python
# !curl https://cdn.freesound.org/previews/82/82797_1254612-lq.mp3 -o ../data/alarm.mp3
```


```python
y, sr = lr.load('../data/alarm.mp3', sr=None)

display(Audio(y, rate=sr))
```

    /Users/danielhopfner/miniconda3/lib/python3.9/site-packages/librosa/util/decorators.py:88: UserWarning: PySoundFile failed. Trying audioread instead.
      return f(*args, **kwargs)




<audio  controls="controls" >
    Your browser does not support the audio element.
</audio>




```python
plt.plot(y)
plt.show()
```


    
![png](time_framing_files/time_framing_4_0.png)
    



```python
rms_amp = np.sqrt(np.mean(y ** 2))

print(rms_amp)
```

    0.18531755



```python
sr
```




    24000




```python
plt.plot(y)
plt.plot(np.ones(y.size) * rms_amp)
plt.show()
```


    
![png](time_framing_files/time_framing_7_0.png)
    



```python
frame_length = 500
hop_size = 80

num_frames = (y.size - frame_length) // hop_size

rms_env = np.zeros(num_frames)
max_env = np.zeros(num_frames)

for i in range(num_frames):
    start_i = i * hop_size
    stop_i = start_i + frame_length
    win = y[start_i:stop_i]
    rms_env[i] = np.sqrt(np.mean(win ** 2))
    max_env[i] = np.max(win)

plt.figure(figsize=(20, 8))
plt.plot(y)
plt.plot(np.linspace(0, y.size, rms_env.size), rms_env)
plt.plot(np.linspace(0, y.size, rms_env.size), max_env)
plt.show()
```


    
![png](time_framing_files/time_framing_8_0.png)
    
