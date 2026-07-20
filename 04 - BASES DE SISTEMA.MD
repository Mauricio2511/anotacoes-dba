## PRECISA TER BACKUP DE TODAS AS BASES DE SISTEMA(MASTER, MODEL E MSDB), EXCETO A TEMPDB.

## MASTER

- Contém informações de configuração da instância, localização dos arquivos LDF e MDF do SQL Server, login, linked server e etc
- Não é possível restaurar a master em versões superiores do SQL Server atual instalado.
- Bases de sistema não restaura em versões superiores, é necessário levar os arquivos, configurações, usuários via scrip.

## MODEL

- Base modelo que é utilizada para a criação de novas bases de dados.
- Também utilizada para criar o TempDB toda vez que o SWL Server é iniciado.

## MSDB

- Utilizada pelo SQL Agent, Database Mail e Service Broker.
- Contém todas as informações de Jobs e histórico de Backup e Restore.

## TEMPDB

- Uma das bases com mais I/O em qualquer ambiente SQL Server
- É utilizada para tabelas temporárias, cursores, tabelas variável, rebuild ONLINE de índices, order by e group by(em caso de pouca memória) e etc.
