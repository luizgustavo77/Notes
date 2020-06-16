# **SalesForce**
### **Noções básicas da Salesforce Platform**
- **Chatter** Permite que várias pessoas comentem e colaborem em um registro específico.

- **Arquitetura**
    - **Multilocação** significa apenas que você está compartilhando recursos dos servidores
    - **Metadados** objeto Propriedade e todos os seus campos como layouts de página, configurações de segurança e quaisquer outras personalizações feitas.
    -  **API** possibilitam que diferentes softwares fiquem conectados e troquem informações entre si

- **AppExchange** Lojas de aplicativos
    - **Armazenamento** Os aplicativos são instalados com o que chamamos de pacote. Para encontrar o pacote:
    1. Em Configuração, pesquise e selecione Pacotes instalados na caixa Busca rápida.
    2. Clique no nome do pacote instalado. É o mesmo nome da página de download do AppExchange.
    3. Clique em Exibir componentes para saber mais sobre o pacote. A página de detalhes do pacote mostra todos os componentes, inclusive campos personalizados, objetos personalizados e classes do Apex no pacote. Essa informação ajuda a determinar se existem conflitos nas suas próprias personalizações.
---

### **Trailhead Playground**
> Um Trailhead Playground é uma organização que pode ser usada para concluir desafios práticos e experimentar novos recursos e personalizações, nós pode ter até 10 , isso significa escrever componentes web do Lightning e criar novos objetos personalizados. Se você nos perguntar, isso é tão divertido quanto o outro playground!

- **Aplicativo**, programas pagos e gratis para facilitar ou melhorar nossas aplicacoes

- **Pacotes** permitem carregar dados de exemplo, campos e objetos personalizados ou qualquer outra coisa
---
### **Usuarios**

- **Nome de usuário** Cada usuário deve ter um nome de usuário que seja único em todas as organizações do Salesforce (e não apenas na sua).
Formato do nome de usuário: Os usuários devem ter um nome de usuário no formato de um endereço de email (ou seja, jdoe@domain.com), mas não precisam usar um endereço de email real. (Podem usar seu endereço de email, se desejarem, desde que esse endereço de email seja único em todas as organizações do Salesforce.)
- **Email** Os usuários podem ter o mesmo endereço de email em todas as organizações.
- **Senhas** Os usuários devem alterar sua senha na primeira vez que fizerem login.
- **Link de login** Os usuários só podem usar uma vez o link de login enviado no email de inscrição. Se um usuário clicar no link e não definir uma senha, você (o administrador) terá que redefinir a senha para que ele possa efetuar login.

- **Licenças de usuário** Uma licença de usuário determina quais recursos o usuário pode acessar no Salesforce. Por exemplo, você pode conceder acesso aos usuários para recursos padrão do Salesforce e Chatter com a licença padrão do Salesforce. Contudo, se você quer conceder acesso aos usuários para recursos do Salesforce apenas, é preciso ter várias licenças que permitam essa escolha. Por exemplo, se você precisa conceder acesso a um usuário para o Chatter sem permitir que ele veja qualquer dado no Salesforce, você pode fornecer a ele uma licença gratuita do Chatter.

- **Perfis** determinam o que os usuários podem fazer no Salesforce. Eles vêm com uma série de permissões que concedem acesso para objetos, campos, guias e registros específicos. Cada usuário pode ter apenas um perfil. 

- **Papéis** determinam o que os usuários podem ver no Salesforce com base em sua localização na hierarquia de papéis. Os usuários no topo da hierarquia podem ver todos os dados dos usuários abaixo deles.

- **Adicionar usuários**

    - **1.** Em Configuração, insira Usuários na caixa Busca rápida e selecione Usuários.

    - **2.** Novo usuário para adicionar um único usuário ou em Adicionar vários usuários para adicionar até 10 usuários de uma vez.

    - **3.** Insira o nome e o endereço de email de cada usuário e um nome de usuário exclusivo na forma de um endereço de email. Por padrão, o nome de usuário é igual ao endereço de email, mas é possível alterar isso.

    - **4.** Selecione a licença de usuário que você deseja associar aos usuários criados.

    - **5.** Selecione um perfil.

    - **6.** Selecione Gerar senhas e notificar o usuário via email para enviar um nome de login e uma senha temporária para cada novo usuário.

    - **7.** Clique em Salvar.

- **Congelar** Acesse a página de perfil do usuário em risco, toque e selecione Congelar.
---
### **Niveis de acesso** 
> O Salesforce inclui controles de segurança de configuração simples através dos quais é possível especificar facilmente quais usuários podem visualizar, criar, editar ou excluir um registro ou campo no aplicativo. É possível configurar o acesso no nível da organização, dos objetos, dos campos ou dos registros individuais.

- **Organização** No nível mais alto, você pode garantir acesso a sua organização mantendo uma lista de usuários autorizados, configurando políticas de senha e limitando o acesso por login a certos horários e locais.
- **Objetos** A segurança em nível de objeto oferece a maneira mais simples de controlar quais usuários têm acesso a quais dados. Configurando permissões para um tipo particular de objeto, você pode impedir que um grupo de usuários crie, visualize, edite ou exclua quaisquer registros daquele objeto. Por exemplo, você pode usar permissões de objeto para garantir que entrevistadores possam visualizar vagas e formulários de emprego, mas não editá-los ou excluí-los.
- **Campos** Você pode usar a segurança em nível de campo para restringir o acesso a certos campos, mesmo para objetos aos quais um usuário tem acesso. Por exemplo, você pode tornar o campo Salário em um objeto Posição invisível para os entrevistadores, mas visível para os gerentes de contratação e recrutadores.
- **Registros** Para controlar os dados com maior precisão, você pode permitir que determinados usuários visualizem um objeto, mas restringir os registros individuais do objeto que eles podem visualizar. Por exemplo, o acesso em nível de registro permite que os entrevistadores vejam e editem suas próprias avaliações, sem expor as avaliações de outros entrevistadores. Você pode gerenciar o acesso em nível de registro das seguintes maneiras.
    - Os **padrões para toda a organização** especificam o nível padrão de acesso que os usuários têm aos registros uns dos outros. Você pode usar as configurações de compartilhamento de toda a organização para bloquear seus dados no nível mais restrito e, em seguida, usar as outras ferramentas de compartilhamento para fornecer acesso seletivamente a outros usuários. Por exemplo, você pode dar a todos os funcionários acesso a um objeto chamado Candidato, para permitir que qualquer pessoa adicione um candidato ao banco de dados. Mas você pode restringir o acesso a Posições, de modo que qualquer pessoa possa ver as vagas disponíveis, mas apenas os funcionários com as permissões apropriadas possam editá-las.
    - As **Hierarquias de papéis** permitem que aqueles mais acima na hierarquia de papéis herdem o acesso a todos os registros de propriedade de usuários abaixo deles na hierarquia. As hierarquias de papéis não precisam corresponder exatamente ao organograma. Em vez disso, cada papel na hierarquia representa um nível de acesso a dados de que um usuário ou grupo de usuários precisa. Por exemplo, você pode restringir o acesso a Candidatos, definindo o padrão para toda a organização como Privado, mas permitir que os recrutadores vejam e editem os registros de candidatos dos quais são proprietários. Os recrutadores não podem ver os registros de candidatos dos quais não são proprietários, pois todos os recrutadores estão no mesmo nível na hierarquia de papéis. No entanto, gerentes de contratação podem receber acesso de leitura/gravação a todos os registros de candidatos, pois estão em um nível mais alto na hierarquia de papéis do que os recrutadores.
    - As **Regras de compartilhamento** permitem que você crie exceções automáticas aos padrões para toda a organização para determinados grupos de usuários, a fim de dar a eles acesso aos registros que eles não possuem ou que normalmente não poderiam ver. As regras de compartilhamento, assim como as hierarquias de papéis, só são usadas para dar acesso aos registros a mais usuários e nunca poderão ser mais rígidas do que as configurações padrão de toda a organização. Por exemplo, você pode permitir que todos os funcionários vejam Posições, mas usar regras de compartilhamento para conceder acesso de edição completo a funcionários em um papel ou grupo chamado Gerentes de contratação.
    - O **compartilhamento manual** permite que os proprietários de registros específicos os compartilhem com outros usuários. Embora o compartilhamento manual não seja automatizado, como as configurações de compartilhamento para toda a organização, as hierarquias de papéis ou as regras de compartilhamento, ele pode ser útil em algumas situações, por exemplo, se um recrutador que for entrar de férias precisar ceder temporariamente a propriedade de um formulário de emprego a outro funcionário.

---
### **Dashboard**
- Objetos, tabelas
    - Criamos colunas (variaveis) e ele ja monta telas de CRUD
    - OBS: Marca a opcao _"Iniciar o assistente da nova guia personalizada após salvar este objeto personalizado"_
- TAB, telas 
    - Adicionamos ao Aplicativo, nele podemos trazer objetos, sites, etc...
- Aplicativo, App Manager
    - Ambiente onde reunimos informacoes usando de TAB (chamadas de itens tambem)


---

### **Modelagem de dados**

- **Objetos padrão** são aqueles objetos que vêm incluídos no Salesforce. Objetos comerciais comuns, como Conta, Contato, Lead e Oportunidade, são todos objetos padrão.

- **Objetos personalizados** são objetos criados para armazenar informações específicas da sua empresa ou indústria.

- **Relacionamentos de objeto**
    - **Pesquisa** vincula dois objetos para que você possa “pesquisar” um dos objetos nos itens relacionados do outro objeto. Os objetos nos relacionamentos de pesquisa funcionam como objetos independentes e têm suas guias próprias na interface de usuário.

    - **Mestre e detalhes** O objeto mestre controla determinados comportamentos do objeto detalhe, por exemplo, quem pode ver os dados do detalhe. No relacionamento entre mestre e detalhes, o objeto detalhe não funciona independentemente, na verdade, se um registro do objeto mestre é excluído, todos os registros de detalhe relacionados são também excluídos.

- **Schema Builder** Mapeia a relacao entre os objetos, aqui tambem podemos criar objetos e relacionamentos

---
### **Gerenciamento de dados**
- **Importação**
    - **Assistente de importação de dados** Com esta ferramenta, acessível por meio do menu Configuração, você pode importar dados em objetos padrão comuns, tais como contatos, leads, contas, bem como dados em objetos personalizados. É possível importar até 50.000 registros por vez. Oferece uma interface simples para especificar os parâmetros de configuração, fontes de dados, e mapeamentos de campo que mapeiam os nomes de campo em seu arquivo de importação com os nomes de campo no Salesforce.

    - **Data Loader** Aplicativo cliente que pode importar até cinco milhões de registros por vez, de qualquer tipo de dados, a partir de arquivos ou de uma conexão de banco de dados. Pode ser operado pela interface de usuário ou pela linha de comando. Neste último caso, é preciso especificar fontes de dados, mapeamentos de campo e outros parâmetros por meio de arquivos de configuração. Isso possibilita automatizar o processo de importação, usando chamadas de API.

- **Exportação**
    - **Assistente de exportação de dados** é um assistente no navegador, que pode ser acessado pelo menu Configuração. Permite exportar dados manualmente uma vez a cada sete dias (para exportação semanal) ou a cada 29 dias (para exportação mensal). Você também pode exportar dados automaticamente, em intervalos semanais ou mensais. Na Professional Edition e na Developer Edition, você pode gerar arquivos de backup somente a cada 29 dias, ou automaticamente apenas em intervalos mensais.

    - **Data Loader** aplicativo cliente que você deve instalar separadamente. Pode ser operado pela interface de usuário ou pela linha de comando. Essa última opção é útil para situações em que você deseja automatizar o processo de exportação ou utilizar APIs para integração com outro sistema.

- **Change Data Capture** você pode receber alterações de registros do Salesforce em tempo real e sincronizar os registros correspondentes em um armazenamento de dados externo. Gera eventos de alteração para todos os objetos personalizados definidos em sua organização do Salesforce e um subconjunto de objetos padrão.

- **Jetterbit Cloud Data Loader** Ferramenta para gestão de dados 100% Free [Dowload](blob:https://web.whatsapp.com/e17feddd-d64e-4e5f-ad14-109e77f8300b)
    - **Operation**
        - **Query** - Consulta
        - **Upsert** - Atualiza se existir ou insere se nao existir
        - **Insert** - Insere o dado 
        - **Update** - Atualiza o dado 
        - **Delete** - Apaga o dado
        - **Bulk Process** - Processos em massa

    - **login:** Conta da Salesforce    
    - **Object:** Selecione o aplicativo que vai usar
    - **Source:** Origem dos dados
    - **Schedule & Options:** Criação de rotinas personalizadas para atualizar os dados
    - **Map:** Mapear as referencias 

---
### **Personalização do Lightning Experience**

- **Oque e?** Um aplicativo é uma coleção de itens que funcionam em conjunto para servir a um propósito específico. No Lightning Experience, os aplicativos Lightning dão aos usuários acesso a conjuntos de objetos, guias e outros itens, tudo em um mesmo pacote prático na barra de navegação.

- **O que você pode colocar em um aplicativo Lightning?**
    - A maioria dos objetos padrão, incluindo a página inicial, o feed principal do Chatter, Grupos e Pessoas.
    - Os objetos personalizados da sua organização
    - Guias do Visualforce
    - Guias de componentes do Lightning
    - Guias de Aplicativos de tela usando o Visualforce
    - Guias da Web

-  **Visivel** Os aplicativos que não têm uma marca de seleção na coluna Visível estão ativos somente na interface do usuário do Salesforce Classic. Os aplicativos marcados como visíveis podem ser usados sem restrições no Lightning Experience

- **App Manager** Aqui podemos criar os aplicativos e gerenciar os existentes 

- **Layouts Compactos** Controlam quais campos seus usuários veem no painel de destaques e no cartão de pesquisa expandida. Confuguramos por Objeto

- **Layouts de página** As páginas do Lightning são um conjunto de componentes do Lightning arrumados nas áreas de uma página que configuramos por objeto. O editor de layout de página permite:
    - Controlar os campos, listas de registros relacionados e links personalizados que os usuários podem ver
    - Personalizar a ordem em que os campos aparecem nos detalhes da página
    - Definir se os campos são visíveis, somente leitura ou obrigatórios
    - Controlar quais botões personalizados e padrão aparecem nos registros e nas listas relacionadas
    - Controlar as ações rápidas que aparecem na página

- **Dashboards** Objeto padrao, nele podemos criar visualizacoes com base nos relatorios que criamos

- **Ações**
    - **Ações específicas de objeto** Têm relacionamentos automáticos com outros registros e permitem aos usuários rapidamente criar ou atualizar registros, registrar chamadas, enviar emails e mais, no contexto de um objeto em particular. 
    - **Ações globais** São criadas em um local diferente daquele em que são criadas ações específicas de objeto. Elas se chamam ações globais porque podem ser colocadas em qualquer lugar em que haja suporte para ações.
---
### **Relatórios**
> Objeto padrao do SalesForce

---
### **Desenvolvimento**
Você já sabe que é possível usar a Salesforce Platform para desenvolver objetos personalizados e funcionalidades específicas para sua empresa.
