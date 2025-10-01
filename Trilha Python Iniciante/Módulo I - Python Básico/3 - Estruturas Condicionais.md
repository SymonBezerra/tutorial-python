# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Estruturas Condicionais

### E se...?

Vimos no último tutorial um resumo sobre tipos de dados, interpolação de *strings* e variáveis. Vimos também sobre os tipos de dados booleano, inteiro e ponto flutuante. Hoje, queremos dar um primeiro uso prático a esses tipos de dados.

Um código Python é basicamente um roteiro de instruções (*script*): tudo o que está escrito nele será executado. E se quisermos que certas partes do nosso código só sejam executadas sob condições específicas? Aí entram as **estruturas condicionais**, tema do nosso tutorial de hoje.

Estruturas condicionais são ativadas (ou não) por valores booleanos. Vejamos um exemplo de estrutura condicional:

```python
number = 0
if number > 0: # operadores relacionais: >, <, >=, <=
    print('Número positivo') # já que number não é maior que zero, esta linha nunca será executada
```

No caso acima, a expressão `number > 0` retorna um valor booleano `False`, e portanto o `print` nunca será executado. Outro detalhe importante: para delimitar blocos de código, ou no nosso caso, dizer que a função `print` está dentro de uma estrutura condicional, usamos a indentação por quatro espaços ao invés de outros recursos, como chaves (`{}`), que é utilizado pelas linguagens C e Java. Não se preocupe, o seu editor de código já converte tabulações (tecla *Tab*) em quatro espaços, como é o caso do Visual Studio Code.

> Experimente trocar o valor da variável `number` e veja como o código se comporta.

No entanto, e se o número não for positivo, mas queiramos uma saída mesmo assim? Podemos usar a seguinte estrutura:

```python
number = 0
if number > 0:
    print('Número positivo')
else:
    print('Número negativo')
```

Vamos além: e se o número for exatamente zero, e queiramos dar uma terceira saída específica para isso? Podemos encadear uma instrução `elif`:

```python
if number > 0:
    if number > 0:
    print('Número positivo')
elif number < 0:
    print('Número negativo')
else:
    print('Número zero')
```

### Cadeias Condicionais

Estruturas condicionais funcionam em formato de cadeia. O que isto significa? Significa que, em uma estrutura *if-elif-else*, assim que uma condição é satisfeita, as demais linhas de código são simplesmente ignoradas. Vamos experimentar esta característica com uma estrutura condicional de duas variáveis booleanas.

```python
number = 0
number2 = 1

if number > 0:
    print('Número positivo')
elif number2 % 2 == 0: # se o número for par
    print('Segundo número é par')
```

> O operador `==` é um operador relacional de comparação (compara se dois valores são iguais). Para diferenciar dois valores, usamos o operador `!=`.

Ou seja, se o valor de `number` for maior que zero, a segunda instrução, que é um `elif`, será simplesmente ignorada. O mais adequado, neste caso, seria usarmos duas instruções `if`:

```python
number = 0
number2 = 1

if number > 0:
    print('Número positivo')
if number2 % 2 == 0:
    print('Segundo número é par')
```

### Operadores Lógicos

Vimos no último tutorial os operadores aritméticos, e mais acima, também os operadores relacionais `>`, `<`, `>=`, `<=` e `==`. Existem ainda os **operadores lógicos**, criados para trabalharmos com valores booleanos. São eles as palavras reservadas `and`, `or`, e `not`.

Se precisamos utilizar mais de uma condição lógica para uma estrutura condicional e ambas necessitam ser verdadeiras, então podemos utilizar o operador `and` ("e"):

```python
number1 = 0
number2 = 0

if number1 > 0 and number2 > 0: # ambas as condições precisam ser True
    print('Dois números positivos')
```

No entanto, se precisamos apenas de uma condição verdadeira, podemos utilizar o operador `or` ("ou"):

```python
number1 = 0
number2 = 0

if number1 > 0 and number2 > 0: # ambas as condições precisam ser True
    print('Dois números positivos')
elif number1 > 0 and number2 > 0: # apenas uma condição precisa ser True
    print('Um número positivo')
```

Se quisermos inverter uma condição, podemos utilizar o `not`:

```python
name = int(input('Digite seu nome: '))
if not name: # string vazia
    print('Nome vazio!')
else:
    print(f'Olá, {name}')
```

O operador `not` tem precedência, pois é unário (ou seja, aceita apenas um operando), seguido pelo operador `and` e, depois, pelo operador `or`. Pensemos no operador `and` como o sinal de multiplicação, que tem precedência sobre a adição (`or`).

Podemos utilizar parêntesis para alterar a precedência:

```python
number1 = 0
number2 = 0
if not (number1 > 0 and number2 > 0):
    print('Um dos números é negativo')
```

> Fazendo um paralelo com a lógica de conjuntos matemáticos, `and` seria o equivalente de intersecção e `or`, o equivalente de união.

Existe ainda um último operador relacional: a palavra chave `is`. Na prática, ele é um comparador de igualdade como o operador `==`. No entanto, ele também compara **endereços de memória**. Na prática:

```python
value1 = 1000
value2 = 1000

print(value1 is value2) # falso, duas referências de memória diferentes
print(value1 == value2) # verdadeiro, ambos os valores são 1000
```

Na prática, podemos utilizar o operador `is` se queremos conferir se a referência está sendo feita a um ponteiro de memória específico. Falaremos mais sobre ponteiros de memória e referências nos tutoriais sobre funções, mas por enquanto, um caso interessante de uso do operador `is` é para comparar valores com `None`, já que o `None` segue o padrão *singleton* (ou seja, todo valor `None` aponta para um único endereço de memória).

> Atenção: alguns valores, como números inteiros no intervalo $ [-5, 256] $ são colocados em um cache, por razões de performance. Comparar valores com o operador `is` para valores em cache sempre resultarão em `True`. Use com cautela.

Neste tutorial, vimos sobre as estruturas condicionais e como trabalhar melhor com os valores booleanos. Mas os valores booleanos podem ativar outro tipo de estrutura: as estruturas de repetição. Veremos mais sobre isso no próximo tutorial. Bons estudos!