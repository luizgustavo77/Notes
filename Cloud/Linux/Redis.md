# Redis
> open-source que armazena chaves com durabilidade opcional.

### Instalando 
[Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-a-redis-cluster-on-centos-7 "Simplificado abaixo")
``` shell
$ wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
$ sudo rpm -ivh epel-release-7-5.noarch.rpm
$ sudo yum -y update
$ sudo yum install redis -y
```
### Configurando
``` shell
$ sudo vim /etc/redis.conf
    adicione "requirepass SEU_REDIS_PASS"
$ redis-server /etc/redis.conf
$ redis-cli ping
```
### Principais comandos
``` shell
$ redis-cli - entra no banco
$ AUTH SEU_REDIS_PASS
$ SET "KEY" VALUE
$ GET "KEY"
$ DEL "KEY"
$ KEYS *
$ EXPIRE KEY TEMPO_EM_SEGUNDOS
```
### Redis Cluster
[Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-a-redis-cluster-on-centos-7 "Preguica de pegar tudo")
