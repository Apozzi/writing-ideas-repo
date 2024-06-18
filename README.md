# Anotaçoes

Repositório com algumas notações:

# Trigonométricas

### Relação 1
1.  Subrelação 1.1 \
Para dominio $x \in [-\frac{n\pi}{4}, \frac{n\pi}{4}]$ aonde $n$ é numero natural temos: \
 $\arccos(\tan(x)) + \arcsin(\tan(x)) = \frac{\pi}{2}$ 

2.  Subrelação 1.2 \
 Para dominio $x \in [\cos(1), 1]$ temos: \
 $\arccos(\arccos(x))+\arcsin(\arccos(x)) = \frac{\pi}{2}$ 

3.  Subrelação 1.3 \
 Para dominio $x \in [\sin(1), -\sin(1)]$ temos: \
 $\arccos(\arcsin(x))+\arcsin(\arcsin(x)) = \frac{\pi}{2}$ 

### Simplificação 1
$\arcsin(\cos(x)) = 2\pi|\frac{x}{2\pi}+\frac{1}{2}-\lceil(\frac{x}{2\pi}+1)|-\frac{\pi}{2}$

### Simplificação 2
$\arccos(\sin(x)) = 2\pi|\frac{x}{2\pi}+\frac{3}{4}-\lceil(\frac{x}{2\pi}+\frac{5}{4})|$

# Código 
Implementação que retorna um ponto dado a triangle wave:
```python 
def triangle_wave_point(t, frequency, amplitude):
    """
    Generate a single point of a triangle wave.

    :param t: Time point
    :param frequency: Frequency of the triangle wave in Hz
    :param amplitude: Amplitude of the triangle wave
    :return: The amplitude of the triangle wave at time t
    """
    t_mod = (t % (1.0 / frequency)) * frequency
    if t_mod < 0.5:
        return 4 * amplitude * t_mod - amplitude
    else:
        return -4 * amplitude * t_mod + 3 * amplitude
```


