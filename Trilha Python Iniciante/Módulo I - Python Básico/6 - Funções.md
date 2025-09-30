# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Funções

No último tutorial, além das exceções, conhecemos brevemente os blocos de funções e também o conceito de *call stack*. Hoje, vamos ver em mais detalhes os conceitos relacionados a funções em Python, e como podemos utilizá-las para deixar o nosso código mais modular.

### O conceito de subrotina: funções *vs.* procedimentos

O nome técnico mais correto para o elemento que compõe a *call stack* é **subrotina** (isto é, instruções de código executados de maneira subjacente). Existem dois tipos de subrotina: as **funções**, que retornam um valor, como foi o caso da função de divisão do último exemplo; e os **procedimentos**, que não retornam nenhum valor.

> Chamaremos ambos os tipos de subrotina de "função" neste tutorial.

Uma função é definida pela palavra chave `def`:

```python
def func(): # esta linha recebe o nome de assinatura da função
    pass
```

Funções podem ter zero ou mais argumentos:

```python
def add(n1, n2):
    return n1 + n2
```

A palavra chave `return` retorna um valor, mas também finaliza a função, retirando-a da *call stack*. Ou seja, o `return` pode ser utilizado para finalizar estruturas de repetição:

```python
def is_prime_number(num):
    for i in range(1, num):
        if num % 2 == 0: # é divisível
            return True # na primeira ocorrência, a função e, consequentemente, o loop for são encerrados
    return False
```

Podemos atribuir valores a partir destas funções:

```python
def is_prime_number(num):
    for i in range(1, num):
        if num % 2 == 0:
            return True
    return False

while True:
    num = int(input('Digite um número positivo: '))
    if num < 0:
        print('Número negativo!')
    else: break

is_prime = is_prime_number(num)
if is_prime:
    print(f'O número {num} é primo')
else:
    print(f'O número {num} NÃO é primo')
```

Podemos transformar a função em um procedimento, neste caso:

```python
def is_prime_number(num):
    for i in range(1, num):
        if num % 2 == 0:
            print(f'O número {num} é primo')
    print(f'O número {num} NÃO é primo')

while True:
    num = int(input('Digite um número positivo: '))
    if num < 0:
        print('Número negativo!')
    else: break

is_prime_number(num)
```

> Se tentarmos atribuir um procedimento a uma variável, o valor atribuído será um `None`.

### Escopo de variáveis: global *vs.* local

Cada elemento na pilha tem suas próprias variáveis - isto é chamado de **escopo**. Ou seja, tendo como base o último exemplo, poderíamos ter como base o seguinte *script*:

```python

num = 17 # escopo global

def is_prime_number(num):
    # num aqui possui um escopo local
    for i in range(1, num):
        if num % 2 == 0:
            print(f'O número {num} é primo')
    print(f'O número {num} NÃO é primo')

is_prime_number(num)
```

Neste caso, mesmo possuindo o mesmo nome, `num` (global) e `num` local são variáveis diferentes na memória: quando a função é chamada, é feita uma "cópia" dos parâmetros que são passados. Ou seja, se fizéssemos uma alteração dentro da variável `num` local - o que transformaria a função em uma **função impura**, a variável global não seria afetada.

```python
num = 17

def is_prime_number(num):
    for i in range(1, num):
        if num % 2 == 0:
            print(f'O número {num} é primo')
    print(f'O número {num} NÃO é primo')
    num += 1

is_prime_number(num) # continua sendo 17
```

> Existe um paradigma de programação baseado apenas em funções puras: a **programação funcional** (*functional programming*), que é bastante usada em *frameworks* de programação *front-end*.

Para alcançarmos esta funcionalidade, temos duas opções.

1. Retornar o valor da cópia e reatribuí-lo à variável global:
```python
num = 17

def is_prime_number(num):
    for i in range(1, num):
        if num % 2 == 0:
            print(f'O número {num} é primo')
    print(f'O número {num} NÃO é primo')
    num += 1

num = is_prime_number(num) # 18
```

2. Utilizamos explicitamente a variável global, especificada pela palavra chave `global`:

```python
num = 17

def is_prime_number(num):
    global num
    for i in range(1, num):
        if num % 2 == 0:
            print(f'O número {num} é primo')
    print(f'O número {num} NÃO é primo')

is_prime_number() # 18
```

Toda variável que declaramos dentro de uma função só existe dentro do escopo da mesma. No entanto, é possível acessar variáveis globais dentro do escopo local. Ou seja, a linha `global num`, neste caso, é redundante. A palavra chave `global` é apenas necessária quando:

1. Redefinimos variáveis globais:

```python
num = 1

def change_num(new_num)
    global num
    num = new_num # sem o global, uma nova variável `num` seria criada
    num += 1 # sem o `global`, teríamos um `UnboundLocalError`
```

> Veremos no próximo tutorial, onde falaremos das coleções em Python, que objetos mutáveis podem ser alterados sem o `global`.

### Argumentos

Toda variável presente assinatura de uma função recebe o nome de **argumento**, e toda variável passada na invocação de uma função recebe o nome de **parâmetro**. Confuso? Vamos explicar no código:

```python
def func(arg1, arg2): # argumentos
    return arg1 + arg2

# parâmetros
param1 = 1
param2 = 2

func(param1, param2)
```

Já entendemos o conceito de "cópia" e de escopo global *vs.* local. Há um outro conceito que podemos encontrar nos argumentos de uma função: podemos definir **valores padrão** para os argumentos de uma função. Neste caso, poderíamos ter uma função assim:

```python
count = 0
def inc(inc=1)
    global count
    count += 1
```

Há apenas uma regra quanto a valores padrão: eles devem estar ao final da assinatura da função:

```python
def inc_example1(num): # CORRETO!
    pass # bloco de código

def inc_example2(inc=1, num): # ERRADO!
    pass # bloco de código
```

Valores padrão são especialmente úteis em diversos casos quando utilizamos funções. Num resumo, podemos tornar o nosso código mais *modular* ao utilizarmos funções, pois podemos reaproveitar código de uma maneira mais limpa e até variável, já que o comportamento da função também depende dos seus parâmetros. No próximo tutorial, também veremos como utilizar melhor coleções como parâmetros de funções.

### Bônus: o operador *walrus*

Pense no seguinte caso: e se quisermos invocar uma função com a expressão de uma estrutura condicional ou de repetição? Para isso, existe o operador ***walrus*** (morsa, `:=`), que pode ser utilizado da seguinte maneira.

Imaginemos o seguinte caso com a função de números primos:

```python
def is_prime_number(num)
    for i in range(num):
        if num % i == 0:
            return True
    return False

num1 = int(input('Digite um número: '))
num2 = int(input('Digite outro número: '))
for i in range(num1, num2 + 1):
    if is_prime_number(i):
        print(f'Primeiro número primo encontrado: {i}')
```

E se quisermos fazer alguma operação com a variável `range`? Poderíamos declará-la fora do *loop* `for`, mas podemos fazer isso tudo em uma linha única, usando o operador de morsa:

```python
for i in (interval:=range(num1, num2 + 1)): # precisa ser usado com parênteses
    print(f'Buscando números primos de {interval.start} até {interval.stop}, número atual: {i}')
    # resto do código
```

Vejamos um outro exemplo:

```python
while (num:=int(input('Digite um número: '))) != 0:
    print(is_prime_number(num))
```

Ou seja, podemos utilizar *one-liners* para resumir o nosso código.

No próximo tutorial, veremos sobre variáveis que armazenam mais de um valor, as coleções, e suas principais características. Bons estudos!