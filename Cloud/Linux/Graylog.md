# GRAYLOG
***Install***  
[ItzGeek](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-graylog-on-centos-7-rhel-7.html)  
***Audirotia e captura de log***  
* logs - registro de eventos
* cluster - sistem com duas ou mais aplicacoes
* nodes - trabalham em conjunto para executar algo
* loadbalance - checa por ping para ver se recebe os dados 
> OBG: precisa de java8 e tem um PDF na pagina com passo a passo de como instalar

***administracao de usuarios***  
* ***syslog***
    * input - adiciona parametros e seleciona tipo de entrada
    * global - para funcionar em tudo 
    * node - seleciona a interface que manda os dados
    * blind adress - configura para parametros ou 0.0.0.0 para tudo
    * port - 1514
* ***nxlog***  
  * input gelf - substitui graylog
  * input - gelf tcp
  * porta - 12201
  * roles - cria regras

***Tags / Streams***  
```
~ - combinacao com palavras digitadas  
? - substitui uma letra por qual quer outra  
* - pega tudo ou varias letras  
>< = - numerico  
```

***Notificacoes***  
Pode configurar todas as regras ou so uma
tipos de regras e elas podem ser invrtidas - exatamente isso / expressao regular / maior / menor / campo presente / campo te q conter / sempre da certo 
 * condicao de alerta :  
 1- campo com valor tal  
 2- campo com valor max o min  
 3- quantidade de log por minut  

***Configurando memoria ram***   
``` shell
vi /etc/sysconfig/graylog-server = xms/xmx
/usr/share/graylog-server/plugin
```