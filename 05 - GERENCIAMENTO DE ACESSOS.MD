## ACESSO SYSADMIM É SOMENTE PARA DBA

# SEGURANÇA A NÍVEL DE SERVIDOR
- Criação de LOgins no SQL Server
  - Windows(Domínio)
  - Do SQL Server

A melhor prática é usar login de domínio por conta das politicas de segurança do AD.

Em caso de precisar criar login para alguma aplicação, podemos usar o login direto do SQL Server.

Cria o login na aba GENERAL.
- Em login do SQL Server, uma das opções mais interessantes é a que força a colocar uma senha complexa.
- DEFAULT DATABASE: Onde o usuário vai cair ao entrar no servidor. 

SERVER ROLES.
- Focar na Sysadmin. Se a pessoa for DBA, usar esse acesso, caso contrário deixar em public que permite apenas que o usuário consiga logar e ir para aba USER MAPPING.

# SEGURANÇA A NÍVEL DE DATABASE

USER MAPPING
- Definir permissão por base de dados.
- Ao selecionar as bases de dados, precisará definir o database role.
- Em boa parte dos casos usará somente:
  - db_owner: usuário que precise fazer tudo dentro da database 
  - db_datareader: usuário que precisa ler todas as tabelas, views e functions(acesso de leitura, usar SELECT) 
  - db_datariter: usuário que precisa fazer insert, update e delete(acesso de escrita)


# SEGURANÇA A NÍVEL DE OBJETOS(TABELAS, VIEWS, FUNCTIONS, PROCEDURE)

GRANT:
  - GRANT SELECT, UPDATE, INSERT ON OBJETO TO USUARIO
  - GRANT EXECUTE ON PROCEDURE TO USUARIO

DENY
  - DENY SELEC, UPDATE, INSERT ON OBJETO TO USUARIO

REVOKE
  - REVOKE SELECT ON OBJETO TO USUARIO


--

Login é nível de servidor
- Quando cria um login fica "Security" -> "Logins"

Usuário é nível de database
- Quando criar um usuário fica dentro da database em "Security" -> "Users"




