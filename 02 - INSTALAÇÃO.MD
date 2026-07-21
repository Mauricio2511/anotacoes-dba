# INSTALAÇÃO DO SQL SERVER

- Next nas primeiras etapas até INTALATTION TYPE

## INSTALAÇÃO TYPE

- Escolher entre instalar uma nova instância ou instalar serviços em uma instância existente

##  PRODUCT KEY

- Inserir licença

## LICENCE TERMS

- Aceitas os termos

## FEATURE SELECTION

Nesta seção é definido os recursos que serão instalados

INSTANCE FEATURES - Recursos/Serviços por instância
- Database Engine Services
- Full Text and Semantic Extractions for Search

SHARED FEATURES - Recursos/Serviços que são instalados apenas 1 única vez independente da quantidade de instâncias que já possui instalada.
- Client Tools Connectivity
- integration Services
- Cliente Tools Backwards Compatibility
- Cliente Tools SDK
- SQL Client Connectivity SDK

INSTANCE ROOT DIRECTORY: Selecionar o disco e pasta de instalação

## INSTANCE CONFIGURATION

- Se for a primeira instalação/primeira instância na máquina, ir na ipção DEFAULT INSTANCE. Caso contrário ir em NAMED INSTANCE e definir o nome

## SERVER CONFIGURATION 

- Configurar usuários e collation
- SERVICE ACCOUNTS: Definir os usuários para cada serviço em SERVICE, conforme boas práticas do planejamento.
- STARTUP TYPE: Deixar em AUTOMATIC, principalmente no AGENT
- Marcar a caixinha do GRANT PERFORM VOLUME MAINTENANCE TASK PRIVILEGE TO SQL SERVER DATAVASE ENGINE SERVICE.

COLLATION: Definir a Collation

## DATABASE ENGINE CONFIGURATION

SERVER CONFIGURATION:
- Marcar MIXED MODE (SQL SERVER AUTHENTICATION AND WINDOWS AUTHENTICATION): Essa opção permite utilizar a autenticação do Windows e também logins do SQL Server. Ao marcar essa opção, é necessário definir uma senha para o login SA, que possui permissão de sysadmin.
- Definir uma senha segura para o SA, nos campos que pedem password.
- Adicionar o usuário da máquina que está fazendo a instalação como Administrador em ADD CURRENT USER.

DATA DIRECTORIES:
- Nesta etapa define quais os discos/locais para base/log

TEMPDB:
Essa tela é para configuração de arquivos para TempDB

- Por padrão, o SQL Server pode configurar até 8 arquivos de dados para a TempDB, de acordo com a quantidade de processadores lógicos disponíveis.
- Avaliar a adição de novos arquivos de dados caso seja identificada contenção na TempDB relacionada a PAGELATCH_UP ou PAGELATCH_EX.
- Dependendo da quantidade de processadores lógicos e da carga do ambiente, pode ser necessário utilizar mais de 1 arquivo de dados na TempDB.
- O indicado inicialmente é utilizar até 8 arquivos de dados, de acordo com a quantidade de processadores lógicos. Normalmente, a TempDB utiliza apenas 1 arquivo de log.
- Pode deixar o que vem por padrão/default


Opções importantes para verificar:

- Initial size MB: Definir o tamanho inicial de acordo com a carga do ambiente, evitando crescimentos frequentes. Os arquivos de dados da TempDB devem possuir o mesmo tamanho e a mesma configuração de crescimento.
- Initial size MB do TempDB Log file: Definir o tamanho inicial de acordo com a utilização do ambiente, evitando crescimentos frequentes do arquivo de log.

É possível alterar após o SQL Server estar instalado

FILESTREAM
Habilita quando vai trabalhar com arquivos muito grandes. Caso para ser analisado. Habilitar quando a aplicação precisar armazenar dados VARBINARY(MAX) no sistema de arquivos utilizando o controle transacional do SQL Server. Cada caso deve ser analisado.


## INSTALL

A partir das configurações acima basta clicar no install para finalizar



