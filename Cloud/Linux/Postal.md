# Postal
***Instalando***  
 Obs: esta incompleto para fazer direito compara com: 
 * [GitHub](https://github.com/atech/postal/wiki/Installation)
 * [AboutCode](http://aboutcode.net/postal/)  
 * [HowToForge](https://www.howtoforge.com/tutorial/how-to-create-a-fully-featured-mail-server-using-postal/)
``` bash
curl https://raw.githubusercontent.com/atech/postal/master/script/install/ubuntu1604.sh | sh
postal make-user
sudo -u postal postal start
postal stop
vim /etc/systemd/system/postal.service
# [Unit]
# Description=Postal Mail Platform
# After=mysqld.service rabbitmq-server.service
# Wants=mysqld.service rabbitmq-server.service
#
# [Service]
# ExecStart=/usr/bin/postal start
# ExecStop=/usr/bin/postal stop
# ExecReload=/usr/bin/postal restart
# User=postal
# Restart=on-failure
# Type=forking
#
# [Install]
# WantedBy=mysqld.service rabbitmq-server.service

systemctl enable postal
systemctl start postal
postal restart
node -v
npm -v
apt install npm
sudo apt install git
postal auto-upgrade
postal auto-upgrade --channel beta
```

**CLOUDFLARE**  
```
 add A no cloudflare
 add txt NOME.ymi.io -  conteudo ele da no postal
 add DKIM q tb e txt com o nome em negrito e o e o conteudo
 add rp.NOME.ymi.io com o ip do serv
 add CNAME psrp.NOME.ymi.io para o rp.NOME.ymi.io
 add MX NOME.ymi.io p/ nx.NOME.ymi.io
 add MX nome.ymi.io p/ IP
 VALIDA
```