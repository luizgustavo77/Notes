# aws
> Cloud Vender (plataformas de Cloud)  

*Nunca podemos usar a conta admin, o correto e criar uma conta com todas as permissoes para acessar e nao a admin*
* Lambda - custa por tempo de execucao, totalmente stateless (nao fica nenhum arquivo salvo), nao dura mais de 15min e toda funcao lambda precisa de um cloudwatch
 - Evento : podemos adicionar um evento que dispara a funcao de no Lambda descrevendo o metodo (Get,Put...) e ate um prefixo / sufixo necessarios para disparar a funcao
* S3 - sao volumes para armazenamento de dados em todos os formatos, o dentro do S3 voce pode criar Buckets que nada mais sao que containers individuais onde podemos configurar regras   
    * Todos os Buckets sao unicos e seu DNS (nome), deve ser diferente de todos os outros dentro da AWS
* CloudFormation -  ferramenta da AWS para receber informacao e entender oque esta sendo passado