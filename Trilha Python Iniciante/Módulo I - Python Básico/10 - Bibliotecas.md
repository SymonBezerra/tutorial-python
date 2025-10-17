# Trilha Python Iniciante - Symon Bezerra
## Módulo I - Python Básico → Bibliotecas

### Importando bibliotecas

No último tutorial, vimos como manipular arquivos com o interpretador Python. Até agora, só utilizamos as funções da biblioteca padrão (<em><strong>st</strong>andar<strong>d lib</strong>rary</em>, ou `stdlib`). Neste tutorial, veremos como utilizar bibliotecas extras, algumas fornecidas junto com o próprio interpretador Python.

Podemos importar uma biblioteca usando a palavra chave `import`. Vamos começar pela biblioteca de funções matemáticas, `math`:

```python
import math

print(math.sqrt(100)) # 10.0 → raiz quadrada
print(math.cbrt(1000)) # 10.0 → raiz cúbica
print(math.floor(100.5)) # 100 → arredondamento para o primeiro inteiro abaixo
print(math.ceil(100.5)) # 101 → arredondamento para o primeiro inteiro acima
print(math.exp(5)) # e^5
print(math.exp2(10)) # 2^10
print(math.cos(0)) # 1 → cosseno
print(math.sin(0)) # 0 → seno
print(math.pi) # constante pi
```

Uma observação sobre as funções trigonométricas: elas estão em radianos. Para converter para radianos um valor em graus, use a função `math.radians`.

```python
# cosseno de 45° == raiz de 2 dividido por 2
print(math.cos(math.radians(45)) == math.sqrt(2) / 2) # True
```

Outra biblioteca que podemos importar é a biblioteca `random`:

```python
import random

random.seed(42) # insere uma seed no gerador de números
# assim, os resultados são reproduzíveis

print(random.random()) # número float aleatório
dice = list(range(1, 7)) # dado de 6 lados
print(random.choice(dice)) # escolhe um número da lista
print(random.randint(1, 6)) # número aleatório inteiro no intervalo [a,b]
print(random.choices(dice, k=6)) # seis jogadas do dado de seis lados
print(random.shuffle(dice)) # embaralha os valores
print(random.randrange(0, 10, 2)) # escolhe um número entre 0, 2, 4, 6 ou 8
```

Algumas bibliotecas que já vêm instaladas junto do interpretador Python e que são bastante utilizadas em vários projetos:

- `collections`, coleções extras de dados, como filas e dicionários-padrão
- `datetime`, utilitários para manipulação de *timestamps* (data e hora)
- `json`, funções para trabalharmos com o formato de arquivo JSON
- `os`, funções relacionadas ao sistema operacional e ao terminal
- `requests`, funções para requisições HTTP (internet)
- `time`, funções de relógio

### O gerenciador de pacotes `pip` e o ambiente virtual `venv`

Para a instalação de bibliotecas externas, temos duas ferramentas:

- O gerenciador de pacotes do Python, o `pip`, que realiza o *download* e a instalação de bibliotecas adicionais no nosso interpretador.
- O ambiente virtual (<em><strong>v</strong>irtual <strong>env</strong>ironment</em>, ou `venv`), que gera uma instalação isolada para que possamos instalar versões específicas de bibliotecas num pacote de bibliotecas.

> A utilização de `venv`'s é uma boa prática, pois com a atualização das bibliotecas, funcionalidades que implementamos com versões anteriores podem se tornar inutilizáveis.

Vamos criar o nosso primeiro `venv` com o seguinte comando:

```sh
# Válido para Linux\Windows
python3 -m venv venv # criar um venv numa pasta chamada "venv"
```

Para ativar, podemos utilizar o seguinte comando:

```powershell
# Windows
./venv/bin/Activate.ps1
```

```sh
# Linux
source venv/bin/activate
```

> O `venv` basicamente sobrecarrega o comando `python3` do seu terminal, fazendo com que todas as execuções de código Python se refiram ao ambiente virtual e suas bibliotecas, ao invés do interpretador instalado globalmente. Para desativá-lo, tanto no Windows como no Linux, basta usar o comando `deactivate`.

A partir daí, podemos utilizar o comando `pip` para instalar uma biblioteca. Vamos utilizar como exemplo neste tutorial o módulo `BeautifulSoup`:

```sh
pip install beautifulsoup4
```

O módulo `BeautifulSoup` provê utilitários para trabalharmos com conteúdos XML/HTML, o que é especialmente útil para lermos conteúdos de páginas da Web (uma técnica chamada de *web scraping*). Vamos fazer um exemplo misturando as bibliotecas `BeautifulSoup` e `requests`, esta última já instalada com o interpretador Python.

> É importante ler a documentação de uma biblioteca ou *framework* ao decidir utilizá-la.

```python
# importe primeiro módulos nativos
import requests

# depois os módulos adicionais
from bs4 import BeautifulSoup # equivalente de import bs4.BeautifulSoup

# caso existam, módulos criados pelo usuário por último

URL = 'https://docs.python.org/pt-br/3/library/venv.html' # documentação do módulo `venv

# extrair conteúdo com requisição GET
content = requests.get(URL).content

# realizar parsing (leitura) do conteúdo HTML com BeautifulSoup
soup = BeautifulSoup(content, 'html.parser')

# a estrutura da página pode ser analisada com o inspetor do navegador
# procurar pela tag <div> com a classe 'body'
text_body = soup.find('div', {'class': 'body'})

# escrever conteúdo de texto num arquivo
with open('documentacao_venv.txt', 'w') as file:
    file.write(text_body.text)
```

### Criando nossa própria biblioteca

Por fim, é possível criarmos nossos próprios módulos e bibliotecas e importá-los na nossa estrutura de código. Para isso, basta criarmos um script, que chamaremos aqui de `library.py`, e importá-lo no código principal.

```python
# library.py
CONST_VALUE = 1000

def fn(n1, n2):
    return n1 + n2
```

```python
# script.py → código principal

import library

print(library.CONST_VALUE) # 1000
print(library.fn(1, 2)) # 3

```

Deste modo, podemos criar nossas próprias bibliotecas, o que torna o nosso código mais modular e mais estensível, organizado em arquivos menores e menos monolíticos.

> Veremos mais sobre o gerenciamento de bibliotecas criadas por usuário e pacotes no módulo sobre **Ambiente de Desenvolvimento**.

### Bônus: `if __name__ == '__main__'`

Alguns programadores Python utilizam a seguinte diretiva para testar seus *scripts*:

```python
# library.py
CONST_VALUE = 1000

def fn(n1, n2):
    return n1 + n2

print('Biblioteca importada')

if __name__ == '__main__': # __...__ → "dunder" (double underscore)
    print('Este script é uma biblioteca, não deve ser executado sozinho')
```

O que esta linha de código faz é acessar a variável `__name__` (uma variável do próprio interpretador, por isso marcada pelo *dunder*) e, se o valor desta variável for `__main__` (ou seja, se o *script* for executado sozinho ao invés de ser importado por outro arquivo de código), o bloco de código será executado.

Isto significa que o primeiro `print` será executado sempre, seja ao importar o *script* como biblioteca, seja ao executá-lo sozinho. Isto é bastante útil para testarmos funcionalidades das nossas bibliotecas em estruturas mais simples.

Aproveite os novos conhecimentos e explore bastantes novas bibliotecas. Lembre sempre de consultar as documentações e tutoriais. Bons estudos!