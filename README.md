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

Para todos os outros valores de $x$ as determinadas funções retornam indefinido.

### Simplificação 1
$\arcsin(\cos(x)) = 2\pi|\frac{x}{2\pi}+\frac{1}{2}-\lceil(\frac{x}{2\pi}+1)|-\frac{\pi}{2}$ 

Aqui está uma implementação eficiente da função, utiliza modulo ao invés de gambiarras matématicas, ignore a formula anterior e de preferencia a essa:
```python
tau = 2 * math.pi
half_pi = math.pi / 2

def arcsin_cos(x):
    x_normalized = (x + math.pi) % tau
    return half_pi - x_normalized if x_normalized < math.pi else x_normalized - 3*half_pi
```


### Simplificação 2
$\arccos(\sin(x)) = 2\pi|\frac{x}{2\pi}+\frac{3}{4}-\lceil(\frac{x}{2\pi}+\frac{5}{4})|$

Implementação eficiente desta função, usando a mesma lógica que o anterior:
```python
tau = 2 * math.pi
half_pi = math.pi / 2

def arccos_sin(x):
    x_normalized = (x + 3*half_pi) %  tau
    return x_normalized if x_normalized < math.pi else -x_normalized + tau
```

### Trivial 1
Fácilmente observavel através de propriedades básicas da trigonometria: \
$\arcsin(\tan(x)) = -\arcsin(\cot(x+\frac{\pi}{2}))$  \
$\arccos(\tan(x)) = -\arccos(\cot(x+\frac{\pi}{2}))+\pi$ 

### Gráficos 1
Esse gráfico vou chamar de fire-wave pela aparencia, dado $f$ sendo $\arccos$ ou $\arcsin$ temos:
$$x_{fire}(t)=
\begin{cases}
    \frac{x^2-x}{x},& \text{if } x\geq 1\\
    0,              & \text{otherwise}
\end{cases}
$$

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


