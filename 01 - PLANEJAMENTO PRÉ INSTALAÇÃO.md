# anotacoes-dba

## Instalação e Configuração

# 1. DEFINIR A MELHOR VERSÃO

Versões:

- **Enterprise** (Edição com o conjunto mais completo de funcionalidades e maiores limites de hardware) / Mais cara
- **Standard** (Funcionalidades e hardware limitados, mas geralmente atende bem até grandes negócios) Mais em conta 
- **Developer** (Possui recursos da versão Enterprise, mas não pode ser usada em ambientes de produção) gratuita
- **Web** (Edição voltada principalmente para hospedagem de sites e aplicações por provedores de serviços), muito comum em datacenters
- **Express** (Muitas limitações de hardware e funcionalidades), em algumas empresas pequenas pode até ser utilizado, exemplo: padaria ou mercado pequenos.

# 2. PLANEJAR ONDE SERÁ INSTALADO

- Binários
- Base de dados
    - Dados, Log, TEMPDB (ideal é separar cada um deles em um disco diferente). Dificilmente é possível separar, mas se conseguir, separar Dados e Log
    - RAID (1, 5 e 10): O RAID 10 geralmente oferece melhor desempenho de escrita e redundância. O RAID 5 não é tão bom para escrita.

# 3. DEFINIR A COLLATION QUE VAI SER UTILIZADA PELA INSTÂNCIA

- Collation - Determina as regras que o SQL Server utiliza para comparar e ordenar caracteres
- Se for um SQL novo, questionar ao dono da aplicação qual a collation o SQL Server deve ter para a base.

**SE FOR REALIZAR UMA MIGRAÇÃO, É INDISPENSÁVEL SABER QUAL A COLLATION DO SQL INSTALADO ATUALMENTE
**

- Existe Collation na instância e também cada base pode ter uma collation diferente
  - Ficar atento a collation da base ser diferente, pois pode dar problema ao fazer query comparando string com a TEMPDB ou com uma base de collation diferente.
- Caso instale a instância com a collation errada, será necessário avaliar a reinstalação da instância ou a reconstrução das bases de sistema com a collation correta. Reinstalar a instância é menos trabalhoso e recomendado.
- Collation pode impactar na performance.
- Ao criar um novo banco se não definir a collation ele terá a mesma collation da instância

COLLATION CI_AI: Pode ser utilizada quando a aplicação não precisa diferenciar letras maiúsculas e minúsculas nem caracteres com e sem acento.  
- CI: Permite encontrar letras independente se a letra é maiuscula ou minuscula
- AI: Permite encontrar letras com ou sem acento

# 4. DEFINIR AS CONTAS DE SERVIÇO DO SQL SERVER

- Contas de domínio(uma por serviço)
- Recomendação(pelo menos 1 conta de domínio para o Agent e outra para o MSSQL Server), não precisam ser administrador da máquina
- Se usar as constas acima no momento da instalação, o próprio SQL da as permissões necessárias para cada conta
- O usuário que executa a instalação precisa ter permissão de administrador local. As contas utilizadas pelos serviços do SQL Server não precisam ser administradoras locais.


# 5. DEFINIR QUAIS RECURSOS E SERVIÇOS SERÃO INSTALADOS

Reporting Services, Analysis Services e Integration Services: Instalar somente os recursos e serviços que serão utilizados no ambiente.

# 6. PLANO DE ENERGIA DO SERVIDOR

- Deixar sempre em High Performance (Não economizar energia no servidor de banco de dados)



