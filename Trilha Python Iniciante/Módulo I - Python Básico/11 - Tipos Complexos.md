# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Tipos Complexos

No último tutorial, vimos como utilizar bibliotecas externas à `stdlib` e também como instalar módulos adicionais utilizando o `pip`. A grande maioria das bibliotecas, ou melhor dizendo, até mesmo a grande maioria dos módulos nativos do Python se baseiam em uma forma de programar fundamentada na definição de tipos complexos: a **orientação a objetos** (OO).

Teremos um próximo módulo da **Trilha Python Iniciante** que será completamente dedicado a este assunto. No entanto, gostaríamos de fazer uma breve introdução à OO, visto que este é um tópico fundamental para dominar conceitos mais avançados de qualquer linguagem de programação.

### Definindo tipos complexos

Utilizamos até agora tipos complexos definidos pelo próprio Python, como o tipo `list`, `dict`, `set` e `tuple` (as coleções básicas). Podemos importar outros tipos complexos a partir das diversas bibliotecas do ecossistema da linguagem, porém podemos definir também os nossos próprios tipos complexos. No mundo da OO, estes tipos complexos são chamados de **objetos**. Ou seja, a partir de agora, tudo será *orientado a objetos*, ou seja, tudo serão objetos.

Um objeto é uma unidade de programação que define em si atributos e funções, e interage com outros objetos. A definição de um objeto é chamada de **classe**, e uma variável de um determinado objeto é chamada de **instância**. Vamos definir um objeto do tipo carta de baralho.

```python
class Card: # tipo carta
    def __init__(self, rank, suit):
        self.rank = rank # "rank", valor
        self.suit = suit # "suit", naipe

card = Card('Ás', 'Espadas')
print(f'Carta: {card}')
```

Calma, vamos ver uma informação por vez. Como dito anteriormente, a definição de um objeto é uma classe, neste caso, um bloco de código definido pela palavra reservada `class`. Ainda se recorda sobre os padrões de nomenclatura? Então, no mundo Python, nomes de classes definidas pelo usuário são escritas em *PascalCase*.

Lembra de quando usamos os tipos de coleções (por exemplo, `list`) como uma função, e chamamos isto de **construtor**? Então, é isto que faz a função `__init__`, marcada especialmente pelo *dunder*.

> No mundo Python, funções de classes marcadas com *dunder* são chamadas de **métodos mágicos**. Teremos um tutorial para tratarmos especialmente deste tópico no módulo sobre Orientação a Objetos.

O que significa a variável `self`? Então, ela é o ponteiro da instância que chama a função. Vejamos um exemplo com listas:

```python
# Instanciemos um objeto do tipo `list`

array = list()

array.append(0) # chamamos a função `append`

# seria perfeitamente possível utilizar:

list.append(array, 0) # onde array é o ponteiro `self`
```

Como visto na penúltima linha, *instanciamos* um objeto do tipo carta ao chamarmos o construtor da classe. No entanto, o `print` nos dá uma informação confusa, como `<__main__.Card object at 0x...>`. Para imprimirmos os **atributos** da classe (neste caso, naipe e valor), usamos a seguinte sintaxe.

```python
print(card.rank) # Ás
print(card.suit) # Espadas
```

Vemos então um padrão básico: definimos objetos através de classes, e suas características através dos atributos. Porém, objetos podem conter funções dentro de si. Podemos definir tanto funções como procedimentos, acessando os atributos da classe através do ponteiro `self`.

```python
class Card: # tipo carta
    def __init__(self, rank, suit):
        self.rank = rank # "rank", valor
        self.suit = suit # "suit", naipe

    def show(self): # mostrar carta
        return f'{self.rank} de {self.suit}'

card = Card('Ás', 'Espadas')
print(f'Carta: {card.info()}') # retorna a string da função `show`
```

> No mundo orientado a objetos, funções pertencentes a classes são chamadas de **métodos**.

### Bônus: o método mágico `__str__`

E se pudéssemos sobrescrever a conversão de um objeto para *string*, ou melhor, se pudéssemos customizar o que é retornado ao passarmos ele para a função `print`? É isso que faz o método mágico `__str__`:

```python
class Card: # tipo carta
    def __init__(self, rank, suit):
        self.rank = rank # "rank", valor
        self.suit = suit # "suit", naipe

    def __str__(self): # equivalente de str(card)
        return f'{self.rank} de {self.suit}'

card = Card('Ás', 'Espadas')
print(f'Carta: {card}') # retorna a string do método mágico __str__
```

### Conclusão do Módulo

Meus parabéns, você chegou ao final do módulo Python Básico, o primeiro módulo da trilha Python Iniciante do nosso Tutorial Python! Agora, você está pronto para começar a aprender conceitos mais avançados de orientação a objetos! Revise sempre o conteúdo e divirta-se com seus novos conhecimentos. Bons estudos! 