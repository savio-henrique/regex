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
  * [B-L Caracteres](#b-l-caracteres)
  * [B-L Modificadores](#b-l-modificadores)
  * [B-L Intervalo](#b-l-intervalo)
</details>

#### :book: [Referência](#📖-referência)


## :star: Básico

### O QUE DIABOS SÃO EXPRESSÕES REGULARES?

Expressões regulares, também conhecidas como **ERs**, **regex**, **regexes** e entre outras, é uma ferramenta muito poderosa utilizada para **"casar"** com uma determinada sequência de caracteres.

Casar é algo como combinar e verificar caso o texto dado siga o padrão descrito pela ER.

É muito usada para a verificação e procura de padrões específicos em textos digitais e dados do tipo string.

Pode parecer algo intimidador por conta da má legibilidade, porém, ao analisar cada componente individualmente, vê-se que não é um "bicho de sete cabeças" como muitos pensam.

Para facilitar o seu aprendizado, aqui você verá uma breve descrição e exemplos dos tipos de metacaracteres utilizados para a formação dessas ERs.

---

### Tipo unitário - 

Os metacaracteres unitários são metacaracteres cujo casam somente com um caractere, um único valor da tabela ASCII.

#### Ponto

O ponto ( **```.```** ) casa com um único caractere qualquer, sem específicidade, casando com qualquer caractere da tabela ASCII.

> Exemplo:
>
>  ```...``` casa com "aaa","abb", "uhf" ou "(1@"

---
 
#### Caractere

Um caractere específico em uma Expressão Regular é o mesmo que casar um único caractere com aquele valor ASCII.

> Exemplo:
>
> ```a``` casa somente com "a" e ```olá``` casa somente com "olá"

---

#### Lista

A lista ( **```[]```** ) casa um único caractere cujo é pertencente à essa lista. Pode-se usar de intervalos que seguem a ordem numérica da tabela ASCII, como ```[A-z]```, cujo também casa com os caracteres **"[\\]^_`"**, recomendando-se usar [Classes POSIX](#classes-posix).

> Exemplo:
>
> ```[a-z]``` casa qualquer caractere de "a" até "z".
>
> ```[0123]``` casa um caractere caso ele seja "0", "1", "2" ou "3".

**Lista negada**

A lista negada ( **```[^]```** ) é quase o mesmo que a lista, porém ela casa qualquer caractere exceto os que a pertencem.

> Exemplo:
>
> ```[^1234abcd]``` casa quaisquer caracteres que não sejam "1", "2", "3", "4", "a", "b", "c" ou "d".

**Normalidade**

Todo caractere inserido dentro de uma lista é um caractere comum, inclusive os metacaracteres como ```.```, ```*``` entre outros, com exceção dos caracteres ```-```, ```]``` e ```[``` que devem ser inseridos no começo da lista ou no final da lista.

> Exemplo:
>
> ```[*{}.]``` casa com os caracteres "*", "{", "}" e ".".
>
> ```[][-]``` é uma lista cujo casa com os caracteres "]", "[" e "-".

---

### Quantificadores -

Os quantificadores são metacaracteres cujo quantificam a quantidade que um [grupo](#grupo) ou metacaractere unitário para aumentar a quantidade de "casamentos" que fazem.

#### Asterisco

O asterisco ( **```*```** ) casa com qualquer quantidade de caracteres, ou seja, para ele não importa se não há o caractere, se há um ou se há mais caracteres.

> Exemplo:
>
> ```a*``` casa com "", "a", "aa" e assim por diante...
>
> O curinga das ERs ```.*``` casa com qualquer caractere em qualquer quantidade, inclusive strings vazias como "".

---

#### Opcional

O metacaractere opcional ( **```?```** ) casa com nenhum ou um do caractere quantificado, ou seja, o caractere se torna opcional.

> Exemplo:
>
> ```casas?``` casa com "casa" e com "casas" pois o "s" se torna opcional.
>
> ```casa[srlm]?``` casa com "casa", "casas", "casar", "casal" e "casam".

---

#### Requerido

O requerido ( **```+```** ) faz com que o caractere a ser quantificado seja obrigatório, casando com um ou mais desse caractere.

> Exemplo:
> 
> ```[a-z]+``` casa de "a" até "z" obrigatoriamente em qualquer quantidade.
>
> ```domingos+``` casa com "domingos", "domingoss", "domingosss", "domingossss" e assim por diante.

---

#### Chaves

As chaves ( **```{n,m}```** ) são metacaracteres que quantificam na quantidade mínima e máxima, podendo omitir a quantidade máxima.

> Exemplo:
>
> ```[0-9]{3,9}``` casa com um número de 3 à 9 dígitos de 0 à 9.
>
> A ER ```[0-9]{3}.[0-9]{3}.[0-9]{3}-[0-9]``` casa com o modelo de um CPF, por exemplo : "123.456.789-0"

---

### Delimitadores -

Os metacaracteres delimitadores são metacaracteres que descrevem ou barram limites no interpretador de ER.

#### Grupo

O grupo ( **```(...)```** ) é um tipo especial de metacaractere que delimita a ação de uma ER específica, tornando possível quantificá-la como um único caractere, assim como fazer o uso de [retrovisores](#retrovisores).

> Exemplo:
>
> ```(joga)``` casa com "joga", mas ```(joga){2}``` casa somente com "jogajoga".
>
> A ER do CPF, agora com o uso de grupos, pode ser reformulada para: ```([0-9]{3}.){2}[0-9]{3}-[0-9]``` porém ainda fica algo muito grotesco.

---

#### Início

Esse delimitador de início ( **```^```** ) é um metacaractere que deve sempre ser colocado no início da ER, simboliza que quer casar a ER somente se ela estiver no começo de  uma linha.

> Exemplo:
>
> ```^amarelo``` casará com "amarelo" somente se ele estiver no início da linha, por exemplo, não casaria a palavra "amarelo" de "o meu carro é amarelo" e sim com "amarelo é a cor do meu carro".
>
> ```^^``` casa com uma string cujo o início é um acento circunflexo, ou seja, casa com "^".

---

#### Fim

Assim como o metacaractere início, o metacaractere fim ( **```$```** ) é o seu complementar, têm de ser posto no final da ER, simbolizando que somente casará caso a linha termine com essa determinada ER.

> Exemplo:
>
> ```123$``` casa somente com "123" no final de uma linha.
>
> São usados juntos o ```^``` e o ```$``` para casar uma linha inteira assim: ```^dobrados$``` casa somente com a string completa "dobrados".

---

#### Borda

A borda ( **```\b```** )é um metacaractere delimitador que casa as bordas de uma palavra, os limites.

> Exemplo:
>
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

> Exemplo:
>
> ```dois\*litros``` casa somente com "dois*litros", o asterisco se torna literal.
>
> ```isso\\esse``` casa somente com "isso\esse", veja que há a possibilidade de escapar o escape, caso desejar.

---

#### Ou

O metacaractere ou ( **```|```** ) é um metacaractere que casa com uma opção ou outra.

> Exemplo:
>
> ```isso|esse``` casa com "isso" ou com "esse".
>
> ```(super|hiper)?mercado``` casa com "supermercado" ou com "hipermercado" ou com "mercado".

---

#### Classes POSIX

Classes POSIX são uma classe de objetos que representam intervalos, e são regionalizados, ou seja, se está no Brasil, utiliza-se os caracteres do Brasil, se está na Alemanha, utiliza-se os caracteres alemães.

Para mais informações consulte a [Tabela POSIX](#tabela-das-classes-posix).

> Exemplo:
>
> ```[[:alnum:]]{3}``` casa com 3 caracteres alfanuméricos.
>
> ```[:digit:]``` casa com um único dígito.

---

### Precedência -

Os metacaracteres possuem uma ordem de precedência, seguindo:

1. Quantificador ( ```g+``` )
2. Concatenação ( ```ab``` )
3. Ou ( ```ab|cd``` )

> Exemplo:
>
> ```abc|bca``` casa "abc" ou "bca", pois a concatenação tem precedência maior, e não casa "abcca" ou "abbca", para casá-los teria-se de usar a ER ```ab(c|b)ca```.
>
> ```ab{3}|ec{3}``` casa com "abbb" ou "eccc", pois o quantificador têm precedência maior que a concatenação e que o ou, e não casaria "ababab" ou "ececec", porém, caso queira casá-los teria que usar a ER ```(ab){3}|(ec){3}```.

---

## :skull: Avançado

### Referenciadores -

Os metacaracteres referenciadores são metacaracteres cujo objetivo é referenciar uma certa parte da expressão, normalmente sendo grupos.

#### Retrovisores

Os retrovisores ( **```\1, \2, \3 ...```** ) são metacaracteres responsáveis por referenciar grupos anteriormente processados pela ER, por isso casam somente com o que já foi previamente processado. Seguindo sua numeração pela ordem de aparição do grupo. 

> Exemplo:
>
> ```(lero)-\1``` casa com "lero-lero".
>
> ```((super|hiper|mini)mercado) é um \2 \1``` casa com "supermercado é um super supermercado" ou trocando os "super" por "hiper" ou "mini". Veja que a ordem cujo os números são utilizados é derivada da ordem em que os grupos foram abertos, ou seja, a ordem em que aparecem os ```(``` .
> Essa ER não casa com "hipermercado é um super supermercado" pois o grupo ```\1``` foi processado com o valor "hipermercado" e o grupo ```\2``` foi processado com o valor "hiper".

---

### Gulodice -

A gulodice é um conceito dos quantificadores que classificam todos eles, diz-se guloso aquele quantificador cujo tenta casar o máximo de caracteres possíveis, por exemplo:

A ER ```[ar]*a``` casaria com qual dessas alternativas na palavra arara?

1. "a"       - nenuma vez a [ar]
2. "ara"     - duas vezes a [ar]
3. "arara"   - quatro vezes a [ar]
4. n.d.a 

Por ser um caractere guloso, ele casaria o máximo de caracteres possíveis, sendo assim, casaria com a alternativa 3.

Esse é um dos motivos pelos quais evitamos o uso dos chamados curingas como ```.*``` pois eles casariam com todos os caracteres independente do resto da ER.

> Exemplo:
>
> ```<.*>``` querendo casar quaisquer tags em uma string, ao tentar com a  string "\<b> uma string \</b>", o ```.*``` acabaria casando com  a parte em negrito: "<***b> uma string </b***>.
>

Para a resolução disso, alguns programas oferecem a utilização de quantificadores não-gulosos, como os abaixo.

---

### Quantificadores não-gulosos -

#### Asterisco não-guloso

O asterisco não-guloso ( **```*?```** ) age como o asterisco porém casando sempre o mínimo possível.

> Exemplo:
>
> Guloso: ```a.*``` casa com "aaaaaa"
>
> Não-Guloso: ```a.*?``` casa com "a"

---

#### Opcional não-guloso

O opcional não-guloso ( **```??```** ) age como o opcional comum porém casando sempre o mínimo possível.

> Exemplo:
>
> Guloso: ```a.?``` casa com "aa"
>
> Não-Guloso: ```a.??``` casa com "a"

---

#### Requerido não-guloso

O requerido não-guloso ( **```+?```** ) age como o requerido comum porém casando sempre o mínimo possível.

> Exemplo:
>
> Guloso: ```a.+``` casa com "aaaaaa"
>
> Não-Guloso: ```a.+?``` casa com "aa"

---

#### Chaves não-gulosas

As chaves não-gulosas ( **```{n,m}?```** ) age como as chaves porém casando sempre o mínimo possível.

> Exemplo:
>
> Guloso: ```a.{1,3}``` casa com "aaaa"
>
> Não-Guloso: ```a.{1,3}?``` casa com "aa"

---

### Barra-letras -

Os barra letras são um tipo especial de metacaracteres, pois, a depender do interprete da ER, eles podem ter diferentes significados e diferentes usos. São identificados por uma barra invertida ```\``` seguida de uma letra qualquer do alfabeto, seja minúscula ou maiúscula.

Para mais informações sobre os barra-letras, consulte a documentação do aplicativo que deseja usar e a [tabela dos barra-letra](#tabela-de-barra-letras).

---

### Modificadores Especiais -

Não bastando tantas funcionalidades para as ERs, quem as usava queria sempre mais e mais funcionalidades, adicionando assim os modificadores especiais, que fazem muito mais do que somente casar certos caracteres.

São geralmente um grupo com uma interrogação dentro seguido de sua funcionalidade ```(?<identificador><conteúdo>)```.

#### Comentário

O comentário ( **```(?#texto)```** ) é como nos comentários de código, não é interpretado pelo interprete da ER, tornando possível se comentar alguma parte da expressão.

> Exemplo:
>
> ```(?#meu nome)Sávio (?#meu sobrenome)Henrique``` casa com "Sávio Henrique".

---

#### Lookups

Lookups são mecanismos que dão uma "espiada" mais a frente ou atrás, e, caso a ER contida neles case, é retornado sucesso. Mais explicações a frente.

Existem 2 tipos de lookups:

* Front lookup
  * !Front Lookup
* Back Lookup
  * !Back Lookup

**Front Lookup**

O Front Lookup ( **```(?=ER)```** ) dá uma "espiada" para a frente, e caso a ER contida case ele casa os termos anteriores.

> Exemplo:
>
> ```Cauda (?=de Dragão)``` só casará "Cauda" caso seja seguida por "de Dragão", porém o termo casado será só "Cauda", não "Cauda de Dragão".

**!Front Lookup**

O !Front Lookup ( **```(?!ER)```** ) assim como o anterior, dá uma "espiada" a frente, porém é o contrário, pois só casa caso esse trecho não siga a ER contida nele.

> Exemplo:
>
> ```Sapo (?!cururu)``` casará somente se "Sapo" não for seguido de "cururu", porém casará "Sapo" se vier seguido de "azul", "verde" entre outros.

**Back Lookup**

Assim como o Front Lookup, o Back Lookup ( **```(?<=ER)```** ) dá uma "espiada" porém para trás do trecho, note o ```<``` apontando para a esquerda.

> Exemplo:
>
> ```(?<=Carlos )Santos Dumont``` casará apenas "Santos Dumont" se for precedido por "Carlos ".

**!Back Lookup**

Igual aos anteriores, o !Back Lookup ( **```(?<!ER)```** ) dá uma "espiada" para trás e casa somente o que trecho caso ele não siga a ER contida.

> Exemplo:
>
> ```(?<!Carlos )Santos Dumont``` casará apenas "Santos Dumont" se não for precedido por "Carlos ".

---

#### Grupo Excluído

O grupo excluído ( **```(?:ER)```** ) funciona igual um grupo comum, porém a sua diferença é que ele não é incluido na contagem de grupos, portanto não se pode referenciar ele por meio de retrovisores, como um grupo fantasma.

> Exemplo:
>
> ```(Jonah) (?:J.) (Jameson)``` casa o nome completo de "Jonah J. Jameson" porém ```\1``` contém "Jonah" e ```\2``` contém "Jameson".

---

#### Grupo Nomeado

O grupo nomeado é um grupo que possui um nome, podendo obter-se o valor casado referenciando pelo nome (a maioria dos aplicativos não possuem suporte a esse tipo de referência).

> Exemplo:
>
> ```(?<nome>Sávio) (?<sobrenome>Henrique)``` casaria "Sávio Henrique".
>
> ```(?<nome>Sávio) (?<sobrenome>Henrique) (?P=sobrenome)```, em alguns lugares, essa ER casaria com "Sávio Henrique Henrique".

---

#### Grupo modificador

O grupo modificador ( **```(?modificador)```** ) configura a ER a partir de um modificador, que é uma letra cujo pode ser:

| Letra | Significado|
|---|---|
| i | Ignorar a diferença entre maiúscula e minúscula|
| m | Trata o texto como multilinha
| s | Trata o texto como uma única linha|
| x | Permite inclusão e espaços e comentários|
| L | Levar em conta a localização do sistema (somente Python) |

> Exemplo:
>
>  ```(?\i)dormiu``` casa com "DORMIU" ou "dormiu" ou "DorMIu", entre outras.

---

#### If-then-else

O if-then-else ( **```(?(condição)ER-sim|ER-não)```** ) , assim como na programação, funciona como um operador ternário, caso a condição seja dada como verdadeira, utilize a ER-sim, caso não, utilize a ER-não. Geralmente essa condição é uma referencia para um grupo prévio.

É raramente suportada por aplicativos, por isso, verifique com a documentação.

> Exemplo:
>
> ```(\+)?(?(1)[0-9]{2} )[0-9]{3} 9[0-9]{8}``` casa com um número de telefone, caso tenha o "+" no começo, deve ser seguido por 2 dígitos, casando "033 912345678" e também "+55 033 912345678". Nesse caso, não utilizei a ER-não.
>
> ```(Sr.)?(?(1) Comandante|Cabo) Sávio``` casa, caso tenha "Sr." no começo, com "Sr. Comandante Sávio", e, caso não o tenha, com "Cabo Sávio". Ou seja, têm de haver "Comandante" ou "Cabo" caso não haja o honorífico.

---

#### Código

Aqui é onde o ponto máximo de perca de compatibilidade de ERs entre aplicativos reside.

O Código ( **```(?{código})```** ) permite-se colocar código de linguagens de programação dentro da própria ER.

O exemplo abaixo é tirado do manual do Perl:

```perl
$_ = 'a' x 8;
m<
  (?{ $cnt = 0})              #inicializa 
  (
    a
      (?{
        local $cnt = $cnt +1; #incrementa
      })
    )*
    aaaa
    (?{ $res = $cnt })        #se ok, copia para uma var não-local
  >x;
```

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

[Site oficial das Expressões Regulares]()