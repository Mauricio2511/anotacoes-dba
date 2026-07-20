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


