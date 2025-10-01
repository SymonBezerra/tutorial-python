# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Coleções

No último tutorial, vimos o conteúdo sobre funções, e como funciona o escopo global *vs.* local de variáveis. Neste tutorial, veremos as principais **coleções** da linguagem Python, e algumas das funções que podem manipulá-las.

### Armazenar mais de um valor

Variáveis comuns podem armazenar um único valor. Em resumo, elas são ponteiros de memória alocados para um determinado valor. No entanto, existem formas de alocarmos mais de um ponteiro de memória numa única variável: é aí que entram as coleções. As principais coleções do Python são as listas (`list`), as tuplas (`tuple`), os conjuntos (`set`) e os dicionários (`dict`).

Comecemos pela estrutura de dados primordial, a lista. Basicamente, ela coloca elementos um ao lado do outro, como em uma prateleira. Listas são declaradas no Python através de colchetes (`[]`), ou através da função `list`:

> Em outras linguagens, listas são chamadas de `arrays` (vetores).

```python
empty_list = list() # lista vazia
array = [1,2,3]

for i in array: # iterável
    print(array[i]) # colchetes: operador de indexação
```

Podemos executar algumas operações com listas:

```python
array = list()

for i in range(10):
    array.append(i) # inserir ao final

# Elementos em listas são contados a partir do número zero
print(array[0]) # imprime o primeiro elemento

print(array.index(5)) # imprime o índice da primeira ocorrência do número 5,
                      # retorna um ValueError caso o elemento não esteja na lista

last_element = array.pop() # retorna o último elemento da lista, removendo-o
first_element = array.pop(0) # retorna o primeiro elemento, removendo
# causa um IndexError se a lista estiver vazia ou se o índice for invaĺido para a lista

array.remove(2) # remove a primeira ocorrência do elemento 2

sorted_array = sorted(array) # ordena a lista
reversed_array = sorted(array, reverse=True)

new_array = array.copy() # copia o array

array.insert(0, 100) # insere o elemento `100` antes do índice zero
```

Uma observação sobre ponteiros de memória: listas e coleções referenciam um conjunto de ponteiros. Se declaramos:

```python
array = [1,2,3]
new_array = array # apenas copia o ponteiro
# qualquer operação feita em `array` será feita em `new_array` e vice versa

new_array = array.copy() # maneira correta
```

Listas podem conter múltiplos tipos de dados, até outras listas (o que seria chamado de **matriz**):

```python
mixed_array = [1, True, [1,2,3], 0.5]
```

O segundo tipo de coleção no Python é similar às listas, porém com uma diferença crucial: são constantes, ou seja, não podem ter elementos removidos ou adicionados. Estamos falando das **tuplas** (`tuple`), definidas por parêntesis (`()`). As tuplas também possuem índices numéricos a partir do zero, porém são imutáveis:

```python
const_values = (1,2,3)

for i in const_values: # iterável
    print(const_values[i])
```

Tuplas são mais apropriadas quando queremos passar valores fixos. Um exemplo seria:

```python
SIZE = (8,8) # valor constante

board = list()
for i in range(SIZE[0]):
    print(f'Adicionando linha {i}')
    for j in range(SIZE[1]):
        print(f'Adicionando coluna {chr(ord('A') + j)}')
```

Outro tipo de coleção no Python são os **conjuntos** (`set`). Os conjuntos diferem das listas e tuplas em dois sentidos: primeiro, conjuntos não possuem índice, sendo possível acessar um elemento apenas pelo próprio elemento:

```python
integers = {0,1,2,3,4,5,6,7,8,9}

print(integer[0]) # 0
```

Outra característica que o torna bem útil é que os elementos dentro de um `set` são únicos, ou seja, não é possível adicionar dois elementos iguais. Podemos utilizar isto para algumas operações como:

```python
array = [100, 100, 200, 300, 500, 200, 400]

unique = set(array) # criamos um set a partir da variável array
for u in unique:
    print(u) # 100, 200, 300, 500, 400
```

É possível criar uma coleção a partir de outra, usando o tipo como função (**construtor**):

```python
CONST_VALUES = (100, 200, 300)
array = list(CONST_VALUES) # transformamos a lista em tupla

# isto vale para list, tuple e set
```

Por fim, veremos a última coleção deste tutorial: estamos falando do **dicionário** (`dict`). O dicionário é como uma lista, porém, ao invés de ter índices sequenciais numéricos a partir do zero, ele pode ter como índice qualquer objeto *hashable* (o que inclui *strings*, inteiros e até alguns objetos compostos, como as tuplas). Vejamos um exemplo:

```python
RANK_VALUES = {  # cartas
    'Quatro': 1,
    'Cinco': 2,
    'Seis': 3,
    'Sete': 4,
    'Dama': 5,
    'Valete': 6,
    'Rei': 7,
    'Ás': 8,
    'Dois': 9,
    'Três': 10
}

SUIT_VALUES = {  # naipes
    'Ouros': 1,
    'Espadas': 2,
    'Copas': 3,
    'Paus': 4
}

MANILLA = 'Dama'

# função que compara manilhas do Truco
def compare_card(card1, card2): # onde `card1` e `card2` são tuplas de strings (valor, naipe)
    if RANK_VALUES[card1[0]] == MANILLA and RANK_VALUES[card2[0]] == MANILLA:
        return SUIT_VALUES[card1[1]] > SUIT_VALUES[card2[1]]
    else:
        return RANK_VALUES[card1[0]] > RANK_VALUES[card2[0]]
```

Neste exemplo acima, poderíamos muito bem utilizarmos uma lista e ordenar os valores em um equivalente um para um. No entanto, para um uso mais legível das funcionalidades, podemos inverter a *string* como **chave** (índice) e o número inteiro como **valor**. Ou seja, o dicionário é uma estrutura de dados chave-valor, ao invés de ser linear.

Alguns exemplos de funções com dicionários:

```python
rank_values = {  # cartas do Truco
    'Quatro': 1,
    'Cinco': 2,
    'Seis': 3,
    'Sete': 4,
    'Dama': 5,
    'Valete': 6,
    'Rei': 7,
    'Ás': 8,
    'Dois': 9,
    'Três': 10
}

card = rank_values['Rei']

card2 = rank_values['Oito'] # retorna um KeyError

card3 = rank_values.get('Nove', -1) # retorna -1 caso não encontre, se não for especificado, o valor retornado será None

new_ranks = {
    'Oito': 11,
    'Nove': 12,
    'Dez': 13
}

rank_values.update(new_ranks) # adiciona chaves-valores ao dicionário, caso sejam iguais, sobrescreve

for card in rank_values: # equivalente de rank_values.keys()
    print(card) # imprime a chave

for value in rank_values.values():
    print(value) # imprime o valor

for card, value in rank_values.items():
    print(card, value) # retorna chave e valor

keys = list(rank_values.keys()) # `keys`, `values` e `items` retornam uma função generator, não uma coleção - atenção para isto!
```

Atenção para a sintaxe `for card, value in rank_values.items()`: a função `items` retorna uma tupla. Valores como tuplas e listas podem ser **desempacotados** (*unpacked*) atribuindo-os a um número de variáveis igual ao número de elementos presentes:

```python
array = [1,2,3] # o mesmo vale para tuplas
first, second, third = array
print(first) # 1
print(second) # 2
print(third) # 3
```

## Listas e dicionários em uma única linha: *list* e *dict comprehension*

Provavelmente você já deve ter visto em alguma aula de matemática a declaração de um conjunto como $ A = \{x | x > 0\} $, neste caso, o conjunto dos inteiros positivos. Podemos utilizar uma sintaxe similar para construir listas e dicionários a partir de outros objetos iteráveis, ou seja, de outras coleções. Vejamos um exemplo:

```python
# Exemplo de list comprehension
array = list(range(1, 11)) # 0 a 10
squared_array = [x**2 for x in array]
# o que seria equivalente de:
# for x in array: squared_array.append(x**2)
```

Neste caso, passamos uma **expressão** que transforma o valor recebido. O mesmo poderia ser feito com *unpacking*:

```python
pairs = [(0,0), (1,1), (2,2), (3,3)] # coordenadas de uma reta
squared_numbers = [(x**2, y**2) for x, y in pairs]
# equivalente de [(pair[0]**2, pair[1]**2) for pair in pairs)]
```

É possível também fazer o mesmo para dicionários:

```python
# Exemplo de dict comprehension
numbers = list(range(10))
alphabet = {
    ord('A') + n: chr(ord('A') + n)
    for n in numbers
}
# dicionário resultante: {0: 'A', 1: 'B'...}
```

É possível até encadear mais de uma *comprehension*, seja de dicionário ou de lista. Atenção: isso pode diminuir a legibilidade do seu código, mesmo que economize um *loop* `for`, então, use com sabedoria.

```python
def f(x):
    return x**2 + 1
matrix = [
    (1,1),
    (2,2),
    (3,3),
    (4,4)
]

f_matrix = [
    [x, square_inc(y) for x,y in pair] for pair in matrix
]
```

## Bônus: `*args` e `**kwargs` em funções

Vimos no último tutorial que podemos utilizar argumentos com valores padrão na assinatura de funções. Isto está diretamente ligado às coleções que acabamos de ver. Por exemplo: como uma função `print` consegue concatenar as *strings* separadas por vírgulas (ou seja, receber infinitos argumentos e concatená-los)? Podemos replicar este comportamento numa função de soma de números, por exemplo:

```python
def sum_numbers(*args): # o asterisco sinaliza que `args` é uma tupla
    total = 0
    for n in args:
        total += n
    return total

print(sum_numbers(1,2,3)) # 6
```

Podemos fazer isto para argumentos posicionais ou para argumentos de palavra-chave:

```python
def list_values(**kwargs): # os dois asteriscos sinalizam que `kwargs` é um dicionário
    values = []
    for key in kwargs:
        values.append(kwargs[key])

print(list_values(a=1, b=2)) # [1,2]
```

Na verdade, os operadores `*` e `**`, quando aplicado a listas e dicionários, podem descompatá-los não só para funções, mas para outros construtores.

```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}

dict3 = {**dict1, **dict2} # unindo os itens dos dois dicionários

# podemos fazer o mesmo em assinatura de funções
def add(n1, n2):
    return n1 + n2

values = (1,2)
print(add(*values)) # equivalente de add(1,2)
```

No próximo tutorial, veremos mais sobre como manipular *strings*. Por hora, pratique seus novos conhecimentos sobre coleções, pois eles abrem um mundo de possibilidades de novas implementações! Bons estudos!