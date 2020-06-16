# Migração de Database MariaDB

* ***Exportar a base de dados:***  
``` bash
sudo /usr/bin/mysqldump --force --opt --user=root -p --databases BANCO | gzip > "/home/dumps/DUMP/2018-09-25_PM/BANCO.gz"
```

* ***Enviar via rsync para a outra máquina:***
``` bash 
rsync --progress -avz -e "ssh -i /home/centos/xavantes" /home/dumps/DUMP/2018-09-25_PM/BANCO.gz root@IP:/home/import_databases
```

* ***Descompactar o arquivo:***
``` bash
gunzip /home/import_databases/BANCO.gz
```

* ***Importar o banco de dados:***
``` bash
mysql -u root -p -f < /home/import_databases/BANCO
```