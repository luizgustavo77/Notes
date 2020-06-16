# **QlikSense**
> Tanto o QlikView quanto o QlikSense funcionam bem como ferramentas de BI, mas o QlikSense funciona como um Self-Service BI que seria uma forma de dividir as responsabilidades entre o Usuario e o setor de TI.

- **Responsabilidades:**
    - **TI:** Transformacao de dados e qualidade da informacao
    - **Usuario:** Constroem as analises

### **Dados**
> Podemos carregar os dados mas as relacoes devem ser criadas dentro da aplicacao, por mais que ela tenha uma IA que da sugestoes das relacoes a serem criadas.

- **Nomes das colunas:** Após carregar os dados podemos alterar os nomes das colunas pela ferramenta, tornando mais claro oque cada uma carrega

- **Visao:** Podemos remover o campo da Analise, assim nao é possivel usar ele para gerar as visualizacoes

### **Aplicativos**
> Sao espacos que contem dentro deles a base de dados, dentro do aplicativos construimos pastas e nelas ficam os dashboards que fazem toda a demonstracao dos dados. Os filtros sao gerados automaticamente pelo nome das colunas.
> Os aplicativos ficam salvos como QVF e podemos exportar e importar eles

- **Campos:**
    - Tabelas carregadas nos dados

- **Itens Mestre**
    - **Dimensoes:** Sao definicoes que valem para toda a aplicacao
        - **Unico:** Apenas um valor
        - **Hierarquia:** Podemos abrir mas informacoes ao clicar em um dado 
    - **Medidas:** Cria regras simples(calculos) e a linguagem é parecida com a usada no excel

- **Graficos** 
    - Adiciona visualizacao e depois inserimos as medidas
    - Podemos configurar o Grafico ao clicar nele editando: Dados, Classificacao, Complementos, Aparencia.

- Objetos Personalizados

### **Historias**
> Podmeos gerar apresentacoes com as informacoes do Qlik Sense

- **Snapshot:** Podemos copiar uma visualizacao como um print e adicionar um comentario para adicionar na hora de gerar uma apresentacao
