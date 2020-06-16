# LINUX 

***Comandos basicos***
``` bash 
Tab- completa o comando
cd NOME- muda diretorio atual e no NOME colocando .. volta um ... volta dois e por ai vai
pwd - exibe diretorio atual
mkdir - cria pasta
cp -r ARQUIVO CAMINHO - copia uma pasta/arquivo para um diretorio
mv ARQUIVO CAMINHO - move ou renomeia arquivo para renomear so colocar o nome no CAMINHO
echo - escreve ou cria txt
rm -r - apaga com tudo que tem dentro
cat - mostra oq tem no arquivo
clear - limpa terminal
ls - lista com -la mostra ocultos detalhados
rwho - mostra usuarios conectados
locate NOME - localiza
 sudo updatedb - atualiza diretorio apos instalar locate
rmdir - remove diretorio
vi NOME - le ou cria txt
vim NOME - le ou cria txt
 yy - copia linha toda
 dd -- apaga linha toda
 i - insert
 :wq - sai e salva
-q - nao mostra processos
```
***zip unzip***  
``` bash
zip NOME.zip NOME - zipa arquivos
unzip -r NOME.zip - unzip de arquivos
tar -cz NOME > NOME.tar.gz - zipa arquivos formato TAR
tar -xz < NOME.tar.gz
```

***manipula processos***
``` bash
ps - lista processos
ps -e - mostra todos os processos
kill NUMERO - mata processo
kill -9 NUMERO - MATA SEM CHANCE DE FECHAR PELAS CONFIGURACAO
grep NOME - busca
top - mostra processos da CPU
 top -u USUARIO - mostra processos de CPU do usuario
jobs - mostra processos abertos no terminal
 crtl+z - pausa processo
 crtl+c - mata processo
 bg NUMERO - joga no background
 fg NUMERO - joga no terminal
 estree NUMERO - mostra ramificacoes
``` 
***executa prog e manipula usuario***
``` bash
chmod +/- x/w/r NOME - adiciona ou retira permissoes
which NOME - mostra de onde vem
sudo passwd - muda ou cria senha para usuario
sudo adduser - cria um usuario novo
sudo userdel -r NOME - deleta usuario
whoami - diz qual usuario esta usando
sudo chmod o-r/x/w NOME - para adicionar ou retirar direito de um usuario
install NOME - instala
search  NOME - procura
update - atualiza tudo
remove NOME - remove
sudo dpkg -i NOME.deb - instala um deb
sudo dpkg -r NOME.deb - desinstala deb
sudo service start/stop - para controlar um servico
ssh -x usuario@ip - acessa com interface
sudo scp -r ARQUIVO usuario@ip:/home/usuario - manda arquivo para o servidor
**Dispensando uso de senha para sudo
#includedir /etc/sudoers.d
lg ALL=(ALL) NOPASSWD:ALL
```

***Adiciona ou altera portas SSH***
``` bash
Conecte-se ao seu servidor por SSH
Alternar para o superusuário
Execute o seguinte comando:
vim /etc/ssh/sshd_config
Localize a seguinte linha:
# Port 22
Remover # e altere 22 para seu número de porta desejada. - PARA ADICIONAR MAIS SO PRECISA COLOCAR MAIS "Port NUMERO" abaixo desse
Reinicie o serviço sshd executando o seguinte comando:
service sshd restart
```

***Obtendo infra***
``` bash
cat /proc/cpuinfo - tras info do processador
cat /proc/meminfo - tras indo da memoria ram
df -h - tras indo do DISK
du -lh /CAMINHO --max-depth=1 - mostra o usu de tudo centro do CAMINHO
sudo du -a / | sort -n -r | head -n 20
top - mostra servicos em ordem de consulmo
cat /etc/*-release
```
***Migrando arquivos***  
* *Exportar a base de dados:*  
``` bash
sudo /usr/bin/mysqldump --force --opt --user=root -p --databases ymi_theconcept_dev | gzip > "/home/dumps/DUMP/2018-09-25_PM/DB.gz"
```  
* *Enviar via rsync para a outra máquina:*  
``` bash
rsync --progress -avz -e "ssh -i /CAMINHO" /home/dumps/DUMP/2018-09-25_PM/DB.gz root@IP:/home/import_databases
```
* *Descompactar o arquivo:*
``` bash
gunzip /home/import_databases/BD.gz
```
* *Importar o banco de dados:*
``` bash
mysql -u root -p -f < /home/import_databases/BD
```

***DEBIAN***  
* ERRO- As assinaturas a seguir não puderam ser verificadas devido à chave pública não estar disponível: NO_PUBKEY 93C4A3FD7BB9C367
* SOLUCAO- sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys NÚMERO_DA_CHAVE

***Variavel de Ambiente***  
[Conteudo tirado de](https://www.todoespacoonline.com/w/2015/07/variaveis-de-ambiente-no-linux/)
``` bash  
export VARIAVEL="VALOR" - adiciona variavel   
env | grep NOME - busca variaveis  
sudo nano /etc/bash.bashrc - adiciona permanente igual na primeira linha export VARIAVEL="VALOR" ao final do arquivo
```

***Cluster VS LoadBalance***  
Um cluster é para garantir redundância em caso de falha, e o load balance é para distribuir uma carga de requisições/processamento. Depende de onde e com qual serviço ou aplicação você está trabalhando, cada caso deve ser analisado em particular.

***Teclado***
``` bash
sudo dpkg-reconfigure keyboard-configuration
```
***Firewall debian***  
``` shell
sudo ufw app list
sudo ufw app info "Apache Full"
sudo ufw allow in "Apache Full"
sudo ufw allow 80
sudo ufw allow 443
sudo ufw reload
sudo ufw enable
```

***Firewall Centos***
``` shell
firewall-cmd --add-port=9090/tcp --permanent
firewall-cmd --add-port=9100/tcp
firewall-cmd --reload
```

***Auto Startup prog on Debian***
``` shell
sudo update-rc.d apache2 enable
```