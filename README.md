# Anotaçoes

Repositório com algumas notações:

# Topologia

# Trigonométricas

Dado $X, Y \subseteq \mathbb{R}$, com as propriedades.
 1. $X \cup Y = \mathbb{R}$

### Notação
Para que não tenha confusões com notação já conhecida $\cos^2(x)=(\cos(x))^2$ eu proponho a seguinte notação
para trigonométricas compostas, em que: <br/><br/>
$\cos^{*2}(x)=\cos(\cos(x))$ <br/><br/>
também: <br/><br/>
$\cos^{*n}(x)=\cos \circ \cos \circ ... \circ \cos(x)$
<br/><br/>
A mesma notação também pode ser utilizada para demais funções trigonométricas. <br/>

### Relação 1
1.  Subrelação 1.1 \
Para dominio $x \in [n\pi - \frac{\pi}{4}, n\pi + \frac{\pi}{4}]$ aonde $n$ é numero natural temos: <br/>
 $\arccos(\tan(x)) + \arcsin(\tan(x)) = \frac{\pi}{2}$  <br/>

2.  Subrelação 1.2 \
 Para dominio $x \in [\cos(1), 1]$ temos: <br/>
 $\arccos(\arccos(x))+\arcsin(\arccos(x)) = \frac{\pi}{2}$  <br/>

3.  Subrelação 1.3 \
 Para dominio $x \in [\sin(1), -\sin(1)]$ temos: <br/>
 $\arccos(\arcsin(x))+\arcsin(\arcsin(x)) = \frac{\pi}{2}$  <br/>

Para todos os outros valores de $x$ as determinadas funções acima retornam indefinido.

### Simplificação 1
$\arcsin(\cos(x)) = 2\pi|\frac{x}{2\pi}+\frac{1}{2}-\lceil(\frac{x}{2\pi}+1)\rceil|-\frac{\pi}{2}$

Aqui está uma implementação eficiente da função, utiliza modulo ao invés de gambiarras matématicas, ignore a formula anterior e de preferencia a essa:
```python
tau = 2 * math.pi
half_pi = math.pi / 2

def arcsin_cos(x):
    x_normalized = (x + math.pi) % tau
    return half_pi - x_normalized if x_normalized < math.pi else x_normalized - 3*half_pi
```


### Simplificação 2
$\arccos(\sin(x)) = 2\pi|\frac{x}{2\pi}+\frac{3}{4}-\lceil(\frac{x}{2\pi}+\frac{1}{4})\rceil|$

Implementação eficiente desta função, usando a mesma lógica que o anterior:
```python
tau = 2 * math.pi
half_pi = math.pi / 2

def arccos_sin(x):
    x_normalized = (x + 3*half_pi) %  tau
    return x_normalized if x_normalized < math.pi else -x_normalized + tau
```

### Simplificação 3
A função $\arctan(\tan(x))$  é somente uma inversão no dominio $x \in [\frac{\pi}{2}, - \frac{\pi}{2}]$, para todo x nos reais temos: <br/><br/>
$\arctan(\tan(x))= x - \pi\lceil \frac{x}{\pi} - \frac{1}{2}\rceil$ <br/><br/>
Também para $\arctan(\cot(x))$ temos: <br/><br/>
$\arctan(\cot(x))= \pi\lceil \frac{x}{\pi}\rceil - x - \frac{\pi}{2}$ <br/>

### Simplificação 4
A função $\arccos(\cos(x))$ é somente uma função inversa própria no dominio $x \in [0, \pi]$ \
A função $\arcsin(\sin(x))$ é somente uma função inversa própria no dominio $x \in [\frac{\pi}{2}, - \frac{\pi}{2}]$ \
Para todos o $x$ nos reais temos: <br/><br/>
$\arcsin(\sin(x))=2\pi|\frac{x}{2\pi}+\frac{5}{4}-\lceil\frac{x}{2\pi}+\frac{3}{4}\rceil|-\frac{\pi}{2}$ <br/><br/>
$\arccos(\cos(x))=2\pi|\frac{x}{2\pi}+1-\lceil\frac{x}{2\pi}+\frac{1}{2}\rceil|$ <br/><br/>

```python
tau = 2 * math.pi
half_pi = math.pi / 2

def arcsin_sin(x):
    x_normalized = (x + 3*half_pi) % tau
    return half_pi - x_normalized if x_normalized < math.pi else x_normalized - 3*half_pi

def arccos_cos(x):
    x_normalized = (x + math.pi) % tau
    return math.pi - x_normalized if x_normalized < math.pi else x_normalized - math.pi
```

E para todo $n>1$ temos: <br/><br/>
$\arcsin^{*n}(\sin^{*n}(x))= \arcsin(\sin(x))$  <br/><br/>
$\arccos^{*n}(\cos^{*n}(x))= \pi|\frac{x}{\pi}+1-\lceil\frac{x}{\pi}+\frac{1}{2}\rceil|$  <br/><br/>
É importante deixar claro que a mesma relação que ocorre com seno não ocorre com cosseno ou seja $\arccos^{*n}(\cos^{*n}(x)) \neq \arccos(\cos(x))$.

### Trivial 1
Fácilmente observavel através de propriedades básicas da trigonometria: <br/><br/>
$\arcsin(\tan(x)) = -\arcsin(\cot(x+\frac{\pi}{2}))$  <br/><br/>
$\arccos(\tan(x)) = -\arccos(\cot(x+\frac{\pi}{2}))+\pi$ <br/><br/>

### Gráficos 1
Esse gráfico vou chamar de fire-wave pela aparencia, dado $f$ sendo $\arccos$ ou $\arcsin$ ou alguma função periodica com periodo e amplitude pi/2 temos:

$$x_{\text{fire}}(t) = \begin{cases} 
    f(\tan(x)), & \text{if } f(\cot(x)) \text{ is undefined}, \\
    f(\cot(x)), & \text{if } f(\tan(x)) \text{ is undefined}
\end{cases}$$

A seguinte condicional foi criada de forma a reparar a simetria.

TODO: Inversas precisas

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


