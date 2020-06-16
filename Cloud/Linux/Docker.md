# Docker
***Container***  
* VIRTUALIZACAO DA SUA APLICACAO  
Converte sua aplicacao para um binario com tudo que sua aplicacao precisa
Apenas 1 kernew gerencia todos os containers
Podemos dizer que Conteiner sao VM pequenas pois ele emula sua aplicacao
Name space - faz a identificacao dos Dockers
C group - limita e libera recursos para o container (memoria, cpu, ...)
Netfilter - configura a rede, portas de entrada, ...

***ERROS***  
* DNS - https://development.robinwinslow.uk/2016/06/23/fix-docker-networking-dns/

***Requisitos***  
*processador 64bits*  
*kernew acima da 3.8 - uname -r*

***INSTALANDO***  
Docker Debian  
* ***Install***  
``` bash
curl -fsSl https://get.docker.com/ | sh
docker --version  
  * se nao foi usa: /etc/init.d/docker start  
```
* ***Docker Composer***  
``` bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose  
chmod +x /usr/local/bin/docker-compose  
docker-compose --version    
```
Docker Centos  
* ***Install***  
``` bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  
sudo yum install docker-ce  
sudo usermod -aG docker $(whoami)  
sudo systemctl enable docker.service  
sudo systemctl start docker.service  
```
* ***Compose Centos***  
``` bash
sudo yum install epel-release  
sudo yum install -y python-pip  
sudo pip install docker-compose  
sudo yum upgrade python*  
docker-compose version  
```
DOCKER AWS
* ***Install***
``` bash
sudo amazon-linux-extras install docker -y
sudo service docker start 
sudo usermod -a -G docker ec2-user
```
* ***Docker Compose***
``` bash
sudo curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-`uname -s`-`uname -m` | sudo tee /usr/local/bin/docker-compose > /dev/null
sudo chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

***Administrando container***  
``` docker
docker run IMAGE - cria um container se nao tiver a imagem ele da um pull
docker container ls - mostra containers em execucao
docker images - mostra todas as imagens baixadas e paradas
docker container ls -a - mostra todos os containers ja executados
docker container run -ti IMAGEM /bin/bash - cria container com terminal interativo *EX:docker run -ti centos:7*
docker container run -d IMAGEM /bin/bash - cria container SEM terminal interativo *EX:docker run -d centos:7*
Ctrl + d - mata container
Ctrl + p + q - sai do container mas mantem ele em execucao
docker attach IdDoContainer - para voltar para o container
docker create IMAGEM - cria o container mais nao executa mais nada
docker stop IdDoContainer - pausa o container
docker unpause IdDoConteiner - despausa o conteiner
docker start IdDoConteiner - starta o container
docker status IdDoConteiner - mostra uso de cpu, memoria, disco, rede...ME
docker rm IdDoConteiner - remove tudo do conteiner se nao estiver em execucao
docker inspect IdDoConteiner - mostra um overview sobre o msm
 OBS: podemos rodar ele com grep ex: | grep -i mem - para memoria
docker container run -ti --name NOME IMAGEM - o NOME seria o nome que vc pode dar para o container
docker container run -ti --memory NumeroUnidade --name NOME IMAGEM - com o campo memory aplicamos um maximo de ram ex: 512m - 512 megabytes
 OBS: podemos trocas --memory por -m
docker update IdDoConteiner -m 1024m NOME - com isso podemos alterar a RAM do container pelo NOME
docker container run -ti --cpu-shares 1024 -name NOME IMAGEM - assim colocamos o quanto de cpu podemos usar
 OBS: para entender como funciona.. se so tem uma com 1024 ela tem 100% do uso se temos uma com 1024 e outra com 512 uma tem 75% e outra 25%... assim vai
 OBG: podemos pesquisar cpu com | grep -i cpu
docker update --cpu-shares 512 NOME - assim podemos mudar cpu .. se temos duas com 512 cada uma tem 50%
docker container run -ti -v /home/ubuntu/DOCKER:/compartilhado -name NOME IMAGEM - assim damos o caminho para uma pasta compartilhada
 OBS : para encontrar no host "docker inspect -f {{.Mounts}} IdDoContainer"
docker container run -p PortaHost:PortaDocker - assim determinamos que porta acessa o docker
 OBS: podemos ver a saida disso no comando "iptables -t nat -L -n"
docker container run --mas-address ENDERECO - adicionar mac adress
docker container run --nat=host - assim todos os parametros de rede serao ferentes do host sem mais ip do container
docker container run -e VARIVAEL=VALOR - passa variavel de ambiente
docker container run --volumes-from NOME - importa volume de outro container
docker tag IdDoContainer NOME:VERSAO - para mudar nome do container
docker rmi -f NOME - apaga uma imagen
docker container run --restart=always - sempre q o serv reiniciar reinicia o container para n ficar off
docker container run --dns 0.0.0.0 - configura o dns do docker
docker container run --hostname NOME - nome de usuario
docker container run --link NOME - conecta conteiners
docker container run --expose NUMERO - expoe porta
docker container run --publish NUMERO:NUMERO - expoe porta do host para porta do container
docker exec -it NOME CAMINHO - aqui podemos acessar container q n acessa via attach exCaminho: /bin/bash
docker exec -it id_ou_apelido comando - EXECUTA SEM ENTRAR 
docker stop $(docker ps -a -q) - para tudo
docker rm $(docker ps -a -q) - remove tudo
```
***SWARM***  
``` docker
docker swarm init - inicia node master
  OBS: esse comando ja te devolve o comando para adicionar NOS a esse cluster
  OBS: nao podemos ter menos de 51% dos master entao se tivermos 4 e dois parar ele nao funciona ja q perdeu 50% e so podemos perder 49% ja se tivermos 5 podemos perder 2 e ficamos com 60% em uso acima dos 51% minimo
docker node ls - mostra os nos adicionados ao cluster
docker swarm join-token manager/worker - devolve o comando para um no ingressar com alguma das opcoes ou atualizar um no para um novo cargo
docker node promete HOSTNAME - promove de worker para manager
docker node demote HOSTNAME - passa de manager para worker
docker service create --name NOME -p PORTA:PORTA --replicas NUMERO IMAGEM - cria um servico no docker
docker service ls - mostra servicos
docker service ps NOME - tras onde e como estao rodando os servicos
docker service logs -f NOME - tras os logs
docker service create --name NOME -p PORTA:PORTA --replicas NUMERO --limite-cpu 2.4 IMAGEM - aqui o limite de cpu funciona por core nesse caso usamos 2.4 core e pensando que o servidor tem 3 core
docker service create --name NOME -p PORTA:PORTA --replicas NUMERO --limit-memory 500M IMAGEM - limitamos uso de memoria para cada container
docker container status IdDoContainer/NOME - tras um overview
docker service scale NOME=NUMERO - scala servico criando replicar pelos nods
docker service update --image NOME:VERSAO - faz um update da imagem em todos os containers do SWARM
 OBS: Eles nao compartilham o mesmo diretorio sabendo que voce esta suvindo em varios servidores logo e melhor adicionar um drive remoto como X-RAY
```
* ***Adicionando X-RAY***  
``` shell
curl -sSL httpd://rexray.io/install | sh -s -- stable
vim /etc/rexray/config.yml -ADICIONA O CONTEUDO ABAIXO COM AS CREDENCIAIS
rexray
  logLevel: debug
libstorage:
  service: ebs
  integration:
    volume:
      fileMode: 0777
      operations:
        mount:
          preempt: true
  server:
    services:
      ebs:
        driver: ebs
        ebs:
          acessKey: LOGIN
          secretKey: SENHA
          region: REGIAO
systemctl restart rexray
docker volume create --driver rexray NOME.exemplo1
rexray volume mount NOME.exemplo1
 OBS: dentro do docker_compose.yml voce adiciona:
  volumes:
    NOME.exemplo1:
      external: true - PORQUE VOCE TEM QUE CRIAR FORA DO COMPOSE O DRIVE COM O REXRAY
 OBS: para desmontar usa "rexray volume umount NOME.exemplo1"
``` 

***Dockerfile***  
``` docker
NOME DO ARQUIVO OBRIGATORIO Dockerfile
para rodar dentro do diretorio que se encontra o arquivo digita "docker build -t NOME:1.0 ."
 OBG:o ponto pode ser trocado pelo caminho assim nao tem q ser no local
FROM IMAGEM - OBRIGATORIO SER O PRIMEIRO determina imagem tipo debian
ADD nome.txt /CAMINHO/CAMINHO - add um arquivo em um lugar no container e manda tar.gz
CMD ["sh", "-c", "echo", "$HOME"] - parametro para principal processo container
LABEL Descricao="Bla bLa BLAA" - adiciona comentarios para seu container
COPY nome.txt /CAMINHO/CAMINHO - copia coisas para container
ENTRYPOINT ["/usr/bin/apache2ctl", "-D", "FOREGROUND"] - determina um processo que se parar mata o container junto
ENV nome="VariavelDeAmbiente" - cria uma variavel de ambiente para o container
 EX p/ apache:
  ENV APACHE_LOCK_DIR="/var/lock"
  ENV APACHE_PID_FILE="/var/run/apache2.pid"
  ENV APACHE_RUN_USER="www-data"
  ENV APACHE_RUN_GROUP="www-data"
EXPOSE 80 - EXPOE A PORTA 80
RUN apt-get PROGRAMA - roda comandos de terminal se for mais q um separa por && termina com "apt-get clean"
USER usuario - cria um usuario me nao colocar usuario fica root
WORKDIR /CAMINHO/ - diretorio padrao q acessa
VOLUME /CAMINHO/ - cria um diretorio compartilhado
 OBS: para encontrar no host "docker inspect -f {{.Mounts}} IdDoContainer"
 OBS: pode passar o caminho ex /CAMINHO/CAMINHO /CAMINHO
```

***Docker HUB***  
*aqui podemos conhecer e baixar IMAGENS PRONTAS*  
``` shell
https://hub.docker.com  
docker login - acessa  
docker push IdDoContainer - sobe uma imagen para o hub em vez do ID pode usar o NAME tb  
docker search NOME - busca imagem no HUB  
docker pull NOME - baixa imagem  
```

***Criando Docker Machine***  
 *OBS: instala o VM*  
``` shell
wget https://github.com/docker/machine/releases/download/v0.12.2/docker-machine-`uname -s`-`uname -m`
sudo mv DOCKER_MACHINE /usr/local/bin/
```

***Docker Compose***  
``` docker
nome docker-compose.yml
build: /CAMINHO/Dockerfile - executa o dockerfile
command: COMANDOS - executa um comando
container_name: NOME - passa o nome do container
dns: 0.0.0.0 - indica dns server
dns_search: exemplo.com - especifica dominio
dockerfile: CAMINHO/Dockerfil - aponta para dockerfile alternativo
env_file: .VARIAVEL -especifica variaveis de ambiente
environment: - adiociona variaveis de ambiente
  RACK_ENV: develipment
expose: - expoe portas do container
 - "8080"
external_links: - linka a container que n percisao estar no docker atual
 - redis_1
extra_hosts: - adiona uma entrada no /etc/hosts do container
 - "somehost:162.242.195.82"
image: centos:7 - indica uma imagem
labels: - adiciona metadata ao container
  com.example.description: "Bla"
links: - linka a container do mesmo docker
   - db
log_driver: syslog - indica o formato do log a ser gerado
log_opt:
  syslog-address: "tcp://192.168.1.1:123"
net: "hots" - modo de uso da rede
ports: - expoe portas do container e host
 - "3000"
volumes: - cria volumes
  - /var/lib/mysql
```
