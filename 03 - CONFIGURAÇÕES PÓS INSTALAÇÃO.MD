## INSTALAÇÃO DO ÚLTIMO SERVICE PACK DISPONÍVEL PARA A VERSÃO UTILIZADA

- Sempre instalar em um servidor de homologação antes
- Sempre realizar backup das bases

RTM: Primeira versão de um SQL Server, nunca foi atualizado
Cumulative(CU): Atualizações de correção, pode existir mais de um, exemplo: cu1, cu2, etc..
SP(service Pack): Contempla todas as atualizações cumulativas. Pode conter mais de um também

Para instalar o último SP, não precisa instalar os anteriores. Ele já contém todas atualizações anteriores.

SERVICE PACK É INDISPENSÁVEL.
Atualização por instância

HOTFIXES(Cumulatives)
- Indicação é sempre instalar as atualizações cumulativas
- Necessário uma boa rotina para conseguir instalar, pois é necessário parar o servidor
- SP é importante ter uma rotina definida também

Site que contém todas as atualizações do SQL Server:
https://buildnumbers.wordpress.com/sqlserver/


## CONFIGURAÇÃO DE MEMÓRIA DO SQL SERVER

Por padrão o SQL Server vem com a configuração para usar 100% da memória disponível. 

O SQL Server usa muita memório, pois tenta manter o máximo de páginas de tabela em cache para trazer um resultado mais rápido, evitando ter que consultar no disco porque é mais lento


Recomendação:

| RAM total do Servidor| Recomendado para o SQL Server |
|---:|---:|
| 16 GB | 12 GB |
| 32 GB | 28 GB |
| 64 GB | 56 GB |
| 128 GB | 112 GB |


## PARALELISMO

Quantidade de cores que o SQL usa para realizar uma query

- MAX DEGRER OF PARALLELISM
  - A recomendação é limitar a quantidade de cores que poderão ser usados em uma query. Máximo recomendado é apenas 8 cores. Por padrão vem 8 que indica que o SQL usará todos os cores

- COST THERESHOLD FOR PARALELISM
  - Definir também a partir de qual custo uma query deverá usar paralelismo. Por padrão vem 5, mas pode aumentar pra cima de 35 que não terá problema


## ERRO LOG

- Sempre o o SQL reiniciado, é criado um novo arquivo.
- Ideal é aumentar para +-20 a quantidade de arquivo de ERROR LOG.

Os arquivos de erros log crescem rápidos. Para evitar arquivos gigantes, criar um JOB para rodar semanalmente a SP abaixo:

exec sp_cycle_errorlog

Essa SP vai criar um novo arquivo de error log. Cada arquivo terá 1 semana de error log.


## INSTANTE FILE INITIALIZATION

Serve para o arquivo MDF. Opção que foi marcada na tela de configuração de contas e collation

- Em restore, com isso habilitado ao invés do SQL limpar o MDF para depois gravar os arquivos do restore, o SQL vai gravar por cima, evitando a demora nessa limpeza.
- Melhora também o tempo de criação de novas bases do crescimento
- Em instância já instalada que não está habilitado, é necessário parar o banco para habilitar

