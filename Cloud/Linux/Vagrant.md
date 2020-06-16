# Vagrant
***configs do vagrant***  
```
sudo apt-get install virtualbox
sudo apt-get install vagrant
vagrant version - versao
vagrant init - inicia arquivo para config do vagrant
vagrant status - mostra status da maquina virtual
vagrant up - vai iniciar a maquina virtual
vagrant ssh - entra no ssh da maquina virtual
vagrant halt - desliga
vagrant destroy - apaga tudo
vagrant reload - reinicia a maquina vitural
```
***Criando***
```
vagrant init - dentro do diretorio para dar o arquivo padrao de config do vagrant
config.vm.box: ... - podemos dizer qual SO para ver os disponiveis acesse https://vagrantcloud.com/search
config.vm.network: ... - redireciona tudo que chegar na porta 8080 para uma porta padrao
config.vm.provider "virtualbox" do |vb|
 vb.gui = boll - para dizer se vai ter interface grafica
 vb.memory = "..." - quanta memoria vai ter
end
config.vm.provision = "shell", inline: <<-SHELL
AQUI COLOCA TODO O SHELL QUE QR NA MAQUINA
SHELL
```
***EXEMPLO:Vagrant***
```
Vagrant.configure("2") do |config|
    config.vm.box = "debian/stretch64"
    config.vm.network :forwarded_port, guest: 80, host: 8080
    config.vm.network :private_network, ip: "192.168.33.11"
    config.vm.provider "virtualbox" do |machine|
    	machine.memory = 2024
    	machine.name = "vagrant" 
    end
    config.vm.provision :shell, path: "setup.sh"
end
```

***EXEMPLO:setup.sh***
```
echo "install vim"
sudo apt-get -y install vim

echo "install curl"
sudo apt-get -y install curl

echo "install net-tools"
sudo apt-get install net-tools

echo "update all"
sudo apt-get update && apt-get upgrade
```