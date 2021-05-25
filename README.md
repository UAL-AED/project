<!-- <style type="text/css" rel="stylesheet">
    h1, h2, h3 { font-weight: bold; }
    .warning { color: red; font-weight: bold; margin-bottom: 10px;}
</style> -->

# [Algoritmos e Estruturas de Dados 2020 2021](https://elearning.ual.pt/course/view.php?id=1787) - [UAL](https://autonoma.pt/) <!-- omit in toc -->

## Projeto <!-- omit in toc -->

- [Datas Relevantes](#datas-relevantes)
- [Descrição](#descrição)
- [Instruções](#instruções)
  - [Definir data atual (DD)](#definir-data-atual-dd)
  - [Registar cliente (RC)](#registar-cliente-rc)
  - [Registar família (RP)](#registar-família-rp)
  - [Registar série (RS)](#registar-série-rs)
  - [Registar episódio (RE)](#registar-episódio-re)
  - [Alterar Plano (AP)](#alterar-plano-ap)
  - [Cancelar plano (CP)](#cancelar-plano-cp)
  - [Associar cliente a família (AF)](#associar-cliente-a-família-af)
  - [Desassociar cliente de família (DF)](#desassociar-cliente-de-família-df)
  - [Eliminar série, temporada, ou episódio (ES)](#eliminar-série-temporada-ou-episódio-es)
  - [Eliminar cliente (EC)](#eliminar-cliente-ec)
  - [Listar clientes (LP)](#listar-clientes-lp)
  - [Listar famílias (LF)](#listar-famílias-lf)
  - [Listar séries (LS)](#listar-séries-ls)
  - [Listar séries alugadas (LSA)](#listar-séries-alugadas-lsa)
  - [Listar séries alugadas por família (LSAF)](#listar-séries-alugadas-por-família-lsaf)
  - [Alugar série (AS)](#alugar-série-as)
  - [Cancelar aluguer (CA)](#cancelar-aluguer-ca)
- [Estrutura do projeto e repositório git](#estrutura-do-projeto-e-repositório-git)
- [Testes de *input*/*ouput*](#testes-de-inputouput)
- [Entrega](#entrega)
- [Prova de Autoria](#prova-de-autoria)
- [Avaliação](#avaliação)

## Datas Relevantes
| Data                      | Evento                               |
| ------------------------- | ------------------------------------ |
| 15/05/2021                | Disponibilização do enunciado.       |
| 30/05/2021                | Disponibilização de testes públicos. |
| 27/06/2021 23:59:59 GMT   | Entrega final do trabalho.           |
| 28/06/2021 --- 06/07/2021 | Provas de autoria.                   |

## Descrição

Considere uma uma loja online para aluguer de séries.

A loja oferece os seus serviços a clientes. Cada cliente pode adquirir um plano individual, ou familiar (ver a [Tabela 1](#tab-plans)). 

Cada cliente tem um estado atribuído, que deve corresponder ao plano de subscrição de serviço. Estes estados são: *Standard*, *Premium*, *Pack* família, ou *Cancelado*.

Ao pertencer a um *Pack* família, o plano de cliente passar a ter as caraterísticas do *Pack*. Cada *Pack* família tem até 4 clientes.

Quando um cliente cancela a sua subscrição, passa ao estado *Cancelado*.

O aluguer é feito por episódio, ou por temporada de série. O tempo do aluguer começa a contar da data atual do sistema, e varia de acordo com o plano de subscrição. Terminado o tempo, os episódios são retirados da lista de conteúdo alugado pelo cliente. A [Tabela 1](#tab-plans) apresenta as várias hipóteses.

<div id="tab-plans">Tabela 1: Tempos de aluguer por plano de subscrição.</div>

| Ordem | Plano       | Tempo máximo de aluguer |
| :---- | :---------- | ----------------------: |
| 1     | *Standard*  |                  4 dias |
| 2     | *Premium*   |                  7 dias |
| 3     | *Pack*      |                  4 dias |
| 4     | *Cancelado* |                  0 dias |

O sistema da loja funciona com uma data atual de referência. Quando a loja é inicializada, essa data está indefinida, e maioria das operações relacionadas com alugueres não é permitida (exceção para `DD`, e `L`).

## Instruções
Na descrição das várias instruções é indicada a sua sintaxe. Os argumentos são separados por espaços em branco, e cada linha é terminada por um caráter fim de linha.

Para cada instrução é indicada a lista de expressões de saída, quer para execuções com sucesso, quer para insucesso.

No caso de insucesso só deve surgir uma mensagem de erro. Verificando-se várias situações de insucesso em simultâneo, deve surgir apenas a mensagem do primeiro cenário, de acordo com a ordem de saídas de insucesso descritas para cada instrução.

Caso o utilizador introduza uma instrução inválida, ou seja, não prevista na lista de instruções desta secção, ou um número de parâmetros errado para uma instrução existente, o programa deve escrever:

    Instrução inválida.

Pode assumir que não existem erros de representação de informação (e.g., texto em vez de valores numéricos).

A descrição de cada instrução pretende ser exaustiva, e sem ambiguidades. Não deve ser possível optar entre vários comportamentos possíveis na mesma situação. Se essa situação ocorrer deve entrar em contacto com equipa docente.

A implementação não deve suportar mais instruções do que as que estão descritas.

### Definir data atual (DD)

Altera a data atual da aplicação para a data indicada.  A data indicada não pode ser anterior à data atualmente em vigor (se existir). A atualização de datas implica a atualização dos registo de aluguer.

O formato da data indicada deve ser *AAAAMMDD* (4 algarismo para o ano, 2 para o mês, e 2 para o dia).

Entrada:

    DD AAAAMMDD

Saída com sucesso:

    Data alterada.

Saída com insucesso:

- Quando a data indicada é anterior à data atual:

      Data indicada é anterior à data atual.

### Registar cliente (RC)

Regista um novo cliente. Cada cliente é composto por um identificador (atribuído automaticamente), nome, e tipo de plano (*Standard* e *Premium*). O nome é único no universo de clientes. É possível registar um cliente pré-existente apenas se o seu plano atual for *Cancelado*, passando a assumir o novo plano indicado.

`Nome` é o nome do cliente, e `Plano` é o plano de subscrição (ver [Tabela 1](#tab-plans)). `IdentificadorSérie` é o identificador único do cliente, gerado automaticamente.

Entrada:

    RC Nome Plano

Saída com sucesso:

    Cliente registado com identificador IdentificadorCliente.

Saída com insucesso:

- Quando não existe data definida:

      Sem data definida.

- Quando já existe um cliente (sem estar no estado *Cancelado*) com o nome indicado:

      Cliente existente.

- Quando não existe um plano de subscrição com o nome indicado:

      Plano inexistente.

### Registar família (RP)

Regista um novo *pack* família. O nome deve ser único no universo de famílias. Não existe limite para o número de famílias.

`NomeFamília` é o nome único da família, e pode conter espaços. `IdentificadorFamília` é o identificador único da família, gerado automaticamente.

Entrada:

    RP NomeFamília

Saída com sucesso:

Saída com insucesso:

- Quando não existe data definida:

      Sem data definida.

- Quando o nome indicado já se encontra registado:

      Família existente.

### Registar série (RS)

Regista uma nova série.

`NomeSérie` é o nome único da série, e pode conter espaços. `IdentificadorSérie` é o identificador único da série, gerado automaticamente.

Entrada:

    RS NomeSérie

Saída com sucesso:

    Série registada com o identificador IdentificadorSérie

Saída com insucesso:

- Quando o nome indicado já se encontra registado:

      Série existente.

### Registar episódio (RE)

Regista um episódio de uma temporada de uma série.

`IdentificadorSérie` é o identificador da série, `NúmeroTemporada` é o número da temporada, `NúmeroEpisódio` é o número de ordem do episódio na temporada, e `NomeEpisódio` é nome do episódio. O par `NúmeroTemporada` e `NúmeroEpisódio` é único em cada série. `NomeEpisódio` pode conter espaços.

Entrada:

    RE IdentificadorSérie NúmeroTemporada NúmeroEpisódio NomeEpisódio

Saída com sucesso:

    Registo efetuado com sucesso.

Saída com insucesso:

- Quando a série não existe:

      Série inexistente.

- Quando o episódio já existe:

      Episódio existente.

### Alterar Plano (AP)

Altera o plano associado ao cliente individual, para *Standard* ou *Premium*.

`IdentificadorCliente` é o identificador do cliente, e `Plano` o nome do plano de subscrição de serviço.

O conteúdo alugado pelo cliente passa a estar sujeito às caraterísticas do novo plano. Pode ser necessário terminar alugueres ativos.


Entrada:

    AP NúmeroCliente Plano

Saída com sucesso:

    Plano alterado com sucesso.

Saída com insucesso:

- Quando o cliente não existe:

      Cliente inexistente.

- Quando o cliente pertence a uma família:

      Cliente associado a família.

### Cancelar plano (CP)

Cancela o plano de um cliente individual. O plano de cliente passa para a *Cancelado*. Se o cliente pertencer a uma família, a operação é equivalente a [DF](#desassociar-cliente-de-família-df).

`IdentificadorCliente` é o identificador do cliente.

Entrada:

    CP IdentificadorCliente

Saída com sucesso:

    Plano cancelado com sucesso.

Saída com insucesso:

- Quando o cliente não existe:

      Cliente inexistente.

### Associar cliente a família (AF)

Associa um cliente a uma família. O cliente tem que estar previamente registado. Cada cliente só pode pertencer a uma família.

`IdentificadorFamília` é o identificador da família, e  `IdentificadorCliente` é o identificador do cliente.

Entrada:

    AF IdentificadorFamília IdentificadorCliente

Saída com sucesso:

    Cliente associado com sucesso.

Saída com insucesso:

- Quando a família não existe:

      Família inexistente.

- Quando o cliente não existe:

      Cliente inexistente.

- Quando o cliente já está associado a uma família:

      Cliente associado a outra família.

### Desassociar cliente de família (DF)

Elimina a associação entre cliente e família. O cliente passa para o plano *Cancelado*.

`IdentificadorCliente` é o identificador do cliente.

Entrada:

    DF IdentificadorCliente

Saída com sucesso:

    Cliente desassociado com sucesso.

Saída com insucesso:

- Quando o cliente não existe:

      Cliente inexistente.

- Quando o cliente não está associado a qualquer família:

      Cliente não associado a família.

### Eliminar série, temporada, ou episódio (ES)

Elimina série, temporada, ou episódio de temporada.

`IdentificadorSérie` é o identificador da série. `NúmeroTemporada` (opcional) é o número da temporada, e `NúmeroEpisódio` é o número do episódio (opcional).

Se não for indicado um identificador de temporada, toda a série é eliminada. Se não for indicado um identificador de episódio, toda a temporada é eliminada.

O conteúdo eliminado deixa de estar disponível para alugar, e todos os alugueres atuais desse conteúdo são também eliminados.

Entrada:

    ES IdentificadorSérie NúmeroTemporada NúmeroEpisódio

Saída com sucesso:

    Conteúdo eliminado com sucesso.

Saída com insucesso:

- Quando a série não existe:

      Série inexistente.

- Quando a temporada não existe:

      Temporada inexistente.

- Quando o episódio não existe:

      Episódio inexistente.

### Eliminar cliente (EC)

Elimina um cliente, de acordo com o respetivo identificador. O registo do cliente é eliminado, assim como eventuais associações a famílias e registos de aluguer.

`IdenticadorCliente` é o identificador do cliente.

Entrada:

    EC IdenticadorCliente

Saída com sucesso:

    Cliente eliminado com sucesso.

Saída com insucesso:

- Quando o cliente não existe:

      Cliente inexistente.

### Listar clientes (LP)

Lista todos os clientes com plano individual por ordem de tipo de plano (ver coluna *ordem* da [Tabela 1](#tab-plans)), e por ordem alfabética de nome dentro de cada plano.

Entrada:

    LP

Saída com sucesso:

```text
NomePlano NomeCliente
NomePlano NomeCliente
...

```

Saída com insucesso:

- Quando não existem clientes registados:

      Sem clientes registados.

### Listar famílias (LF)

Lista todas as famílias por ordem alfabética. Por cada família, lista todos os clientes da família por ordem alfabética de nome.

`NomeFamília` é o nome de uma família, e `NomeCliente` é o nome de um cliente.

Entrada:

    LF

Saída com sucesso:

```text
NomeFamília NomeCliente
NomeFamília NomeCliente
...
```

Saída com insucesso:

- Quando não existem famílias registadas:

      Sem famílias registadas.

### Listar séries (LS)

Lista todas as séries registadas na loja, por ordem de número de episódios alugados. Em caso de empate, lista por ordem alfabética de nome da série.

Entrada:

    LS

Saída com sucesso (termina com uma linha vazia):

```text
NomeSérie
NomeSérie
...

```

Saída com insucesso:

- Quando não existem séries registadas:

      Sem séries registadas.

### Listar séries alugadas (LSA)

Lista todos os episódios alugados pelo cliente, por ordem alfabética de nome da série. Dentro mesma série, lista por ordem de número de temporada, e por ordem de número de episódio dentro de cada temporada.

`IdenticadorCliente` é o identificador do cliente. `NomeSérie` é o nome da série, `NúmeroTemporada` é o número da temporada, `NúmeroEpisódio` é o número do episódio, e `NomeEpisódio` é o nome do episódio.

Entrada:

    LSA IdentificadorCliente

Saída com sucesso:

    NomeSérie [NúmeroTemporada/NúmeroEpisódio] NomeEpisódio
    NomeSérie [NúmeroTemporada/NúmeroEpisódio] NomeEpisódio
    ...

Saída com insucesso:

- Quando não existe data definida.

      Sem data definida.

- Quando o cliente não existe:

      Cliente inexistente.

- Quando o cliente não tem episódios alugados:

      Sem episódios alugados.

### Listar séries alugadas por família (LSAF)

Lista todas as séries alugadas por todos os elementos da família, ordenadas por ordem alfabética de nome da série.

`IdentificadorFamília` é o identificador da família. `NomeSérie` é o nome de uma série.

Entrada:

    LSAF IdentificadorFamília

Saída com sucesso:

    NomeSérie
    NomeSérie
    ...

Saída com insucesso:

- Quando não existe data definida.

      Sem data definida.

- Quando a família não existe:

      Família inexistente.

### Alugar série (AS)

Regista o aluguer de episódio(s) de uma série.

Deve ser indicado o nome do cliente seguido do nome da série e indicação da temporada e respetivo número do episódio. Se nenhum número de episódio for indicado, o cliente aluga todos os episódios da temporada indicada.

`IdentificadorCliente` é o identificador do cliente, `IdentificadorSérie` é o identificador da série, e `NúmeroTemporada` é o número da temporada. `NúmeroEpisódio` (opcional) é o número do episódio a subscrever.

Entrada:

    AS IdentificadorCliente IdentificadorSérie NúmeroTemporada NúmeroEpisódio

Saída com sucesso:

    Conteúdo alugado com sucesso.

Saída com insucesso:

- Quando não existe data definida.

      Sem data definida.

- Quando o cliente não existe:

      Cliente inexistente.

- Quando a série não existe:

      Série inexistente.

- Quando a temporada não existe:

      Temporada inexistente.

- Quando o episódio não existe:

      Episódio inexistente.

### Cancelar aluguer (CA)

Cancela o aluguer de um episódio, temporada, ou série.

`IdentificadorCliente` é o identificador do cliente, e `IdentificadorSérie` é o identificador da série. `NúmeroTemporada` (opcional) é o número da temporada a cancelar, e `NúmeroEpisódio` (opcional) é o número do episódio a cancelar.

Se não for indicado o identificador de episódio, o aluguer de todos os episódios da temporada é cancelado. Se não for indicado o número da temporada, o aluguer de todos os episódios da série é cancelado.

Entrada:

    CA IdentificadorCliente IdentificadorSérie NúmeroTemporada NúmeroEpisódio

Saída com sucesso:

    Aluguer de conteúdo cancelado com sucesso.

Saída com insucesso:

- Quando o cliente não existe:

      Cliente inexistente.

- Quando nenhum episódio da série está alugado pelo cliente:

      Série sem aluguer registado.

- Quando nenhum episódio da temporada está alugado pelo cliente:

      Temporada sem aluguer registado.

- Quando o episódio não está alugado pelo cliente:

      Episódio sem aluguer registado.

## Estrutura do projeto e repositório git
A estrutura to projeto está proposta pelo repositório distribuído pelo Github Classroom:

      projeto
      |-- aed_ds : pacote de estruturas de dados
      |-- controllers : controladores da aplicação
      |-- models : modelos de dados da aplicação
      |-- views : interação com a aplicação
      |-- iotests : testes de output, a distribuir pela docência
      |-- tests : testes unitários, opcionais
      |-- program.py : ponto de entrada do programa
      |-- README.md : este ficheiro
      |-- REPORT.md : relatório do projeto

O repositório de referência está disponível em <https://github.com/UAL-AED/project>

Para efetuar a atualizações:

1. Registar o repositório como `upstream` (só deve acontecer uma vez)

        git remote add upstream http://github.com/UAL-AED/project

2. Atualizar o `upstream` (sempre que existirem

        git fetch upstream

3. Obter as alterações (e.g., ficheiro `README.md`)

        git checkout upstream/main README.md

<!-- ### (2021/05/30) Atualização com testes de output -->

## Testes de *input*/*ouput*
O projeto é validado através de um conjunto de baterias de teste de *input*/*ouput*.

Cada bateria é constituída por um ficheiro de entrada e outro e saída. O ficheiro de entrada contém uma sequência de instruções a passar pelo programa que, por sua vez, deve produzir uma sequência de saída exatamente igual ao ficheiro de saída. A comparação será feita *byte* a *byte*, pelo que não podem existir quaisquer diferenças para o programa ser considerado válido.

Os grupos de trabalho devem utilizar as baterias públicas para validar o desenvolvimento do projeto.

As baterias serão distribuídas através do repositório git de referência, na diretoria `iotests` (será necessário registar o repositório de referência como `upstream`, de acordo com as instruções na secção anterior.).

## Entrega

A entrega do projeto é feita no *GitHub Classroom* e na plataforma de *e-learning*.

A entrega no *e-learning* corresponde a um ficheiro `zip` do repositório *GitHub Classroom*.

Deve existir, na raiz do repositório:

- Um ficheiro chamado `program.py`, que será executado com as instruções dos testes;
- Um ficheiro de relatório `REPORT.md` com a identificação dos elementos do grupo de trabalho, e eventuais comentários relativos a estratégias de implementação adotadas, e/ou à distribuição de tarefas.

O código fonte entregue será sujeito a validação com um conjunto de testes reservado para esse efeito.

A ausência de identificação individual no ficheiro de relatório implica a anulação da participação individual no projeto.

## Prova de Autoria

Todos os projetos entregues serão sujeitos a prova de autoria. Para esse efeito, cada grupo terá que efetuar uma discussão com a docência, de forma a demonstrar que o código entregue foi de facto feito pelo grupo, e que a distribuição de trabalho foi equilibrada.

O calendário das provas de autoria será disponibilizado no *e-learning*, após o prazo de entrega da implementação do projeto.

A não comparência na prova de autoria implica a anulação da participação individual no projeto.

## Avaliação

O projeto é avaliado com base em duas componentes: quantitativa (*A*), e qualitativa (*B*). A nota final do projeto é determinada por *(0.5 x A) + (0.5 x B)*.

| Instrução | Peso      |
| --------- | --------- |
| DD        | 2 valores |
| RC        | 1 valor   |
| RP        | 1 valor   |
| RS        | 1 valor   |
| RE        | 1 valor   |
| AP        | 2 valores |
| CP        | 1 valor   |
| AF        | 1 valor   |
| DF        | 1 valor   |
| ES        | 1 valor   |
| EC        | 1 valor   |
| LP        | 1 valor   |
| LF        | 1 valor   |
| LS        | 1 valor   |
| LSA       | 1 valor   |
| LSAF      | 1 valor   |
| AS        | 1 valor   |
| CA        | 1 valor   |

A avaliação qualitativa irá considerar que existem várias formas de resolver o problema descrito, mas que se exige a utilização dos instrumentos e métodos apresentados na unidade curricular de Algoritmos e Estruturas de Dados, nomeadamente:

- Separação entre interface, dados, e lógica da aplicação
- Justificação clara para as variáveis e operações implementadas
- Organização da solução coerente com a metodologia apresentada na disciplina
- Adequação da escolha de estruturas de dados e algoritmos para a resolução do problema
- Utilização dos tipos abstratos de dados (TAD) apresentados pela unidade curricular
  - A implementação dos TAD decorre ao longo do semestre através da realização dos laboratórios
  - Na implementação de TAD é possível criar métodos para utilização interna (i.e., apenas dentro da classe), que não correspondem a métodos de TAD, no entanto a utilização desses objetos não deve recorrer a métodos que não constem dos respetivos TAD, e.g., a *utilização* de objetos `SinglyLinkedList` só deve recorrer a métodos descritos pela TAD `List`
  - O projeto deve funcionar sem alterações caso a implementação das TAD seja alterada pelos docentes

A implementação estrita de todas as instruções descritas neste enunciado assegura, sem prejuízo de reprovação por irregularidade académica, a nota mínima de 10 valores.

A utilização de estruturas de dados não autorizadas (i.e., listas, tuplos, conjuntos, e dicionários Python), ou a utilização de módulos externos não implementados pelo grupo de trabalho, determina uma nota máxima de 12 valores no projeto.

Caso ocorram dúvidas sobre a autorização de determinada estrutura ou módulo, os docentes devem ser contactados para determinar a autorização de utilização.

As notas finais do projeto serão disponibilizadas no *e-learning*.
