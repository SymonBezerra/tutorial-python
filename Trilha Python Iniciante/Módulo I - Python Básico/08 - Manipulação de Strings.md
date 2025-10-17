# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Manipulação de Strings

No último tutorial, vimos como manipular as coleções de dados básicas da linguagem Python. Hoje veremos como manipular uma coleção de dados bem específica: as cadeias de caracteres, ou *strings*.

Sim, toda *string* é basicamente uma lista de caracteres, então podemos aplicar técnicas parecidas com o que utilizamos para listas em *strings* e vice versa. Além disso, podemos manipular textos utilizando técnicas específicas para isto. Veremos algumas delas neste tutorial.

### Uma lista de caracteres

Como as listas e as tuplas, *strings* podem ser indexadas e até particionadas (o que no ecossistema Python é chamado de *slice*):

```python
text = 'Um texto em Python'
print(text[0]) # 'U'
print(text[0:3]) # 'Um' → intervalo [a,b), separado por `:`, no Python é chamado de `slice`

print(text[-1]) # 'n' → índice negativo conta a partir do último elemento
```

> Os `slices` e o operador de indexação também se aplicam às coleções lineares, como listas e tuplas. Outros métodos, como `index` e `count` também podem ser usados da mesma forma.

Podemos comparar *strings* ou extrair um valor booleano delas:

```python
text = input('> ')
if text: # qualquer texto
    print('Python' in text) # busca pela palavra 'Python' dentro da string
else:
    print('TEXTO VAZIO')
```

Um método interessante é nivelarmos a *string* em caracteres minúsculos ou maiúsculos, assim facilitando buscas por textos. No exemplo anterior, a saída seria `False` caso alguém escrevesse a palavra *"python"* com letras minúsculas.

```python
text = input('> ')
if text: # qualquer texto
    print('python' in text.lower()) # busca pela palavra 'Python' dentro da string
    # para letras em maiúsculo, podemos usar a função `upper`
else:
    print('TEXTO VAZIO')
```

Outra função interessante que pode servir bastante para a manipulação de nomes de arquivos é o método `endswith`:

```python
text_files = list() # arquivos de texto
miscellaneous_files = list() # outros arquivos
while True:
    filename = input('Nome do arquivo: ')
    if filename.endswith('txt'):
        text_files.append(filename)
    else:
        miscellaneous_files.append(filename)
```

> O comportamento inverso pode ser encontrado na função `startswith`.

Poderíamos simplificar este código utilizando também o método `split`, que divide a *string* em múltiplos pedaços a partir de um caractere separador. Caso o separador não esteja presente, a própria *string* é devolvida.

```python
text_files = list() # arquivos de texto
miscellaneous_files = list() # outros arquivos
while True:
    filename = input('Nome do arquivo: ')
    file_extension = filename.split('.')[-1].lower()
    # no caso de 'arquivo.txt', teríamos a lista ['arquivo', 'txt']
    if file_extension in ('txt', 'docx'):
        text_files.append(filename)
    else:
        miscellaneous_files.append(filename)
```

E se o nosso arquivo tiver espaços em branco ao final ou no início? Podemos usar a função `strip` para removê-los:

```python
text_files = list() # arquivos de texto
miscellaneous_files = list() # outros arquivos
while True:
    filename = input('Nome do arquivo: ').strip() # remover espaços ao final ou início
    file_extension = filename.split('.')[-1].lower()
    # no caso de 'arquivo.txt', teríamos a lista ['arquivo', 'txt']
    if file_extension in ('txt', 'docx'):
        text_files.append(filename)
    else:
        miscellaneous_files.append(filename)
```

Podemos também conferir se todos os caracteres são numéricos (`isnumeric`) ou letras (`isalpha`):

```python
text = input('Digite um número: ')
if text.isnumeric():
    print('Número válido')
```

Pratique bastante o uso destas funções. No próximo tutorial, veremos como manipular arquivos no nosso código. Bons estudos!