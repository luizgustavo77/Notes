## **REST vs SOAP**
- **REST** Protocolo HTTP que usa Json e XML para a transferencia de objetos, podemos definir em GET e POST o **accept** que define o formato que aguarda como retorno
    - **Ex:** Chamadas para o controller no MVC, por padrão aceita a requisição por JSON
    - **Verbos:** GET, POST, PUT, HEAD, OPTIONS e DELETE

- **SOAP** XML apenas para a transferência de objetos entre aplicações via rede HTTP, não recebe requisições por javascript ja que nao trabalha com Json
    - Chamadas por URL em serviços