# **Engenharia de Software**
> Busca criar etapas para o processo de desenvolvimento de Software, para evitar falhas nos projetos e alavancar as empresas

- **Por que nasceu?** Usado pela primeira vez em 1968 na
conferencia da OTAN, busca de qualidade, orcamento baixo, dentro do prazo e atenda a necessidade do cliente, pois depois de pronto solucionar erros no codigo se torna uma luta 
    - **Qualidade:** Poucos bugs, desempenho, intuitivo, atende os requisitos, ...
    - **Principais falhas:** Por demanda, comunicacao ambigua, arquitetura fraca, testes falhos, ...

- **Requisitos da Area**
    - Requisitos de software
    - Análise e projeto
    - Construção
    - Teste
    - Gerência de projetos
    - Processo de engenharia de software
    - Gerência de configuração
    - Qualidade do software
    - Manutenção do software

- **Caracteristicas de um bom Software**
    - **Especialização versus adaptação:** Elaborar um plano de desenvolvimento de software, indicando em detalhes 
        - Os recursos necessários (humanos e materiais),
        - As estimativas de prazos e
        - Custos (cronograma e orçamento)
    - **Manutenção:**
        - Quanto maior o tamanho do sistema, mais recursos serão
    necessários para sua manutenção
    - **Composição:**
        - Qualquer sistema pode ser decomposto em sistemas menores
    - **Crescimento:**
        - Os sistemas tem uma natureza que tende ao crescimento
    - **Manufatura:**
        - Projeto + produção
    - **Desenvolvimento:**
        - Não existe produção
        - Dependência maior das pessoas
        - Falhas em uma cópia estão em todas as cópias
        - Não há perda de qualidade devido ao processo produtivo
        - Software não desgasta, deteriora-se


- **Manutenção**
    - **Manutenção corretiva:** modifica o software para corrigir defeitos.
    - **Manutenção adaptativa:** modifica o software para acomodar
    mudanças no seu ambiente externo 
    - **Manutenção de aperfeiçoamento:** aprimora o software além dos
    requisitos funcionais originais 
    - **Manutenção preventiva:** faz modificações nos programas de
    modo que eles possam ser mais facilmente corrigidos,adaptados e melhorados.

- **O Processo de Desenvolvimento**
    - **Inicio do processo de Desenvolvimento**
        - Inicia-se a partir de alguma necessidade do negócio
    - **A necessidade de um processo**
        - Todo o diálogo e a interação entre usuários,  rojetistas, ferramentas de desenvolvimento e  ecnologias devem ser transformados num processo.
    - **Processo de Software**
        - Define tarefas requeridas para se construir um software . 
---
## **O valor do software**
> Software é o combustível utilizado pelos negócios modernos   

## **O processo não é tudo!**

---

- **Modelo Cascata**
> Para projetos onde o cliente sabe oque quer e tem requisitos definidos
``` mermaid
classDiagram
      Especificacao --o Planejamento
      Planejamento --o Modelagem
      Modelagem --o Construcao
      Construcao --o Implementacao
      class Especificacao{ 
         - Incicio do Projeto
         - Requisitos
     }
      class Planejamento{
          - Cronograma
      }
      class Modelagem{
         - Analise 
         - Projeto
      }
      class Construcao{
          - Desenvolvimento
          - Testes
      }
      class Implementacao{
          - Entrega
          - Manutenção
          - FeedBack
      }
```

- **Modelo Evolutivo**
> Para processos onde o cliente não tem ideia definida do que precisa, trabalha com o feedback do cliente para modificar o projeto.

``` mermaid
graph TD
DefiniçãoEsboco-->d{Desenvolvimento}
d{Desenvolvimento}-->e(Especificacao)
e(Especificacao)-->d{Desenvolvimento}
d{Desenvolvimento}-->|Entregas Continuas|en(Especificacao)
d{Desenvolvimento}-->v(Validacao)
v(Validacao)-->d{Desenvolvimento}
en(Especificacao)-->VersaoInicial
en(Especificacao)-->VersaoIntermediaria
en(Especificacao)-->VersaoFinal
```

- **Modelo Incremental**
> Para processos onde temos mão de obra reduzida, gera etapas incrementais (ou sistemas), que dividimos o projeto e liberamos ele em modelos simplificados.    

``` mermaid
graph TD
Projeto-->|_Dividindo_|s1(Sistema1)
Projeto-->|_Dividindo_|s2(Sistema2)
Projeto-->|_Dividindo_|s3(Sistema3)
Projeto-->|_Dividindo_|sn(Sisteman)
s1(Sistema1)-->|_FeedBack_|v{Valida}
s2(Sistema2)-->|_FeedBack_|v{Valida}
s3(Sistema3)-->|_FeedBack_|v{Valida}
sn(Sisteman)-->|_FeedBack_|v{Valida}
v{Valida}-->ProjetoFinal

```
---

### **Desenvolvimento da documentação do projeto:** 
> Para este projeto as etapas incrementais podem ser assim definidas:
- **Primeiro incremento:** poderia efetuar as funções de controle de
versões de arquivos, edição e produção de documentos.
- **Segundo incremento:** adicionaria capacidade de edição e de
produção de documentos mais sofisticadas.
- **Terceiro incremento:** incluiria a verificação sintática e gramatical.
- **Quarto incremento:** adicionaria a capacidade avançada de
disposição de página.

**Note que todo o processo pode se repetir até que um produto
completo seja produzido**

---
### **UML**, Unified Modeling Language
> Percebeu-se a necessidade de um padrão para a modelagem de
sistemas, que fosse aceito e utilizado amplamente.
- **Oque é?**   
    - uma linguagem visual.   
    - independente de linguagem de programação.   
    - independente de processo de desenvolvimento.   
- **Não é**
    - uma linguagem programação (mas possui versões!).
    - uma técnica de modelagem.


---
### **Caso de Uso**

- Ponto de uso do ator do sistema
- Sequencia de interacao entre o agente e o sistema
- Define parte da funcionalidade do sistema
- Menos abstracao mais detalhado
```
detalhamento |
             |
             |_______________abstracao
            /
           /
          /
  formato/
```

- **Tipos de caso de uso:**
    - **Principal objetivo:** Objetivo dos atores
    - **Secundario:** Nao tras beneficio mas e essencial

- **Algumas secoes normalmente encontradas:**
	- sumario
	- atores
	- fluxo principal
	- fluxo alternativo
	- referencia cruzada
---

# **PROVA**
1. Porque o software não envelhece mas se deteriora. Oque pode ser feito para ele não deteriorasse?   
R: Porque nos fazemos melhorias e alterações. Para não deteriorar podemos evitar mecher no software.
2. Porque os software legado geralmente exibem uma baixa qualidade?   
R: Pois antigamente os requisitos e recursos eram outros.
3. Oque julga essencial na engenharia de software?   
R: Aumenta a qualidade, diminuir o tempo e diminuit o custo

1. Explique porque um processo de software permite melhorar
continuamente a qualidade de suas entregas
R: Manutenção previa, metodologia, acompanhamento continuo 
2. Qual a diferença entre um processo de negócio e um requisito de
software?
R: Processo de negocio e a regra aplicada dentro do sistema ja o requisito faz parte da arquitetura definida
3. Estabeleça uma analogia entre o processo de captura, tratamento,
distribuição, e qualidade assegurada da água da sabesp, com um
processo de desenvolvimento de software.
R:  Captura agua > Entrada de dados
    Tratamento e distribuição > Tratamento de dados e armazenamento
    Qualidade da agua > Qualidade do software testado
4. Quais atividades do processo de desenvolvimento de software se
referem ao o “que” e ao “como” fazer?
R:  Que > Qual o processo, regra do cliente
    Como > projeto do software, geração de código, teste de software.
5. Verificação e validação do software são as mesmas coisas?
R:  Validação > se o sistema faz oque o cliente queria
    Verificação > se o sistema funciona
---

