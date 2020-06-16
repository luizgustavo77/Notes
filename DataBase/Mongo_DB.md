# MongoDB
***Install***  
[KingHost](https://king.host/wiki/artigo/mongodb-via-terminal-shell/)

**Export**  
``` mongo 
mongodump -d <database_name> -o <directory_backup>
```
**Import**
```
mongorestore -d <database_name> <directory_backup>
```
**Acessa**  
```
mongo -u usuário-da-base -p senha-da-base host-de-conexao/nome-da-base
```
