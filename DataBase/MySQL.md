# MySQL
## Centos
**Install**  
[StackOverflow](https://stackoverflow.com/questions/39025524/how-to-install-mysql-5-7-on-amazon-ec2)  
***
**Comands**  
```
mysql> GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost'; - permissoes para usuario  

ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass'; -  altera pass root  

ALTER USER 'yourusername'@'localhost' IDENTIFIED WITH mysql_native_password BY 'youpassword'; - permite conexao remota
```
## Debian
**Install**  
[Youtube](https://www.youtube.com/watch?v=ug0TFsort24)
``` bash
sudo apt-get install mysql-server
sudo mysql_secure_installation
y
NIVEL DA SENHA...
y
y
y
y
y
sudo mysql -u root -p
use mysql
UPDATE user SET plugin='mysql_native_password' WHERE User='root';
UPDATE mysql.user set authentication_string=PASSWORD('SENHA') where user='root';
FLUSH PRIVILEGES;
quit
```