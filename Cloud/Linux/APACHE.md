# Apache
***Install***
``` shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apache2
sudo chkconfig httpd on
sudo service httpd start
sudo systemctl httpd enable
```

**Configurando**  
```
/etc/httpd/conf/httpd.conf - ADICIONAR NA ULTIMA LINHA DO ARQUIVO
 IncludeOptional conf.d/*.conf
```
**Erros**  
``` shell
sudo chmod -R 777 /var/www/html/
sudo chown -R apache:apache /var/www/html/
sudo chown -R daemon:daemon
```

***Firewall debian***  
``` shell
sudo ufw app list
sudo ufw app info "Apache Full"
sudo ufw allow in "Apache Full"
sudo service apache2 restart
sudo ufw allow 80
sudo ufw allow 443
sudo ufw reload
sudo ufw enable
sudo ufw allow 22
sudo ufw reload
sudo ufw disable
```

***Firewall Centos***
``` shell
firewall-cmd --add-port=9090/tcp --permanent
firewall-cmd --add-port=9100/tcp
firewall-cmd --reload
```

***Comandos***
``` shell
apachectl configtest
```