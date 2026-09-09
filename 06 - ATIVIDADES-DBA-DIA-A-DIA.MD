# DATABASES

Por padrão as bases são criadas com MDF e LDF.

.MDF
  - arquivos de dados

.LDF
  - arquivos de log


Existe também o .NDF, mas a criação é opcional. Que são mais arquivos para a base de dados.
Usado pelos arquivos secundários de dados
NDF = Not Master Data File


## Pontos importantes na criação de uma Database

Todos pontos abaixo já vem um padrão do SQL Server, mas não é recomendado manter.

- Localização dos arquivos de dados e log

- Tamanho inicial dos arquivos de dados e log
  - .MDF deve ser estimado por quem projetou a aplicação
  - .LDF de 10% a 25% do tamenho do .MDF é um valor razoável (referência de internet, não é um padrão)

- Tamanho máximo da base: por padrão vem ilimitado
  - Recomendação do professor: se tem várias bases de dados em um disco é difícil controlar isso. Uma boa opção é criar alertas.
  - Se existir uma base de teste que algum desenvolverdor usa, por exemplo, seria recomendado colocar um limite no tamanho máximo da base (max) size.
  - Se a base atingir o tamanho máximo, terá que excluir algum arquivo que não é usado, aumentar espaço em disco, ou se o log estiver no mesmo disco dá pra usar o shirink

- Opção de crescimento da Base
  - MDF cresce rápido e LDF cresce lento
  - File Autogrowth
  - Sugestão(Não é uma regra):

|          MDF Size           | File Autogrowth |
|:---------------------------:|:---------------:|
|           < 1 GB            |  50 MB – 200 MB |
| 1 GB < MDF Size < 100 GB    |  400 MB – 1 GB  |
| 100 GB < MDF Size < 500 GB  |   1 GB – 5 GB   |
|          > 500 GB           |  5 GB – 10 GB   |

|       LDF Size         | File Autogrowth |
|:----------------------:|:---------------:|
|        < 1 GB          |  20 MB – 100 MB |
| 1 GB < LDF Size < 3 GB | 200 MB – 500 MB |
|        > 3 GB          |  500 MB – 1 GB  |


- Recovery Model

# PAGE VERIFY OPTION

Validação de páginas em disco que o SQL Server faz para nos ajudar encontrar algum problemas de inconsistência(corrupção)

- NONE: Não faz nenhuma validação
- TORN_PAGE_DETECTION: Trabalha verificando alguns bits da página de dados do SQL Server
- CHECKSUM: Faz uma validação completa da página de dados (OPÇÃO MAIS IMPORTANTE).

TODA BASE PRECISA TER A OPÇÃO CHECKSUM HABILITADA.

Query para conferir essa opção para todas bases de dados
  - select name, page_verify_option_desc
    from sys.databases

A partir da versão SQL SERVER 2005 já vem habilitado. Importante realizar essa validação


# CRIAÇÃO DE TABELAS

- Tipos de dados
  - Números:
    - Bigint
    - Int
    - Samllint
    - Tinyint
    - Numeric
    - Bit


| Tipo de dados | Intervalo                                                     | Armazenamento |
|:-------------:|:-------------------------------------------------------------:|:-------------:|
|    `bigint`   | −9.223.372.036.854.775.808 até 9.223.372.036.854.775.807      |    8 bytes    |
|     `int`     | −2.147.483.648 até 2.147.483.647                              |    4 bytes    |
|  `smallint`   | −32.768 até 32.767                                            |    2 bytes    |
|   `tinyint`   | 0 até 255                                                     |    1 byte     |


NUMERIC

| **Precisão** | **Bytes de armazenamento** |
|:------------:|:--------------------------:|
|    1 – 9     |          5 bytes           |
|   10 – 19    |          9 bytes           |
|   20 – 28    |          13 bytes          |
|   29 – 38    |          17 bytes          |

  - Data e Hora: Datetime, Date, Time

  - Cadeias de caracteres
    - Char: Tipo de dado fixo, char(10) vai consumir 10 bytes de armazenamento,              armazenamento máximo de 8000 bytes
    - Varchar: Tipo de dado variável, varchar(10) consome somente a quantidade         usada pela string, armazena até 8000 bytes, mas tem o varchar(max)
    - Nvarchar: unicode variable length character, usado para receber caracteres                 de outros idiomas, ocupa o dobro de espaço do varchar
    - Text: armazenar até 2gb, não é possível usar a busca com like,                         descontinuado.
    - Varchar(Max): A partir do 2015, armazena até 2gb, não é possível criar                         índice em uma coluna varchar(max), de 1 à 8 bytes o SQL                          armazena os dados igual ao varchar, após esse valor o                            armazenamento é igual ao tipo text, é possível usar like.

- Constraints
  - Primary Key
    - Somente 1 por tabela

  - Foreingn Key
    - Coluna que referencia a PK de outra tabela criando relação entre elas

  - Unique
    - Define campos como únicos
    - pode ter mais de 1 por tabela

  - Check
    - Validação realizada no momento do insert

  - Default
    - Valor default será inserido para uma coluna quando não for especificado no insert

SELECIONAR A TABELA E ALT + F1 PARA VERIFICAR NOME, DATA DE CRIAÇÃO, TODAS AS COLUNAS, TIPOS DE DADOS, COLLATION, INDEXS, CONSTRAINTS



# LINKED SERVER

- Funcionalidade do SQL para estabelecer conexão entre dois servidores
- Comunicação entre fontes OLE DB, como Excel, Acess, servidores SQL Server e até servidores como Oracle, MySql, Sybase
- USAR COM MODERAÇÃO EM PRODUÇÃO!!! Em tabelas grandes, ele pode causar locks e queries lentas. Muito lento para grandes volumes.


# DETACH E ATTACH

DETACH
  - Retira base de dados do SQL (MDF e LDF)

ATTACH
  - Coloca a base no SQL

Usado para mover base de um disco para o outro, mudar de servidor. 

Recomendado realizar backup e restore

Outra opção sem usar DETACH E ATTACH

  1 - Rodas o comando: ALTER DATABASE NOME SET OFFLINE(ninguém pode estar conectado na base)
  2 - Alterar o caminho dos arquivos na master com o ALTER DATABASE
  3 - Copiar os arquivos para os novos locais
  4 - Rodas o comando: ALTER DATABASE NOME SET ONLINE


# SHRINK

Reduz tamanho de arquivo MDF, LDF e NDF do SQL Server.

1 - Quando usar? Detelou uma tabela gigante, mas o disco continua usando o tamanho daquele arquivo

Quando deleta uma tabela o dado não é liberado no disco, apenas dentro do MDF. O disco fica alocado por isso continua usando o espaço em disco.

2 - Quando usar? Fez update gigante ou inseriu muitos dados de uma vez, o LOG vai CRESCER MUITO. Pode rodar o SHRINK para reduzir o tamanho.

Problemas:
- Demora muito para rodar
- Índices/Banco ficam fragmentados

Usar somente se realmente for necessário, quando é um espaço realmente que vale a pena
É preciso de uma janela de preferência final de semana quando o banco não está em uso
Após usar SHRINK, é necessário REBUILD nos Índices para desfragmentar

No LDF pode usar com mais tranquilidade, pois roda rápido. Não pode virar rotina. Pode usar em produção
No MDF é necessário muito cuidado, fazer em ambiente de teste para entender o tempo que levará


QUERY PARA VERIFICAR O TAMANHO DO LOG DAS DATABASES

DBCC SQLPERF(LOGSPACE)














