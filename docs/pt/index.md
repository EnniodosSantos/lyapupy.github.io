# Sobre o lyapupy


`lyapupy` é uma biblioteca feita totalmente em Python voltada para a geração e análise de séries temporais caóticas sintéticas, derivadas de sistemas dinâmicos discretos com expoentes de Lyapunov exatos e medidas invariantes conhecidas analiticamente.

## Instalação

O exchaos pode ser instalado via linha de comando utilizando:

* `pip install exchaos`
* `pip install sinthchaos`
* `pip install chaosforge`
* `pip install ergodichaos`
* `pip install ergodic`


## Basic Usage




## Lista de Funções

### Map Time Series (Série Temporal do Mapa)

<div class="func-header">
    <b>map_time_series</b><span>(map_name, x0, steps, trans, prec=50, dec=False, plot=False)</span>
</div>

Computa a evolução de um mapa caótico.

**Parâmetros:**

:   **map_name** (*str*): Nome do mapa caótico. [mapas disponíveis](#lista-de-mapas)
:   **x0** (*float*): Condição inicial para as iterações.
:   **steps** (*int*): Número de iterações usadas para computar a evolução do mapa.
:   **trans** (*int*): Número de iterações transitórias a serem descartadas.
:   **prec** (*int*): Precisão decimal (padrão: 50).
:   **dec** (*bool*): Se deve retornar um objeto `Decimal` (se `True`) ou um `np.array` (se `False`, padrão).
:   **plot** (*bool*): Se deve exibir um gráfico da evolução da convergência (padrão: `False`).

**Retorno:**
:   **values** (*array ou Decimal*): Série temporal contendo a evolução do mapa caótico.

**Tipo de retorno:**
:   numpy.array ou decimal.Decimal

**Exemplos**

```python
>>> map_time_series("Logistic", 0.69, 1000, 100)
array([9.66107169e-01, 1.30976429e-01, 4.55286417e-01,...,2.03055676e-01])
>>>
>>> map_time_series("Ulam", 0.69, 1000, 100, dec=True)
[Decimal('-0.6870338025456384356961511819355663023943768799766'),
 Decimal('0.05596910831936139542992034181417084026349458638572'),...,Decimal('0.11798100275668302052603852642095837137197711931708')]
>>>
>>> map_time_series("Tent", 0.69, 1000, 100, plot=True)
array([0.88, 0.24, 0.48, 0.96, ... , 0.64, 0.72, 0.56])
```

### Lyapunov Estimated (Lyapunov Estimado)

<div class="func-header"> <b>lyapunov_estimated</b><span>(map_name, x0, steps, trans, prec=50, dec=False)</span> </div>

Computa o Expoente de Lyapunov estimado de um mapa caótico.

Parâmetros: : map_name (str): Nome do mapa caótico. : x0 (float): Condição inicial. : steps (int): Número de iterações usadas na média de Lyapunov. : trans (int): Número de iterações transitórias descartadas. : prec (int): Precisão decimal. : dec (bool): Se deve retornar um objeto Decimal (se True) ou um float (se False, padrão).

Retorno: : values (float ou Decimal): O Expoente de Lyapunov estimado do mapa caótico.

Tipo de retorno: : float ou decimal.Decimal

Exemplos

``` Python
>>> lyapunov_estimated("Tent", 0.69, 1000, 100)
0.6931471805599453
>>>
>>> lyapunov_estimated("Tent", 0.69, 1000, 100, dec=True)
Decimal('0.69314718055994530941723212145817656807550013436')
```

### Lyapunov Convergence (Convergência de Lyapunov)

<div class="func-header"> <b>lyapunov_convergence</b><span>(map_name, x0, steps, trans, prec=50, dec=False, plot=False)</span> </div>

Computa a convergência do Expoente de Lyapunov de um mapa caótico.

Parâmetros: : map_name (str): Nome do mapa caótico. : x0 (float): Condição inicial. : steps (int): Número de iterações usadas na média de Lyapunov. : trans (int): Número de iterações transitórias descartadas. : prec (int): Precisão decimal. : dec (bool): Se deve retornar um objeto Decimal. : plot (bool): Se deve exibir um gráfico da convergência.

Retorno: : values (array ou Decimal): Os valores de convergência do Expoente de Lyapunov.

Tipo de retorno: : numpy.array ou decimal.Decimal

### Theoretical Lyapunov (Lyapunov Teórico)

<div class="func-header"> <b>theoretical_lyapunov</b><span>(map_name, dec=False)</span> </div>

Retorna o Expoente de Lyapunov teórico de um mapa caótico.

Parâmetros: : map_name (str): Nome do mapa caótico. : dec (bool): Se deve retornar um objeto Decimal (se True) ou um float (se False, padrão).

Retorno: : values (float ou Decimal): O Expoente de Lyapunov teórico do mapa caótico.

Tipo de retorno: : float ou decimal.Decimal

``` Python
>>> theoretical_lyapunov("Tent")
0.6931471805599453
```

### Lyapunov Summary (Resumo de Lyapunov)

<div class="func-header"> <b>lyapunov_summary</b><span>(map_name, x0, steps, trans, prec=50, dec=False, plot=False)</span> </div>

Parâmetros: : map_name (str): Nome do mapa caótico. : x0 (float): Condição inicial. : steps (int): Número de iterações usadas na média de Lyapunov. : trans (int): Número de iterações transitórias descartadas. : prec (int): Precisão decimal. : dec (bool): Se deve retornar um objeto Decimal. : plot (bool): Se deve exibir um gráfico de resumo.

Retorno: : values (dict): Dicionário contendo o nome do mapa caótico, expoente de Lyapunov teórico, expoente de Lyapunov estimado e a série temporal do mapa.

Tipo de retorno: : dict

``` Python
>>> lyapunov_summary("Tent", 0.69, 1000, 100)
{'map': 'Tent map',
 'theoretical': 0.6931471805599453,
 'estimated': 0.6931471805599453,
 'time_series': array([0.88, 0.24, 0.48, 0.96, 0.08, 0.16, 0.32,..., 0.72, 0.56])}
 ```

## Lista de Mapas

Na teoria do caos, mapas (também conhecidos como mapas iterados, equações de diferenças ou relações de recorrência) são sistemas dinâmicos nos quais o tempo é discreto em vez de contínuo. A simulação de mapas discretos é fundamental, pois estes servem como ambientes controlados para o estudo de sistemas caóticos, permitindo a observação de fenômenos complexos através da evolução de órbitas discretas em vez de fluxos contínuos.

Os seguintes mapas podem ser simulados com este pacote:

### Mapa Logístico (Logistic Map)

String de entrada: "Logistic"

Equação: $x_{n+1} = rx_n(1 - x_n)$

### Mapa de Ulam (Ulam Map)

String de entrada: "Ulam"

Equação: $x_{n+1} = 1 - 2x_n^2$

### Mapa Tenda (Tent Map)

String de entrada: "Tent"

Equação: $x_{n+1} = \begin{cases} \mu x_n & \text{se } x_n < \frac{1}{2} \\ \mu (1 - x_n) & \text{se } x_n \geq \frac{1}{2} \end{cases}$

### Mapa de Gauss (Gauss Map)

String de entrada: "Gauss"

Equação: $x_{n+1} = \frac{1}{x_n} - \lfloor \frac{1}{x_n} \rfloor$

### Mapa de Bernoulli (Bernoulli Map)

String de entrada: "Bernoulli"

Equação: $x_{n+1} = 2x_n \pmod 1$

### Mapa Tenda Assimétrico (Asymmetric Tent Map)

String de entrada: "Asymmetric Tent"

### Mapa de Chebyshev (Chebyshev Map)

String de entrada: "Chebyshev"

Equação: $x_{n+1} = \cos(k \arccos(x_n))$

### Mapa de Cúspide (Cusp Map)

String de entrada: "Cusp"

Equação: $x_{n+1} = 1 - \sqrt{|1 - 2x_n|}$

## Referencias

[^1]: [^1]: STROGATZ, Steven H. **Nonlinear Dynamics and Chaos**: With Applications to Physics, Biology, Chemistry, and Engineering. 2. ed. [S.l.]: CRC Press, 2014.
