# Regex - Um resumo simples

> Um pequeno tutorial ou resumo sobre criação e funcionalidades de Expressões Regulares.

---

## Esse repositório ainda é um WIP (Work in Progress) por isso aguarde mais atualizações

---

## Lista de conteúdo

<details><summary><h3>

:star: Básico

</h3></summary>

* [**O que são?**](#o-que-diabos-são-expressões-regulares)
* [**Tipo unitário**](#tipo-unitário)
  * [Qualquer caractere ( **```.```** )](#ponto)
  * [Caractere ( **```a```** )](#caractere)
  * [Lista ( **```[...]```** )](#lista)
* [**Quantificadores**](#quantificadores)
  * [Qualquer quantidade ( **```*```** )](#asterisco)
  * [Opcional ( **```?```** )](#opcional)
  * [Requerido ( **```+```** )](#requerido)
  * [Chaves ( **```{n,m}```** )](#chaves)
* [**Delimitadores**](#delimitadores)
  * [Grupo ( **```(...)```** )](#grupo)
  * [Início ( **```^```** )](#início)
  * [Fim ( **```$```** )](#fim)
  * [Borda ( **```\b```** )](#borda)
* [**Especiais**](#especiais)
  * [Escape ( **```\```** )](#escape)
  * [Ou ( **```|```** )](#ou)
  * [Classes **POSIX**](#classes-posix)
* [Precedência de metacaracteres](#precedência)

</details>

<details><summary><h3>

:skull: Avançado

</h3></summary>

* [**Gulodice**](#gulodice)
* [**Referenciadores**](#referenciadores)
  * [Retrovisores ( **```\1 , \2 , \3 ...```** )](#retrovisores)
* [**Quantificadores não-gulosos**](#quantificadores-não-gulosos)
  * [Asterisco ( **```*?```** )](#asterisco-não-guloso)
  * [Opcional ( **```??```** )](#opcional-não-guloso)
  * [Requerido ( **```+?```** )](#requerido-não-guloso)
  * [Chaves ( **```{n,m}?```** )](#chaves-não-gulosas)
* [**Barra-letras**](#barra-letras)
* [**Modificadores Especiais**](#modificadores-especiais)
  * [Comentário ( **```(#comentário)```** )](#comentário)
  * [Lookups](#lookups)
  * [Grupo excluído ( **```(?:)```** )](#grupo-excluído)
  * [Grupo nomeado ( **```(?<nome>)```** )](#grupo-nomeado)
  * [Grupo modificador ( **```(?)```** )](#grupo-modificador)
  * [If-then-else ( **(?(condição)ER-sim|ER-não)** )](#if-then-else)
  * [Código ( **(?{código})** )](#código)

</details>

<details><summary><h3>

:bar_chart: Tabelas

</h3></summary>

* [Classes **POSIX**](#tabela-das-classes-posix)
* [**Barra-letras**](#tabela-de-barra-letras)

</details>

### :book: [Referência](#📖-referência)


## :star: Básico

### O QUE DIABOS SÃO EXPRESSÕES REGULARES?

Expressões regulares, também conhecidas como **ER's**, **regex**, **regexes** e entre outras, é uma ferramenta muito poderosa utilizada para **"casar"** com uma determinada sequência de caracteres.

Casar é algo como combinar e verificar caso o texto dado siga o padrão descrito pela ER.

É muito usada para a verificação e procura de padrões específicos em textos digitais e dados do tipo string.

Pode parecer algo intimidador por conta da má legibilidade, porém, ao analisar cada componente individualmente, vê-se que não é um "bicho de sete cabeças" como muitos pensam.

Para facilitar o seu aprendizado, aqui você verá uma breve descrição e exemplos dos tipos de metacaracteres utilizados para a formação dessas ER's.

---

### Tipo unitário - 

Os metacaracteres unitários são metacaracteres cujo casam somente com um caractere, um único valor da tabela ASCII.

#### Ponto

O ponto ( **```.```** ) casa com um único caractere qualquer, sem específicidade, casando com qualquer caractere da tabela ASCII.

> Exemplo:
>  ```...``` casa com "aaa","abb", "uhf" ou "(1@"

---
 
#### Caractere

Um caractere específico em uma Expressão Regular é o mesmo que casar um único caractere com aquele valor ASCII.

> Exemplo:
> ```a``` casa somente com "a" e ```olá``` casa somente com "olá"

---

#### Lista

A lista ( **```[]```** ) casa um único caractere cujo é pertencente à essa lista. Pode-se usar de intervalos que seguem a ordem numérica da tabela ASCII, como ```[A-z]```, cujo também casa com os caracteres **"[\\]^_`"**, recomendando-se usar [Classes POSIX](#classes-posix).

> Exemplo:
> ```[a-z]``` casa qualquer caractere de "a" até "z".
> ```[0123]``` casa um caractere caso ele seja "0", "1", "2" ou "3".

**Lista negada**

A lista negada ( **```[^]```** ) é quase o mesmo que a lista, porém ela casa qualquer caractere exceto os que a pertencem.

> Exemplo:
> ```[^1234abcd]``` casa quaisquer caracteres que não sejam "1", "2", "3", "4", "a", "b", "c" ou "d".

**Normalidade**

Todo caractere inserido dentro de uma lista é um caractere comum, inclusive os metacaracteres como ```.```, ```*``` entre outros, com exceção dos caracteres ```-```, ```]``` e ```[``` que devem ser inseridos no começo da lista ou no final da lista.

> Exemplo:
> ```[*{}.]``` casa com os caracteres "*", "{", "}" e ".".
> ```[][-]``` é uma lista cujo casa com os caracteres "]", "[" e "-".

---

### Quantificadores -

Os quantificadores são metacaracteres cujo quantificam a quantidade que um [grupo](#grupo) ou metacaractere unitário para aumentar a quantidade de "casamentos" que fazem.

#### Asterisco

O asterisco ( **```*```** ) casa com qualquer quantidade de caracteres, ou seja, para ele não importa se não há o caractere, se há um ou se há mais caracteres.

>Exemplo:
> ```a*``` casa com "", "a", "aa" e assim por diante...
> O curinga das ER's ```.*``` casa com qualquer caractere em qualquer quantidade, inclusive strings vazias como "".

---

#### Opcional

---

#### Requerido

---

#### Chaves

---

### Delimitadores -

#### Grupo

---

#### Início

---

#### Fim

---

#### Borda

---

### Especiais -

#### Escape

---

#### Ou

---

#### Classes POSIX

---

### Precedência -

---

## :skull: Avançado

### Gulodice -

---

### Referenciadores -

#### Retrovisores

---

### Quantificadores não-gulosos -

#### Asterisco não-guloso

---

#### Opcional não-guloso

---

#### Requerido não-guloso

---

#### Chaves não-gulosas

---

### Barra-letras -

---

### Modificadores Especiais -

#### Comentário

---

#### Lookups

---

#### Grupo Excluído

---

#### Grupo Nomeado

---

#### Grupo modificador

---

#### If-then-else

---

#### Código

---

## :bar_chart: Tabelas

### Tabela das Classes POSIX 

---

### Tabela de Barra-letras

---

# :book: Referência

Esse artigo foi inspirado e feito com a ajuda do livro "Expressões Regulares - Uma Abordagem Divertida - 2ª Edição" escrito por Aurélio Marinho Jargas pela editora Novatec.