# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Manipulação de Arquivos

> Uma observação fundamental para este tutorial: nos sistemas baseados em Linux e no Mac, URLs de pastas são separados pelo caractere `/`, enquanto que no Windows, pastas são separadas pelo caractere `\`. Neste tutorial, usaremos o padrão Linux\Mac.

No último tutorial, vimos os principais métodos para a manipulação de *strings*. Hoje, veremos como manipular *buffers* de arquivos de texto.

A maioria dos arquivos são nada mais do que grandes *strings*. Em alguns casos, como para os arquivos `.docx` (documentos) e `.xlsx` (planilhas), são pastas compactadas de vários arquivos de textos (neste caso, arquivos XML). Hoje, vamos aprender a como ler e manipular arquivos de texto simples.

Vamos escrever um texto simples em um `arquivo.txt`:

```
Olá! Este é meu primeiro arquivo de texto
manipulado com o interpretador Python.
```

Para abrir este arquivo, utilizaremos o seguinte código:

```python
# para isto, o script Python deve estar na mesma pasta do arquivo
file = open('./arquivo.txt')
content = file.read() # lê o arquivo como uma string única
print(content) # imprime o conteúdo do arquivo
file.close() # fecha o arquivo
```

Se quisermos realizar uma segunda leitura do arquivo, precisamos usar a função `seek` para retornar o ponteiro de memória para o começo do arquivo:

```python
file.seek(0)
```

Podemos também ler o arquivo como uma lista de *strings* ao invés de uma cadeia única:

```python
contents = file.readlines() # lista de strings
```

A função `open` pode receber um segundo parâmetro, que é o modo de leitura do arquivo:

- `r` (*read*), valor padrão; apenas lê o arquivo, retorna um erro caso ele não exista
- `a` (*append*), adiciona conteúdos ao final do arquivo; caso o arquivo não exista, será criado
- `w` (*write*), sobrescreve o conteúdo do arquivo; caso o arquivo não exista, será criado
- `x` (*create*), cria o arquivo, retorna um erro caso ele exista

Podemos também especificar no parâmetro um segundo caractere: `t` (leitura em modo de texto, valor padrão), ou `b` (leitura em modo binário). O modo binário é usado para arquivos de codificação binária, como imagens e PDFs.

> Podemos também especificar leitura e escrita simultânea com os modos `r+`, `w+` e `a+`.

Vejamos um exemplo de criação de um arquivo em modo *append*:

```python
# para evitar a linha da função .close(), podemos utilizar o bloco `with`-`as`
with open('arquivo2.txt', 'a') as file:
    content = 'Meu primeiro arquivo criado com Python\n=D'
    file.write(content)
```

Podemos também utilizar um loop `for` para percorrer as linhas do nosso arquivo:

```python
# Valor padrão de codificação: UTF-8
with open('arquivo.txt', encoding='utf-8') as file:
    for line in file: # percorre cada linha do arquivo
        print(line)
    file.seek(0) # caso desejemos fazer outra operação com o mesmo arquivo
```

> Um outro exemplo de codificação comum é a codificação `latin-1`. Isto será especialmente importante para lidarmos com arquivos em análise de dados, como o formato CSV.

No próximo tutorial, veremos como estender as funcionalidades do nosso interpretador com módulos extras, as chamadas bibliotecas. Bons estudos!