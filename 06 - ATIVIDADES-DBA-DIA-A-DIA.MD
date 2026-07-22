# DATABASES

Por padrão as bases são criadas com MDF e LDF.

.MDF
  - arquivos de dados

.LDF
  - arquivos de log


Existe também o .NDF, mas a criação é opcional. Que são mais arquivos para a base de dados.
Usado pelos arquivos secundários de dados
NDF = Not Master Data File


--

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

--



