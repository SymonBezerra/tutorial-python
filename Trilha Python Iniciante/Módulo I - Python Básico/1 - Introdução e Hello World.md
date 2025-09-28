# Trilha Python - Symon Bezerra
## Módulo I - Python Básico → Introdução e Hello World

Seja bem vindo ao fantástico mundo da programação em Python. Aqui você aprenderá os conhecimentos necessários sobre lógica de programação para se tornar um desenvolvedor nesta linguagem que já é uma das mais populares, se não a mais popular do mundo da computação.

A linguagem Python foi criada pelo cientista holandês Guido van Rossum em 1991, e atualmente se encontra na sua versão 3. Ela é uma linguagem de alto nível, isto é, intencionada como mais próxima à linguagem natural, e de uso geral. Algumas das áreas de aplicação da linguagem Python são as seguintes:

- Inteligência artificial, através de inúmeros SDKs (*kits* de desenvolvimento)
- Análise e engenharia de dados, através de bibliotecas como Pandas e PySpark
- Desenvolvimento Web, através de frameworks como Django, FastAPI e Flask
- Computação científica, com o Numpy
- Processamento de linguagem natural, com bibliotecas como `nltk`
- Desenvolvimento de jogos, com Pygame

Neste primeiro módulo, o Python Básico, aprenderemos as estruturas de código comuns a várias linguagens de programação e como elas são implementadas em Python.

### Seu primeiro programa: *"Hello, World!"*

O primeiro programa que todos os programadores escrevem é chamado de *"Hello, World!"* ("olá, mundo!"). Ele foi convencionado pelo cientista canadense Brian Kernighan, nos anos 70. Vejamos como implementá-lo em Python:

```python
print('Olá, mundo!')
```

Já no *Hello World* podemos ver algumas características chave da linguagem Python: ela possui uma sintaxe simples, baseada na própria língua inglesa; ela não faz uso de chaves (`{}`) e ponto-e-vírgulas (`;`) como delimitadores de instruções e blocos de código (como é o caso da linguagem C, da qual falaremos brevemente ao longo deste curso, pois ela é a linguagem "mãe" do Python); e ela serve perfeitamente para linguagem de *scripting*, isto é, criar pequenos roteiros de código que podem ser executados independentemente, pois tudo o que é escrito num código Python é executado sequencialmente. Veremos mais sobre isto ao longo do curso.

Explicando o programa: faremos uso da função `print`, que simplesmente imprime um texto na saída padrão (`stdout`, ou *standard output*) do terminal do computador. Você verá que boa parte dos programas escritos, especialmente nos níveis iniciais, usam a interface de linha de comando (*CLI*, ou *command-line interface*), ou seja, um terminal. Mais à frente, veremos como utilizar interfaces gráficas de *desktop* ou o navegador Web. Dentro da função `print`, passaremos um texto delimitado por aspas simples (ou duplas, mas neste curso daremos preferência às aspas simples). O programa *Hello World* pode imprimir qualquer coisa, pois a sua única função é testar a `stdout`.

Crie um arquivo `ola_mundo.py` com a linha de código acima, e execute-o com o comando `python3 ola_mundo.py`. Parabéns, você deu seu primeiro passo no mundo da programação Python.

Agora, vamos incrementar o programa com uma outra função:

```python
print('Olá, mundo!')
name = input('Qual é o seu nome?')
print('Olá, ' + name)
```

Faremos uso também da função `input`. Assim como existe uma função de saída padrão, existe uma função de entrada padrão (`stdin`, ou *standard input*). A função `input` recebe como argumento opcional um texto, que será impresso no terminal, e ficará aguardando por uma entrada do usuário. Escreva o código no arquivo `ola_mundo.py`, escreva seu nome do terminal, digite Enter e veja o que acontece. O seu nome será impresso ao executar a linha 3 do programa.

Vemos também dois aspectos das funções `print` e `input`: enquanto a função `print` apenas imprime um texto em `stdout`, a função `input` retorna o valor presente em `stdin`, que pode ser armazenado numa **variável**. Este será nosso próximo assunto, as variáveis e os tipos de dados que elas podem armazenar.

Por hora, comemore o seu primeiro passo no mundo da programação Python!