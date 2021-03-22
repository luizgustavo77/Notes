# REDES

- **rede**
> maquinas interligadas
- **protocolo ping**
> icmp
- **ttl** 
> Numero de maquinas que os dados passam
- **nuckback** 
> 127.0.0.1 (testa placa de rede)
- **dns** 
> passa a url para ip
- **nslookup url** 
> retorna ip
- **hub** 
> liga maquinas a equipamqntos sem diferenciar 
- **computadores manda tudo para todos**
  - cabor:
  - t568a - t568b
- **wireshark** 
> Ver oque usuarios pesquisam
  - **ip.addr==ip**
  - **follow** 
  > tcp stream
  - **tcp** 
  > Transporta informacao
- **http** 
> Sem criptografia
- **https** 
> Com criptografia/SSL
- **switches** 
> Moldem que aprende onde usuarios estao
- **mascara de rede** 
> Configura quem esta na mesma rede
- **default gatway** 
> porta padrao de saida
- **nat** 
> Passa ip privado para publico
- **dhcp** 
> ip dinamico

- **http** 
> Regras da comunicacao porta 80
- **https** 
> Troca de dados com criptografia porta 443
- **cookies** 
> Arquivos texto gerados pelo site para guardar informacao do usuario
- **get** 
> Requisicao
- **post** 
> Atribuicao
- **delete** 
> Apaga
- **put** 
> Atualiza
- **xml** 
> Gerar linguagens de marcação para necessidades especiais.
- **json** 
> É um formato compacto, de padrão aberto independente, de troca de dados simples e rápida entre sistemas.
- **http2** 
> Passa binario e recebe gzip, antes da requisicao http o servidor faz uma requisicao TCP
- **RFC**    
> É a interface padrão de comunicação entre sistemas SAP. É através deste protocolo que as informações são trocadas entre diferentes ambientes

- **DTS (Data Transformation Services)**    
> É um método alternativo que pode ser utilizado para mover dados de um banco de dados do Access para o Microsoft SQL Server.

- **ETL  Extract Transform Load (Extrair Transformar Carregar)**   
> São ferramentas de software cuja função é a extração de dados de diversos sistemas, transformação desses dados conforme regras de negócios e por fim o carregamento dos dados

---

### **Protocolo HTTP**

- **TCP**
> Antes de efetuar a requisição o tem uma identificação entre CLIENT - SERVER para identificar as requisições

- **Função do HTTP**

  Definir um modelo que os dados vão seguir para trafegar 

- **Cabeçarios**
  - **Geral**
    - **Request URL:** Endereço do servidor
    - **Request Method:** Tipo de requisição
    - **Status Code:** Status do retorno
    - **Remote Adress:** IP servidor
  - **Headers**
    - **content-encoding:** Formato do retorno
    - **content-lenght:** Tamanho do retorno
    - **content-type:** Tipo de retorno
    - **date:** Hora de saida da requisição
    - **expires:** Hora pra timeout
    - **server:** Ferramenta que fez a requisição (ex: Google)
    - **location:** Indica em caso de redirecionamento (3xx), para ponde o cliente vai ser redirecionado
  - **Form Data**
    - Aqui temos o json com o objeto em requisições do tipo post



- **Como funciona a requisição para um conteudo HTML?**
> Na verdade quando fazemos uma requisição HTML o primeiro retorno trás apenas o texto com o html e para cada dependencia como imagens, css, js, etc... O navegador vai realizar mais uma requisição