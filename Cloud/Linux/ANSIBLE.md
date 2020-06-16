# Ansible
***COMO INSTALAR E RODAR O ANSIBLE*** 
```  shell
sudo apt-get install ansible
sudo apt-get install python-simplejson
sudo apt-get install python-pip
sudo apt install python-minimal
```

***COMO RODAR***  
``` shell
sudo ansible-playbook NOME.yml -i HOSTS – nome pode ser main ou provisioning
```

**HOSTS**
``` txt
[GRUPO]
IP ansible_python_interpreter=/usr/bin/python3 ansible_user=USER ansible_ssh_private_key_file="/CAMINHO/NOME.pem"
[vagrant]
IP ansible_user=vagrant ansible_ssh_private_key_file="/home/deeoin/Vagrant2/.vagrant/machines/default/virtualbox/private_key"
```
**PROVISIONING**
```
- hosts: all
  roles:
    - NOME
```
**HANDLERS / TASKS**  
```
-TAKS  
roles/NOMES/tasks/main.yml  
-HANDLERS  
roles/NOMES/handlers/main.yml
```

***Comunidade para buscar exemplos***  
[Ansible Galaxy](https://galaxy.ansible.com/)

***PROGRAMACAO***
```
--- //comeca com essas 3 barras
- hosts: //pode por all para ir todos ou um grupo especifico
  tasks: //abaixo vc poe os codigos
    - shell:'//aq dentro das aspas vai o codigo de terminal para ser executado tipo criar um arq txt '
// agr instalando pacotes (se fosse centos n era apt e sim yum....)
    - name: '//aq dentro coloca uma descricao do que o codigo abaixo faz'
      apt:
        name: "{{ item }}"
        state: //estado se refere a versao ex:lastest (seria a ultima)
      become: // bool que informa se quer executar como root ex:yes (iria usar o usuario root)
      with_items:
        - //nome do prog para instalar ex:php5
        - //demais items.
```

***PROGRAMACAO COM SQL***
```
---
    -name: '//aq dentro fica a descricao'
         mysql_db: //descricao tipo o apr entao fica em branco
           name: //nomde do db
           login_user: root
           login_password: //poe a senha se for ubuntu q n tem senha nao precisa adicionar esse campo
           state: //aqui e a magica da coisa... aq e a descricao do que sera feito (present(cria o db) ; absent(destruir o db) ; dump(guarda estrutura) ; import(aplica     script sql em um db vazio) EXEMPLOS: https://docs.ansible.com/ansible/latest/modules/mysql_db_module.html
```
***GERENCIANDO USUARIO NO MARYADB COM ANSIBLE***
```
---
- name: '//descricao'
    mysql_user: //usuario que vai rodar esse comando ROOT
    name: //nome do novo usuario
    password: //senha...
    priv: '//database(ou * para todos).tabela(ou * para todas):privilegios (ou ALL para todos)'
    state: //novamente o state e a magia da coisa tendo algumas opcoes segue novamente o link para ver todo conteudo EXEMPLOS: https://docs.ansible.com/ansible/latest/modules/mysql_user_module.html#mysql-user-module
```

***INSTALA POR CURL (HTTPS) E DESCOMPACTA***
```
---
- name: '//Baixa o arquivo de instalacao do Wordpress'
  get_url:
    url: https://wordpress.org/latest.tar.gz'
    dest: '/tmp/wordpress.tar.gz'

- name: '//Descompacta o wordpress'
  unarchive:
    src: '/tmp/wordpress.tar.gz'
    dest: /var/www/
    remote_src: yes //verifica se o arquivo ja existia no local NECESSARIO!
  become: yes
```

***FAZ COPIAS DE DIVERSOS PARAMETROS***
```
- name: '//descricao'
  copy:
    src: '/var/www/wordpress/wp-config-sample.php'
    dest: '/var/www/wordpress/wp-config.php'
    remote_src: yes
  become: yes
```

***EDITA ARQUIVO TXT***
```
- name: '//descricao'     
  replace:
    path: '/diretorio'
    regexp: "{{ item.regex }}"
    replace: "{{ item.value }}"
    backup: yes
  with_items:
    - { regex: 'campo que procura', value: 'como vaificar'}
  become: yes
```

***COMO COPIAR UM ARQUIVO PARA O SERVIDOR***
```
- name: 'Configura Apache para servir o Wordpress'
  copy:
   src: 'files/arquivo.txt'//obrigatorio usar o files
   dest: '/destino no servidor'
  become: yes
```

***COMO ALTERAR ESTADO DE UM SERVICE
```
- hosts: all
  handlers:
    - name: //NOME QUE SERA USADO PARA CHAMAR
      service:
        name: //descricao do servico ex:apache2
        state: //comando ex:restarted
      become: yes
PARA CHAMAR O COMANDO ACIMA USAMOS 
  notify:
    - //NOME ATRIBUIDO NO HANDLERS
```

***CRIANDO VARS***
```
//dentro do codigo podemos chamar variaveis assim:
"{{ NOME }}" 
//atribuimos os valores das variaveis assim
/group_vars/all.yml
//dentro de all fica assim
NOME: enderecamento
//TAMBEM E POSSIVEL CRIAR VARS VISIVEIS SOMENTE PARA UM GROPU DENOMINADO NO HOSTS SOMENTE CRIANDO O ARQUIVO COM O NOME DELE.
```

***APLICANDO VARS EM ARQUIVOS TXT***
```
//para determinar que dentro do arquivo ha uma variavel usamos
{{ nome }}//na posicao que se espera 
//para salvar as vars usamos o msm arquivo de vars do codigo '/group_vars/all.yml'
//como usar isso no codigo
- name: ' Configura Apache para servir Wordpress'
  template:
    src: 'templates/arquivoQueVamosJogarNoServidor.j2'//os arquivos que serao copiados para serv ficam em templates com extensao .j2
    dest: '/etc/apache2/sites-available/000-default.conf'
```

***DEFAULTS***
```
//no diretorio abaixo podemos criar um default para caso n encontre uma var no group_var use ela
roles/NOME/defaults/main.yml
//la aplica da mesma forma q no group
```