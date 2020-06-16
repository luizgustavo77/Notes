# Shell

***Dig***
> Consulta valor txt do _acme-challenge
```
dig -t txt _acme-challenge.URL
```

***criando o arquivo***  
```
sudo chmod +x NOME - adiciona execucao no arquivo ou usa o "sudo bash NOME"
nome do arquivo tem q ter .sh
```

***configurando o arquivo***  
```
#!/bin/bash - no inicio do arquivo
$1 - pega o primeiro parametro depois do NOME.sh
NOME = VALOR - assim podemos criar variaveis e chamar elas $NOME o VALOR pode ser caminho ~/home
**funcoes no linux q da certo retorna 0 maior que isso e errado
```

***Variáveis Especiais:***  
```
$* → Todos os valores passados como argumentos;
$n → O valor do argumento na posição n;
$0 → Nome do script que está sendo executado;
$1-$9 → Parâmetros passados pela linha de comando;
$# → Total de parâmetros passados;
$? → Valor de retorno do último comando ou de todo o script;
$$ → Número do processo executado (PID).
read NOME - espera a entrada de valores pelo terminal.
```

***Operadores Aritméticos:***
```
+ → Adição
- → Subtração
* → Multiplicação
/ → Divisão
** → Exponenciação
% → Resto da divisão (mod)
```

***Operadores de Comparação:***
```
= → Igual (strings)
!= → Desigualdade
< → Menor que
> → Maior que
<= → Menor ou Igual
>= → Maior ou igual
```

***Operadores de Expressões Condicionais:***
```
-lt → Número é menor que (LessThan)
-gt → Número é maior que (GreaterThan)
-le → Número é menor ou igual (LessEqual)
-ge → Número é maior ou igual (GreaterEqual)
-eq → Número é igual (EQual)
-ne → Número é diferente (NotEqual)
-a → E lógico (AND)
-o → OU lógico (OU)
```

***Testes em Arquivos:***
```
-d → Se for um diretório
-e → Se existir
-z → Se estiver vazio
-f → Se contiver texto
-s → Se o tamanho do arquivo for maior que zero
-r → Se o arquivo tem permissão de leitura
-w → Se o arquivo tem permissão de escrita
-x → Se o arquivo pode ser executado
-nt → Se o arquivo for mais recente (NewThan)
-ot → Se o arquivo é mais antigo (OlderThan)
-ef → Se o arquivo é o mesmo (EqualFile)

--output - nao mostra saida
--white-out - escreve na saida
**contrab -e - para executar de tempos em tempos
```

***algoritimos***
```
-usando FOR :
for VARIAVEL in $@/parametro
do
 COMANDO
done
-usando IF :
if[BOOL]
then
 COMANDO
fi
-usando WHILE:
while [validacao $variavel]
do
 COMANDO
done
```
***enviando EMAILS***   
[TomBuntu](http://tombuntu.com/index.php/2008/10/21/sending-email-from-your-system-with-ssmtp/)  

**Install**  
```
sudo apt-get install ssmtp
sudo vim /etc/ssmtp/ssmtp.conf
SSMTP - usado para configurar o envio de emails :
root=myemailaddress@gmail.com
mailhub=smtp.gmail.com:587
AuthUser=mygmailusername
AuthPass=mypassword
UseSTARTTLS=YES
```
**comando**
```
ssmtp myemailaddress@gmail.com < msg.txt
```
**msg exemplo**
```
To: myemailaddress@gmail.com
From: myemailaddress@gmail.com
Subject: alert

The server is down!
```