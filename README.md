# Regex - Um resumo simples

> Um pequeno tutorial ou resumo sobre criação e funcionalidades de Expressões Regulares.

---

## Esse repositório ainda é um WIP (Work in Progress) por isso aguarde mais atualizações

---

## Lista de conteúdo

<details><summary><h4>

:star: Básico
</h4></summary>

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
<details><summary><h4>

:skull: Avançado
</h4></summary>

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
<details><summary><h4>

:bar_chart: Tabelas
</h4></summary>

* [Classes **POSIX**](#tabela-das-classes-posix)
* [**Barra-letras**](#tabela-de-barra-letras)
</details>

#### :book: [Referência](#📖-referência)


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
>
> ```[0123]``` casa um caractere caso ele seja "0", "1", "2" ou "3".

**Lista negada**

A lista negada ( **```[^]```** ) é quase o mesmo que a lista, porém ela casa qualquer caractere exceto os que a pertencem.

> Exemplo:
> ```[^1234abcd]``` casa quaisquer caracteres que não sejam "1", "2", "3", "4", "a", "b", "c" ou "d".

**Normalidade**

Todo caractere inserido dentro de uma lista é um caractere comum, inclusive os metacaracteres como ```.```, ```*``` entre outros, com exceção dos caracteres ```-```, ```]``` e ```[``` que devem ser inseridos no começo da lista ou no final da lista.

> Exemplo:
> ```[*{}.]``` casa com os caracteres "*", "{", "}" e ".".
>
> ```[][-]``` é uma lista cujo casa com os caracteres "]", "[" e "-".

---

### Quantificadores -

Os quantificadores são metacaracteres cujo quantificam a quantidade que um [grupo](#grupo) ou metacaractere unitário para aumentar a quantidade de "casamentos" que fazem.

#### Asterisco

O asterisco ( **```*```** ) casa com qualquer quantidade de caracteres, ou seja, para ele não importa se não há o caractere, se há um ou se há mais caracteres.

> Exemplo:
> ```a*``` casa com "", "a", "aa" e assim por diante...
>
> O curinga das ER's ```.*``` casa com qualquer caractere em qualquer quantidade, inclusive strings vazias como "".

---

#### Opcional

O metacaractere opcional ( **```?```** ) casa com nenhum ou um do caractere quantificado, ou seja, o caractere se torna opcional.

> Exemplo:
> ```casas?``` casa com "casa" e com "casas" pois o "s" se torna opcional.
>
> ```casa[srlm]?``` casa com "casa", "casas", "casar", "casal" e "casam".

---

#### Requerido

O requerido ( **```+```** ) faz com que o caractere a ser quantificado seja obrigatório, casando com um ou mais desse caractere.

> Exemplo: 
> ```[a-z]+``` casa de "a" até "z" obrigatoriamente em qualquer quantidade.
>
> ```domingos+``` casa com "domingos", "domingoss", "domingosss", "domingossss" e assim por diante.

---

#### Chaves

As chaves ( **```{n,m}```** ) são metacaracteres que quantificam na quantidade mínima e máxima, podendo omitir a quantidade máxima.

> Exemplo:
> ```[0-9]{3,9}``` casa com um número de 3 à 9 dígitos de 0 à 9.
>
> A ER ```[0-9]{3}.[0-9]{3}.[0-9]{3}-[0-9]``` casa com o modelo de um CPF, por exemplo : "123.456.789-0"

---

### Delimitadores -

Os metacaracteres delimitadores são metacaracteres que descrevem ou barram limites no interpretador de ER.

#### Grupo

O grupo ( **```(...)```** ) é um tipo especial de metacaractere que delimita a ação de uma ER específica, tornando possível quantificá-la como um único caractere, assim como fazer o uso de [retrovisores](#retrovisores).

> Exemplo:
> ```(joga)``` casa com "joga", mas ```(joga){2}``` casa somente com "jogajoga".
>
> A ER do CPF, agora com o uso de grupos, pode ser reformulada para: ```([0-9]{3}.){2}[0-9]{3}-[0-9]``` porém ainda fica algo muito grotesco.

---

#### Início

Esse delimitador de início ( **```^```** ) é um metacaractere que deve sempre ser colocado no início da ER, simboliza que quer casar a ER somente se ela estiver no começo de  uma linha.

> Exemplo:
> ```^amarelo``` casará com "amarelo" somente se ele estiver no início da linha, por exemplo, não casaria a palavra "amarelo" de "o meu carro é amarelo" e sim com "amarelo é a cor do meu carro".
>
> ```^^``` casa com uma string cujo o início é um acento circunflexo, ou seja, casa com "^".

---

#### Fim

Assim como o metacaractere início, o metacaractere fim ( **```$```** ) é o seu complementar, têm de ser posto no final da ER, simbolizando que somente casará caso a linha termine com essa determinada ER.

> Exemplo:
> ```123$``` casa somente com "123" no final de uma linha.
>
> São usados juntos o ```^``` e o ```$``` para casar uma linha inteira assim: ```^dobrados$``` casa somente com a string completa "dobrados".

---

#### Borda

A borda ( **```\b```** )é um metacaractere delimitador que casa as bordas de uma palavra, os limites.

> Exemplo:
> ```\bs.``` casa com "sao", "s34", "so", entre outros, mas não com "coi**sa**".
>
> Porém, a ER ```s.\b``` não casa com "são" nem com "s34", mas casa com "so" e com "coisa".
>
> Utilizando dois desse metacaractere podemos delimitar à uma palavra:  ```\bmente\b``` casa somente com "mente", mas não com "extremamente" ou "intensamente".

---

### Especiais -

Os metacaracteres do tipo especial são os que não encaixam necessáriamente em nenhum dos grupos anteriores.

#### Escape

O metacaractere escape ( **```\```** ) é o metacaractere cancelador, ele negativa todos os efeitos especiais do metacaractere seguinte, transformando-o em um literal.

> Exemplos:
> ```dois\*litros``` casa somente com "dois*litros", o asterisco se torna literal.
> ```isso\\esse``` casa somente com "isso\esse", veja que há a possibilidade de escapar o escape, caso desejar.

---

#### Ou

O metacaractere ou ( **```|```** ) é um metacaractere que casa com uma opção ou outra.

> Exemplo:
> ```isso|esse``` casa com "isso" ou com "esse".
> ```(super|hiper)?mercado``` casa com "supermercado" ou com "hipermercado" ou com "mercado".

---

#### Classes POSIX

Classes POSIX são uma classe de objetos que representam intervalos, e são regionalizados, ou seja, se está no Brasil, utiliza-se os caracteres do Brasil, se está na Alemanha, utiliza-se os caracteres alemães.

Para mais informações consulte a [Tabela POSIX](#tabela-das-classes-posix).

> Exemplos:
> ```[[:alnum:]]{3}``` casa com 3 caracteres alfanuméricos.
> ```[:digit:]``` casa com um único dígito.

---

### Precedência -

Os metacaracteres possuem uma ordem de precedência

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

| POSIX | Similar | Significa |
| ------| ---- | ----- | 
| [:upper:] | [A-Z] | Letras maiúsculas |
| [:lower:] | [a-z] | Letras minúsculas |
| [:alpha:] | [A-Za-z] | Maiúsculas e minúsculas |
| [:alnum:] | [A-Za-z0-9] | Letras e números |
| [:digit:] | [0-9] | Números |
| [:xdigit:] | [0-9A-Fa-f] | Números hexadecimais |
| [:punct:] | [.,!?:…] | Caracteres de pontuação |
| [:blank:] | [ \t] | Espaço em branco e TAB  |
| [:space:] | [ \t\n\r\f\v] | Caracteres brancos  |
| [:cntrl:] | - | Caracteres de controle |
| [:graph:] | [^ \t\n\r\f\v] | Caracteres imprimíveis |
| [:print:] | [^\t\n\r\f\v] | Imprimíveis e o espaço |

---

### Tabela de Barra-letras

Existem três tipos de Barra-letras:

* Caracteres
* Modificadores
* Intervalo

##### B-L Caracteres

| **b-l** | Nome | Tradução |
| ---- | ---- | ---- |
| \a | Alert | Alerta (bipe) |
| \b | Backspace | Caractere Backspace |
| \e | Escape | Caractere Esc |
| \f | Form feed | Alimentação |
| \n | Newline | Linha Nova |
| \r | Carriage return | Retorno de Carro |
| \t | Htab | Tabulação horizontal |
| \v | Vtab | Tabulação vertical |

##### B-L Modificadores

| **b-l** | Significado | Similar |
| ---- | ---- | ---- |
| \a | Alfabeto | [[:alpha:]] |
| \A | Não Alfabeto | [^\[:alpha:]] |
| \h | Cabeça de palavra | [[:alpha:]_] |
| \H | Não cabeça de palavra | [^\[:alpha:]_] |
| \l | Minúsculas | [[:lower:]] |
| \L | Não minúsculas | [^\[:lower:]] |
| \u | Maiúsculas | [[:upper:]] |
| \U | Não maiúsculas | [^\[:upper:]] |
| \o | Número octal | [0-7] |
| \O | Não número octal | [^0-7] |
| \B | Não borda |  |
| \A | Início |  |
| \Z | Fim |  |
| \l | Torna minúscula |  |
| \L | Torna minúscula até \E |  |
| \u | Torna maiúscula |  |
| \U | Torna maiúscula até \E |  |
| \Q | Escapa até \E |  |
| \E | Fim da modificação |  |
| \G | Fim do casamento anterior |  |

##### B-L Intervalo

| **b-l** | Equivalente POSIX | Significado |
| ---- | ---- | ---- |
| \d | [[:digit:]] | Dígito |
| \D | [^\[:digit:]] | Não-Dígito |
| \w | [[:alnum:]] | Palavra |
| \W | [^\[:alnum:]] | Não-Palavra |
| \s | [[:space:]] | Branco |
| \S | [^\[:space:]] | Não-Branco |

---

# :book: Referência

Esse artigo foi inspirado e feito com a ajuda do livro "Expressões Regulares - Uma Abordagem Divertida - 2ª Edição" escrito por Aurélio Marinho Jargas pela editora Novatec.