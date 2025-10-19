# Trilha Python Iniciante - Symon Bezerra
## Módulo II - Programação Orientada a Objetos → Introdução

> Recomendamos fortemente que você leia também o tutorial 11 do **Módulo Python Básico** desta mesma trilha, pois ele contém uma introdução mais detalhada à orientação a objetos.

Seja bem vindo ao segundo módulo da **Trilha Python Iniciante**! Hoje daremos início aos nossos estudos sobre **Programação Orientada a Objetos**, um paradigma essencial para entender diversas linguagens de programação, e especialmente compreender o ecossistema Python.

Neste módulo, buscaremos entender desde os conceitos básicos do paradigma até padrões de indústria que te tornarão um desenvolvedor cada vez mais completo no ecossistema Python.

### Uma nova maneira de escrever código

Até agora, tudo o que vimos sobre programação organiza o nosso código em **funções**. Nos primórdios da computação, elas sequer existiam. Aos poucos, surgiu o conceito de **subrotina**, em linguagens como o BASIC (que foi muito popular nos computadores domésticos de 8 bits dos anos de 1970 e 1980). No entanto, o código destas linguagens ainda contava com aspectos similares aos de programação em linguagem de máquina (*assembly*), o que tornava a organização das estruturas uma tarefa difícil.

Convencionou-se, então, uma série de princípios conhecidos como **programação procedural**, que organizava todo o código em funções e procedimentos. No entanto, códigos procedurais possuíam alguns problemas bem conhecidos:

- Repetição de código: reutilizar código procedural é algo difícil. Por exemplo, se criarmos uma série de procedimentos na nossa biblioteca para livros, precisaremos criar outros procedimentos para revistas, outros para artigos acadêmicos, e assim por diante.

- Falta de proteção de dados: como não há um encapsulamento natural, manter código procedural é difícil graças ao *shared state* (estados compartilhados). Em outras palavras, qualquer um pode acessar qualquer ponto do código a qualquer momento, e não é possível, em termos de programação, implementar uma regra que diga o contrário.

- Manutenção: tipos de dados compostos e funções ficam separados, tornando assim difícil manter um e outro.

O paradigma de orientação a objetos, mesmo que não seja perfeito, oferece algumas soluções para isso. A programação orientada a objetos (doravante, POO) é um paradigma de programação que organiza o código em objetos - unidades que combinam dados e comportamentos relacionados em uma única estrutura coesa. Em essência, a POO transforma programas de uma coleção de funções processando dados soltos para um sistema de objetos colaborativos, onde cada um é responsável por seus próprios dados e comportamentos, tornando o código mais organizado, reutilizável e escalável.

### Os quatro pilares

A POO é definida em quatro pilares:

1. **Abstração**: é possível definir unidades de código abstratas nos objetos. Ou seja, não é necessário conhecer a fundo a implementação subjacente de um objeto para utilizá-lo. Isto os torna mais reutilizáveis e facilita a sua manutenção.
2. **Encapsulamento**: é possível definir variáveis e até funções que são completamente isoladas do escopo global. Isto torna as capacidades dos nossos objetos mais restritas e direcionadas.
3. **Herança**: é possível definmir tipos que são subtipos de outros objetos, reaproveitando boa parte da implementação já realizada.
4. **Polimorfismo**: ao mesmo tempo que é possível reaproveitar o código já implementado, podemos redefinir sua implementação, modificando-a.

> Neste tutorial, falaremos sobre o pilar da Abstração.

### O conceito de objeto

Um objeto é uma unidade de programação que define em si atributos e funções, e interage com outros objetos. A definição de um objeto é chamada de **classe**, e uma variável de um determinado objeto é chamada de **instância**.

Vamos instanciar um objeto do tipo `Carro`: um carro possui uma marca, modelo e ano de fabricação - estes seriam seus **atributos**. Algumas funcionalidades de um carro seriam ligar, desligar, acelerar e freiar. Dados estes **comportamentos**, podemos definir um atributo booleano que diz se o carro está ou não ligado, e um atributo inteiro para representar sua velocidade.

```python
class Car:
    def __init__(self, brand, model,  year): # construtor
        self.brand = brand # marca
        self.model = model # modelo
        self.year = year # ano de fabricação

        self.is_started = False # ligado
        self.speed = 0 # velocidade

    def start(self): # ligar
        if not self.is_started:
            print('Ligando carro')
            self.is_started = True

    def turn_off(self): # desligar
        if self.is_started and self.speed = 0:
            print('Desligando carro')

    def accelerate(self): # acelerar
        print('Acelerando')
        if self.is_started:
            self.speed += 10

    def brake(self): # freiar
        if self.speed > 0:
            print('Freiando')
            self.speed -= 10

car = Car('Fiat', 'Uno', 1996) # chamando o construtor
car.start() # Dar partida
car.accelerate() # Acelerar
car.brake() # Freiar
car.turn_off() # Desligar
```

Muita informação de uma única vez, certo? Então, vamos com calma. O que definimos aqui é uma unidade de programação que contém variáveis e funções vinculadas a si, ou seja, um **objeto**. Temos a função `__init__`, o nosso **construtor**, que recebe alguns parâmetros como qualquer função. O primeiro deles é o parâmetro `self`, isto é, o argumento da própria instância que está chamando o construtor. Como atributos desta instância, serão colocados as variáveis da chamada do construtor (ex.: `self.brand = brand`), além de outras duas que não estão no construtor (`is_started` e `speed`). Daí, criamos nossos **métodos**, isto é, as funções vinculadas ao objeto, que são os seus **comportamentos**, manipulando os atributos do próprio objeto.

Daqui para a frente, veremos cada vez mais como criar e manipular objetos em Python. Este conhecimento será de fundamental importância para dominarmos conceitos e técnicas mais avançadas de programação. Bons estudos!