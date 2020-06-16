# CERTBOT
[Site Official](https://community.letsencrypt.org/t/getting-wildcard-certificates-with-certbot/56285)

***Instala e gera certificado***
``` shell
wget https://dl.eff.org/certbot-auto
sudo chmod a+x certbot-auto
apachectl configtest - depois apache2 reload
```

***RENOVA CERTIFICADO LEMBRE-SE DE ADICIONAR A KEY NO CLOUDFLAME OU AWS CHECAR AONDE APONTA*** 
``` shell
./certbot-auto certonly --manual -d *.example.com -d example.com --preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory

sudo certbot renew --dry-run
```

***AWS***
``` shell
sudo rm -rf /opt/eff.org/*
sudo yum -y install python36 python36-pip python36-libs python36-tools python36-virtualenv
sudo /usr/bin/pip-3.6 install -U certbot
sudo /usr/bin/pip-3.6 install certbot-apache
sudo /usr/local/bin/certbot renew --debug
```

***DELETA***
``` shell
sudo certbot delete --cert-name example.com
```

***SSL ON LOAD BALANCE***
``` txt
ADICIONA O PRIVKEY
ADICIONA FULLCHAIN
NA PAGINA INICIAL VAI APARECER A OPCAO DE ADICIONAR
```