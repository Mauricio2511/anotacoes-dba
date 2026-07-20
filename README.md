# anotacoes-dba

## Instalação e Configuração

# 1. DEFINIR A MELHOR VERSÃO

Versões:

- **Enterprise** (Funcionalidades ilimitadas dentro do que o SQL Server entrega) / Mais cara
- **Standard** (Funcionalidades e hardware limitados, mas geralmente atende bem até grandes negócios) Mais em conta 
- **Developer** (Possui recursos da versão Enterprise, porém é proibida para utilizar em ambiente de produção) gratuita
- **Web** (Mais usada em datacenter), não utilizado em empresa
- **Express** (Muitas limitações de hardware e funcionalidades), em algumas empresas pequenas pode até ser utilizado, exemplo: padaria ou mercado pequenos.

# 2. PLANEJAR ONDE SERÁ INSTALADO

- Binários
- Base de dados
    - Dados, Log, TEMPDB (ideal é separar cada um deles em um disco diferente). Dificilmente é possível separar, mas se conseguir, separar Dados e Log
    - RAID(SSD) (1, 5, e 10) Melhor é o 10, o 5 é ruim para escrita

# 3. DEFINIR A COLLATION QUE VAI SER UTILIZADA PELA INSTÂNCIA

- Collation - Determina as regras que o SQL Server utiliza para comparar e ordenar caracteres
- Se for um SQL novo, questionar ao dono da aplicação qual a collation o SQL Server deve ter para a base.

**SE FOR REALIZAR UMA MIGRAÇÃO, É INDISPENSÁVEL SABER QUAL A COLLATION DO SQL INSTALADO ATUALMENTE
**

- Existe Collation na instância e também cada base pode ter uma collation diferente
  - Ficar atento a collation da base ser diferente, pois pode dar problema ao fazer query comparando string com a TEMPDB ou com uma base de collation diferente.
- Caso instale a instância com collation errada, o mais recomendado e reinstalar com a correta
- Collation pode impactar na performance.
- Ao criar um novo banco se não definir a collation ele terá a mesma collation da instância

COLLATION CI_AI: (MELHOR DE SER UTILIZADA POR SER INSENSITIVE)
  - CI: Permite encontrar letras independente se a letra é maiuscula ou minuscula
  - AI: Permite encontrar letras com ou sem acento

# 4. DEFINIR AS CONTAS DE SERVIÇO DO SQL SERVER

- Contas de domínio(uma por serviço)
- Recomendação(pelo menos 1 conta de domínio para o Agent e outra para o MSSQL Server), não precisam ser administrador da máquina
- Se usar as constas acima no momento da instalação, o próprio SQL da as permissões necessárias para cada conta
- Não precisa ser administrado local do servidor para instalar o SQL Server


# 5. DEFINIR QUAIS RECURSOS E SERVIÇOS SERÃO INSTALADOS

- Reporting Service, Analyses Service, Integration Services(Integration Services, é uma boa instalar por conta das funcionalidades e também não é um pacote pesado, é um recurso leve)


# 6. PLANO DE ENERGIA DO SERVIDOR

- Deixar sempre em High Performance (Não economizar energia no servidor de banco de dados)



