# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Exceções

Vimos nós últimos tutoriais sobre estruturas de controle, a saber, estruturas condicionais e de repetição. No entanto, algumas situações podem causar erros que, se não tratados, podem levar a uma parada abrupta do código. Estes erros no mundo da programação são chamados de **exceções** (*exceptions*).

> No ecossistema Python, as exceções são comumente nomeadas como *Errors*.

### Como tratar erros

Vejamos um caso de um programa simples que pode causar uma exceção:

```python
num1 = int(input('Dividendo: '))
num2 = int(input('Divisor: '))
print(f'Resultado: {num1 / num2}')
```

Diversas exceções podem acontecer neste programa. A primeira delas é o caso do usuário escrever letras ao invés de números na entrada - isso causaria um `ValueError`. O segundo erro possível é se o usuário digitar um zero no segundo `input`, causando um `ZeroDivisionError`.

Para evitarmos uma saída abrupta do código - o que pode ser um problema sério em programas maiores, podemos usar uma estrutura de **tratamento de exceções**. Estruturas assim são úteis quando executamos código que podem gerar erros.

> Em algumas situações, nós inclusive podemos criar e lançar nossas próprias exceções. Mas isto será abordado em outro módulo deste tutorial.

Esta funcionalidade é alcançada através da seguinte estrutura:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    print(f'Resultado: {num1 / num2}')
except: # se não especificado, o except captura qualquer exceção
    print('Houve um erro no programa')
```

Neste caso, tudo o que está dentro do bloco delimitado pela palavra chave `try` é "protegido" pelo `except`, que entra em ação caso alguma exceção seja lançada pelo código. Podemos também especificar qual exceção deve ser capturada pelo bloco, e encadear mais de um bloco `except`:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    print(f'Resultado: {num1 / num2}')
except ValueError:
    print('Dividendo e divisor devem ser números!')
except ZeroDivisionError:
    print('O divisor deve ser diferente de zero!')
```

É possível especificar mais de uma exceção num bloco `except`:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    print(f'Resultado: {num1 / num2}')
except ValueError, ZeroDivisionError:
    print('Houve um erro no programa')
```


Podemos também capturar a própria exceção:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    print(f'Resultado: {num1 / num2}')
except Exception as e: # Exception é o tipo base, no entanto, é possível ser mais específico
    print(f'Houve um erro no programa: {e}') # imprime a mensagem contida na exceção
```

É possível também utilizar um bloco `else` encadeado nesta estrutura, que será executado apenas se o bloco `try` não lançar nenhuma exceção:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    resultado = num1 / num2
except:
    print('Houve um erro no programa')
else:
    print(f'Resultado: {resultado}')
```

Por fim, podemos especificar um bloco que será executado **independentemente** de exceções, ao final da estrutura: o bloco `finally`:

```python
try:
    num1 = int(input('Dividendo: '))
    num2 = int(input('Divisor: '))
    resultado = num1 / num2
except:
    print('Houve um erro no programa')
else:
    print(f'Resultado: {resultado}')
finally:
    print('Fim do programa')
```

Por fim, podemos também lançar uma exceçãoa, o que pode ajudar a explicar melhor os erros do nosso programa:

```python
num1 = int(input('Dividendo: '))
num2 = int(input('Divisor: '))

if num2 == 0:
    raise ValueError('O divisor deve ser diferente de zero!')
```

### O conceito de *call stack*

É importante entendermos um conceito fundamental na programação para compreendermos bem como funcionam e como são tratadas as exceções: a **pilha de chamadas** ou ***call stack***. Um programa de computador é basicamente uma estrutura de pilha (onde o primeiro que entra é o último a sair, e vice versa - *last in, first out*). Quando uma função - assunto do próximo tutorial, mas que será introduzido aqui brevemente - é chamada, como a função `input` ou `print`, uma chamada é adicionada na *call stack*. E após o término desta função, ela deixa a pilha e retorna para a função anterior, até que o programa encerre e a chamada original seja finalizada.

Podemos definir funções no Python usando a palavra chave `def`:

```python
def funcao():
    print('Chamada de função')
```

Imaginemos agora um cenário um pouco complexo: funções que chamam outras funções. Pensemos isso para o programa anterior, onde há uma função `main` (principal) e uma função `divisao`:

```python
def divisao(num1, num2):
    return num1 / num2 # aqui retornamos o valor desta divisão
def main():
    try:
        num1 = int(input('Dividendo: '))
        num2 = int(input('Divisor: '))
        print(f'Resultado: {divisao(num1, num2)}')
    except ValueError:
        print('Dividendo e divisor devem ser números!')
    except ZeroDivisionError:
        print('O divisor deve ser diferente de zero!')

# No Python, cada linha é interpretada sequencialmente, ou seja
# as funções serão interpretadas e ao final, chamaremos a função `main`
main()
```

A pilha de chamadas, considerando um fluxo sem exceções do programa, será a seguinte:

1. Inicialização do programa
2. Inicialização do programa → `main`
3. Inicialização do programa → `main` → `input` (que também é uma função)
4. Inicialização do programa → `main` → `input` (segunda chamada `input`)
4. Inicialização do programa → `main` → `print`
5. Inicialização do programa → `main` → `print` → `divisao`
6. Inicialização do programa → `main` → `print`
7. Inicialização do programa → `main`
8. Programa encerrado

Ou seja, sempre que uma função executa seu bloco de código, ela deixa a pilha. Por que estamos introduzindo este conceito, antes mesmo de introduzirmos o conceito de funções? Acontece que, quando uma exceção é lançada, ela buscará um bloco de código `try`-`except` na função onde foi lançada a exceção. Se o bloco de tratamento não está presente na função, ela é removida da pilha e a exceção passa para a função seguinte, que fará o mesmo processo. Se nenhuma função tiver um bloco de tratamento, a saída de erro com a exceção (chamada de *stack trace*) mostra exatamente por onde a exceção passou - o que é importante para *debug* (depurar nosso código).

> Experimente o código deste último exemplo sem um bloco `try`-`except`, com um divisor igual a zero, e veja quais funções foram chamadas no *stack trace*.

No próximo tutorial, estudaremos melhor os conceitos de funções em Python. Bons estudos!