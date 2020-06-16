# Node Red
> npm_dir costuma ficar home  

> node-red esta no cd mas tem q estar como sudo su

***Adiciona NODO***  
``` npm
npm_dir faz os clones
```

***Remove NODO***  
``` npm
npm uninstall node-red-contrib-meli
```

***ON DEBIAN***  
``` bash
IR ATE /usr/lib E LA npm install DIR_GIT_CLONE
```

***Atualizar NODO***  
``` bash
npm_dir faz os pulls
2- Ir até o diretório do node-red e executar: npm install DIR_GIT_CLONE
pm2 l
pm2 restart 0
```
***ou***  
``` bash
sudo pm2 stop all
sudo pm2 start node-red
```

***Adiciona login***  
```
adminAuth: {
        type: "credentials",
        users: [{
           username: "ADMIN",
            password: "SENHA",
            permissions: "*"
        }]
    },
```

***CERTIFICADO DO NODE-RED***  
```
gera normal e add assim:
https: {
   key: fs.readFileSync("/etc/letsencrypt/live/CERTIFICADO/privkey.pem"),
   cert: fs.readFileSync("/etc/letsencrypt/live/CERTIFICADO/cert.pem")
 },
descomenta o "var fs = require("fs")"
pm2 reload all
httpAdminRoot: '/admin'
```

*Crontab -e
0 7 * * * certbot renew >/dev/null 2>/dev/null

***ATUALIZA NODE-RED***  
```
sudo npm install -g --unsafe-perm node-red
```

***Cria Senha***
```
npm install -g node-red-admin - Instala
node-red-admin hash-pw - depois de rodar vai pedir a Senha
```