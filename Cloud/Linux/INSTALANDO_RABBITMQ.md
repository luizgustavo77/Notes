# RabbitMQ
***Instalando rabbitmq***  
* ***erlang centos***  
```
sudo yum -y update
wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
rpm -Uvh erlang-solutions-1.0-1.noarch.rpm
rpm --import https://packages.erlang-solutions.com/rpm/erlang_solutions.asc
sudo yum install erlang
sudo yum install esl-erlang
```
* ***Instalando Rabbitmq***
```
sudo wget https://www.youtube.com/redirect?v=lTe0d6-nzHc&event=video_description&redir_token=5y1yaeS45YzsMlcfwYsJj8_5Brd8MTUzMzY0ODE1MkAxNTMzNTYxNzUy&q=https%3A%2F%2Fpackages.erlang-solutions.com%2Ferlang-solutions_1.0_all.deb

sudo dpkg -i erlang-solutions_1.0_all.deb

sudo apt-get install erlang erlang-nox

sudo echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list

sudo wget -O- https://www.youtube.com/redirect?v=lTe0d6-nzHc&event=video_description&redir_token=5y1yaeS45YzsMlcfwYsJj8_5Brd8MTUzMzY0ODE1MkAxNTMzNTYxNzUy&q=https%3A%2F%2Fwww.rabbitmq.com%2Frabbitmq-release-signing-key.asc | sudo apt-key add -

sudo apt-get update

sudo apt-get install rabbitmq-server

sudo rabbitmqctl add_user admin password 

sudo rabbitmqctl set_user_tags admin administrator

sudo rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"

sudo rabbitmq-plugins enable rabbitmq_management

/etc/init.d/rabbitmq-server restart
```

 > teste http://localhost:15672/

***Install c master***  
``` shell
git clone git://github.com/alanxz/rabbitmq-c.git
cd rabbitmq-c/
git checkout e1746f92585d59364fc48b6305ce25d7fc86c2a4
mkdir build && cd build
sudo apt-get install libssl-dev
cmake .. *** sudo apt-get install cmake *** sudo apt-get upgrade ***
cmake--build.
make
make install
```
**Instalando cluster***

[HowToForge](https://www.howtoforge.com/how-to-set-up-rabbitmq-cluster-on-centos-7/)
```
sudo vim /etc/hosts
IP rabbit-01
IP rabbit-02
IP rabbit-03
```