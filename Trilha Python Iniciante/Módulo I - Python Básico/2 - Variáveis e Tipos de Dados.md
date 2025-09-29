# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Variáveis e Tipos de Dados

### Tipos Primitivos

Você aprendeu, no tutorial anterior, sobre o programa *Hello World*, as funções `print` e `input`, e também alguns outros conceitos. Consegue recordar o significa `stdin` e `stdout`? Aprendemos que podemos delimitar textos através de aspas simples, e que a função `input` retorna tudo o que for passado em `stdin`, e que estes valores podem ser  armazenados em **variáveis**. Hoje, vamos falar mais sobre elas.

Vamos recordar um pouco o nosso primeiro *Hello World*, o mais simples, que possui apenas uma linha:

```python
print('Hello World')
```

Podemos declarar cadeias de texto arbitrário usando aspas simples ou duplas em Python. Tudo o que está fora de aspas simples será interpretado como instrução de código, como variáveis, apesar de que há algumas palavras reservadas no Python. Cadeias de texto são chamadas de *strings* no mundo da programação, e o Python chama esse tipo pela sigla `str`. As *strings* ou cadeias de caracteres são o nosso primeiro tipo de dados, ou seja, o primeiro tipo de informação que podemos armazenar.

Experimente executar este código para conferir a sua saída:

```python
print(type('Hello World')) # Saída: <class 'str'>
```

Aproveitando: o que significa este asterisco (`#`)? Isto é um **comentário**: tudo que é escrito em uma linha depois de um asterisco é simplesmente ignorado, salvo se ele estiver dentro de uma *string*. Ou seja, podemos comentar o nosso código dessa maneira. Vimos também a função `type`, que retorna o tipo de um valor em Python.

Podemos também definir outros três tipos de dados primitivos em Python: dois são numéricos e o terceiro é utilizado para valores lógicos. Para números inteiros, é usado o tipo `int`:

```python
number = 1
print(type(number)) # Saída: <class 'int'>
```

Caso precisemos trabalhar com números decimais, utilizaremos o tipo `float` ou ponto flutuante:

```python
decimal = 0.5 # parte flutuante separada por ponto
print(type(decimal)) # Saída: <class 'float'>
```

Por fim, temos o tipo **booleano**, ou como é chamado em Python, apenas `bool`. O tipo booleano recebe dois valores possíveis: verdadeiro (`True`) ou falso (`False`). Algumas funções e outras estruturas retornam valores lógicos - veremos mais sobre isso no tutorial seguinte sobre estruturas condicionais.

```python
logic_value = True # ou False
print(type(logic_value)) # Saída: <class 'bool'>
```

Falemos agora sobre duas coisas a respeito das variáveis. Nestes tutoriais, usaremos como padrão nomes de variáveis em inglês, o que pode evitar a troca de referência (*code switching*) entre textos em português e inglês. Além disso, observe como está escrita a variável `logic_value`: ela segue um padrão chamado *snake case*, que escreve nomes de variáveis sempre minúsculos e com palavras separadas por *underlines* (`_`). Alguns tipos de convenções de escrita de referências em programação são:

- *Snake case*: `logic_value`, `new_value`
    + No Python, é utilizado para nomes de variáveis e funções

    + valores constantes são declarados com *snake case* maiúsculo: `CONST_VALUE`
- *Camel case*: `logicValue`, `newValue`
- *Pascal case*: `LogicValue`, `NewValue`
    + no Python, é utilizado para nomes de classes
- *Kebab case*: `logic-value`, `new-value`

É importante conhecer as convenções de nomenclatura para seguir as **boas práticas**, isto é, algo que não é errado se não for feito, mas se espera que se faça daquela maneira e também facilitará o trabalho de outros programadores.

Falemos também sobre valores **constantes**: algumas variáveis possuem valor imutável. No Python, não é possível "congelar" o valor de uma variável, mas por convenção, se uma variável é declarada com *snake case* maiúsculo, seu valor não será alterado e isso será respeitado ao longo do código.

Outra coisa que ficou implícita é que o retorno da função `input` é um valor do tipo `str`. Para recuperarmos um valor de outro tipo, podemos usar os tipos como funções da seguinte forma:

```python
int_value = int(input('Digite um valor inteiro: '))
float_value = float(input('Digite um valor decimal: '))
bool_value = bool(input('Digite um valor lógico: ')) # qualquer texto possui valor lógico True, inclusive a string 'False', exceto a string '' (vazia e sem espaços)
```

A função `int`, por exemplo, converte a *string* em um valor inteiro (ou `float`, ou `bool` respectivamente). No entanto, se tentarmos converter uma string `'a'` para inteiro, receberemos um erro do tipo `TypeError`, e o nosso programa fechará inesperadamente. Aprenderemos a lidar com erros de uma maneira mais graciosa mais à frente, mas por hora, tentaremos evitá-los a todo custo. Para saciar nossa curiosidade, podemos converter um único caractere em inteiro (valor de referência da tabela ASCII) com a função `ord`.

> Esta conversão entre tipos é chamada de ***type casting***.

### Operadores

Assim como na matemática, a linguagem Python possui **operadores** (sinais de operação), que interagem com tipos de dados de maneiras diferentes. Vejamos agora alguns dos operadores presentes em Python.

Podemos somar, subtrair, multiplicar e dividir tipos numéricos em Python:

```python
value1 = 1 + 1 # adição
value2 = 1 - 1 # subtração
value3 = 2 * 2 # multiplicação
value4 = 10 / 2 # divisão
value5 = 10 ** 2 # potência
```

Todas as operações acima possui como operandos (isto é, os valores submetidos à operação) valores do tipo `int`. A adição, subtração e a multiplicação de inteiros retornam valores `int`, exceto a divisão, que retorna um `float`. Para obtermos o quociente (parte inteira) de uma divisão, usando o operador `//`, e obteremos o resto da divisão usando o operador *mod* (`%`). Se somamos um inteiro e um flutuante, ou realizamos uma subtração ou multiplicação entre inteiro e flutuante, o valor resultante será um `float`.

Por quê? A diferença entre tipos de dados está no número de *bits* (casas binárias) utilizados para armazenar cada variável:

- O tipo `str` é uma coleção de caracteres, geralmente 8 bits por caractere
- Já o tipo `int` geralmente utiliza 28 bits ($-2^{14}$ até $2^{14} - 1$)
- O tipo `float` utiliza 64 bits
- O tipo `booleano` utiliza o mesmo tamanho do tipo inteiro, apesar de poder ser representado por um único bit

É possível também alterar o valor de variáveis usando estes operadores:

```python
value1 = 1
value1 = value1 + 1
```

Ou de maneira mais curta:

```python
value1 += 1
# Também é possível utilizar -=, *=, /=, //=, %=
```

> O sinal de `=` é também chamado de **operador de atribuição**.

O que acontece, no entanto, se "somarmos" duas *strings*? Esta operação é chamada de **concatenação**. Experimente este código:

```python
print('Hello' + ' World')
```

O operador `+` é suportado por *strings*. No entanto, se você tentar multiplicar duas *strings*, você verá um `TypeError`.

### Interpolação de Strings

Vimos que é possível concatenar, isto é, unir cadeias de caracteres. No entanto, como podemos misturar *strings* com valores declarados em variáveis, isto é, realizar uma **interpolação**? O Python possui três maneiras para fazer isso:

1. O estilo "antigo", utilizando o operador `%`
2. O estilo "novo", usando a função `format`
3. *F-strings*

O estilo "antigo" é uma herança da linguagem C. Ele utiliza o operador *mod* para interpolar *strings*:

```python
name = 'Symon'
print('Hello, %s!' % name)
```

Se quisermos interpolar mais de um valor, precisamos utilizar parêntesis da seguinte forma:

```python
name1 = 'Symon'
name2 = 'Aluno'
print('Hello, %s and %s!' % (name1, name2))
```

O estilo antigo converte um valor para um dos tipos primitivos, segundo estas convenções:

- `%s` - valor `str`
- `%d` - valor `int`
- `%f` - valor `float`
    + para especificar o número de casas decimais: `%.2f` (para duas casas decimais, como por exemplo, imprimir moedas)

    + para imprimir apenas a parte inteira, `%.0f`

Já o estilo "novo" utiliza uma função chamada `format`:

```python
name = 'Symon'
print('Hello, {}!'.format(name))
```

Ou seja, utilizamos apenas chaves (`{}`) e sequencialmente, os valores passados à função `format` serão inseridos na nossa *string*:

```python
name1 = 'Symon'
name2 = 'Aluno'
print('Hello, {} and {}!'.format(name1, name2))
```

Para casas decimais de valores do tipo `float`, há uma regra similar ao estilo antigo:

```python
price = 0.5 # preço de 50 centavos
print('O preço é R${:.2f}'.format(price))
```

No entanto, a versão 3.6 do Python introduziu a técnica de *f-strings*. Ela segue um estilo similar ao `format`:

```python
name = 'Symon'
print(f'Hello, {name}')
```

Para flutuantes, segue-se também um padrão similar:

```python
price = 0.5
print(f'Preço: {price:.2f})')
```

Qual estilo usar? O estilo de *f-strings* parece ser mais fácil e amigável para iniciantes, porém isso depende da preferência de cada programador. Contudo, às vezes um estilo específico pode tornar a interpolação de *strings* mais limpa, dependendo do caso. Suponhamos a escrita de uma *string* que fosse passada como comando a um terminal, onde houvesse diversas aspas. Neste caso, o estilo antigo pode tornar o código mais legível. Ou digamos que o nosso código seja executado em versões do Python pré-3.6: a compatibilidade pode ser alcançada usando a função `format`.

Há uma última observação para ser feita sobre *strings*: como escrever aspas simples ou duplas nelas, se elas também são o delimitador das próprias *strings*? Entram aí os **caracteres de escape**. O primeiro caractere de escape delimita um salto de linha:

```python
print('Olá!\nSeja bem vindo ao Python!')
# por padrão, todo `print` possui como final o caractere \n
```

Para escrever aspas simples ou duplas, use um caractere de escape:

```python
print('\"Exemplo de citação\"') # Saída: "Exemplo de citação"
```

Há também:

```python
print("\tExemplo de tabulação")
print("Módulo I - Python Básico\\Trilha Python Iniciante") # para escrever o próprio caractere `\`
```

### O valor *None*

Existe ainda um último tipo de dado, o valor `None`: ele representa um valor vazio. Na prática, ele é uma referência a um ponteiro de memória inexistente. Utilizar valores `None` em operações pode resultar em erros, fique atento.

```python
value = None
```

No próximo tutorial, começaremos a dar usos mais práticos para as variáveis que aprendemos hoje através das estruturas condicionais.