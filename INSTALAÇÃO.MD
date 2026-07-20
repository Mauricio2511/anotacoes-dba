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
- Marcar MIXED MODE (SQL SERVER AUTHENTICATION AND WINDOWS AUTHENTICATION): Essa opção habilita a criação de usuários para o SQL SERVER, ao marcar essa opção também é criado o usuário SA que tem permissão de SIS admim.
- Definir uma senha segura para o SA, nos campos que pedem password.
- Adicionar o usuário da máquina que está fazendo a instalação como Administrador em ADD CURRENT USER.

DATA DIRECTORIES:
- Nesta etapa define quais os discos/locais para base/log

TEMPDB:
Essa tela é para configuração de arquivos para TempDB

- O recomendado é deixar apenas 1 arquivo
- Adicionar novos arquivos caso receba em WAIT INFO (PAGELATCH)
- Em bancos grandes é possível ter a necessidade de mais de 1 arquivo
- O indicado é usar no máximo 8 arquivos de log. Por padrão o SQL indica 1 por core do processados. 
- Pode deixar o que vem por padrão/default


Opções importantes para verificar:

- Initial size MB: Por padrão vem 8MB, mas pode aumentar, pois é muito pouco o padrão. Existe casos de 1GB para o TempDB. Cada caso deve ser analisado
- Initial size MB do TempDB Log file segue a mesma lógica acima

É possível alterar após o SQL Server estar instalado

FILESTREAM
Habilita quando vai trabalhar com arquivos muito grandes. Caso para ser analisado.


## INSTALL

A partir das configurações acima basta clicar no install para finalizar



