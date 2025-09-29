# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Estruturas de Repetição

### De novo, tantas vezes!

Vimos no último tutorial como utilizar estruturas condicionais `if`, `else` e `elif`, e como encadeá-las. Também vimos como trabalhar melhor com valores booleanos. Hoje veremos como repetir instruções dentro de blocos de código, as chamadas **estruturas de repetição**.

As estruturas de repetição são mais um recurso para criarmos *scripts* em Python. Temos dois tipos de estruturas de repetição: uma estrutura *finita* e uma (potencialmente) *infinita*. Na realidade, não é bom que o nosso código rode para sempre e devore toda a memória do computador. Isso poderia ser feito com estas linhas de código:

```python
# NÃO EXECUTE ESSE CÓDIGO
# Se executar, pare-o com Ctrl-C
while True:
    print('Hello World') # imprime Hello World indefinidamente
```

Comecemos pela estrutura infinita, o `while`: ela é ativada por valores booleanos, ou seja, *enquanto* dada condição for verdadeira, o bloco de código será executado. Vejamos um exemplo melhor:

```python
# Imprime números de zero até dez
n = 0
while n <= 10:
    print(n)
    n += 1
```

No entanto, podemos alcançar a mesma funcionalidade com uma instrução finita, o *loop* `for`. Vejamos o exemplo:

```python
for i in range(11): # convencionalmente, uma variável sobre um loop for é chamado de `i` (de iterativo)
    print(i)
```

Vamos explicar melhor a estrutura de um `for` simples. O *loop*`for` no Python é iterativo, ou seja, ele percorre um conjunto de elementos. Podemos percorrer qualquer objeto iterável - veremos sobre isso mais à frente no tutorial sobre coleções. No nosso caso, vamos percorrer um objeto `range`, função do tipo *generator* que retorna uma lista de elementos $[a,b) $. Ou seja:

```python
# função range(início, fim, incremento)
# se for passado apenas um argumento, será o argumento fim
range(10) # intervalo [0,9]
range(1, 10) # intervalo [1, 9]
range(1, 10, 2) # [1, 3, 5, 7, 9], ou seja, de um a nove, incrementando de dois em dois
```

> Em outras linguagens, este tipo de estrutura é chamada de *for-each* ("para cada"). O Python utiliza exclusivamente *for-eachs*.

Podemos inclusive misturar estruturas condicionais e *loops*:
```python
n = 0
while n <= 20:
    if n % 2 == 0: # se é par
        print(n)
```

> Experimente fazer o mesmo *loop* usando um comando `for`.

## O conceito de escopo

Já que vimos dois tipos de estruturas de controle em Python, está na hora de introduzirmos um conceito importante para gerenciamento de variáveis: o **escopo**. O escopo de uma variável depende de onde ela foi declarada. Se ela for declarada fora de um bloco de código, será **global** para aquele *script*. Caso contrário, ela será **local** dentro daquele escopo de código.

Vejamos um exemplo:

```python
n = 100
print(n) # 100
for i in range(10):
    n = i * 2
    print(n) # 0, 2, 4,  6, 8, 10, 12, 14, 16, 18
print(n) # 18, pois a variável n foi redefinida dentro do bloco for
```

Veremos mais sobre escopo de variáveis quando estudarmos funções, onde teremos que ser mais atenciosos com variáveis locais e globais.

Caso removamos a primeira linha:

```python
print(n) # 100
for i in range(10):
    n = i * 2
    print(n) # 0, 2, 4,  6, 8, 10, 12, 14, 16, 18
print(n) # 18, pois a variável n foi CRIADA dentro do bloco for
```

### Break, continue e pass

O Python possui três palavras reservadas que podem ser utilizadas para alterar o fluxo de estruturas de repetição. São elas `break`, `continue` e `pass`.

Se desejamos interromper um *loop*, podemos utilizar a instrução `break`:

```python
n = 0
while True:
    n += 1
    print(n)
    if n > 10: break # Bônus: se o bloco de código possui apenas uma linha, podemos escrevê-lo na mesma linha
```

O mesmo pode ser usado para *loops* `for`:

```python
# imprimir números primos de 1 a 100
for i in range(1, 101):
    prime_number = False # número primo
    for j in range(1, i):
        if i % j == 0: # divisível por
            prime_number = True
            break # já que encontramos um divisor, não precisamos calcular os restantes
    if prime_number: print(f'{i} é primo')
```

Se desejamos saltar a condição, podemos utilizar a instrução `continue`:

```python
for i in range(100):
    # imprimir números pares
    if i % 2 == 0: continue
    print(i)
```

Um outro exemplo com `while`:

```python
n = 0:
while n <= 100:
    n += 1
    prime_number = False
    div = 0
    while not prime_number or div < n:
        div += 1 # cuidado com a divisão por zero - ZeroDivisionError!
        if n % div == 0:
            prime_number = True
    if prime_number: continue
    print(f'{n} é primo')
```

Se desejamos apenas ignorar uma instrução ou deixar um bloco de código vazio, podemos utilizar o `pass`:

```python
for i in range(10):
    pass # não executa nada, apenas percorre o iterador de zero a nove
```

Você deve ter visto no penúltimo exemplo o erro `ZeroDivisionError` sendo citado. No próximo tutorial, aprenderemos a lidar com erros e como tratá-los, impedindo o nosso código de ser interrompido abruptamente. Bons estudos!