# **ASP Net (.NET Framework)**
## **Model Binding**
> Tags para facilitar o pegar dados provenientes do usuario por uma requisição Get,Post, ...

### - [**Documentação**](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-3.1)

---

## **WCF** Windows Communication Foundation
- **Instalar** Componentes individuais > Windows Communication Foundation
- **Criar** Novo projeto do tipo, "Aplicativo Web ASP .NET (.NET Framework)"
- **Dao** Objeto responsavel pelo retorno do serviço, nele criamos e passamos o formato da resposta.
``` c#
[DataContract]
public class Cliente
{
    [DataMember]
    public string Nome { get;set; }

    [DataMember]
    public string Cpf { get; set; }
}
```
- **Interface**
```c#
[ServiceContract]
public interface IClienteService
{

    [OperationContract]
    void Add(Cliente c);

    [OperationContract]
    Cliente Buscar(string nome);
}
```
---
## **MVC**
> Model, View and Controller
### **Servidor**
> Nós instanciamos uma aplicação WEB atraves da implementação do IWebHost (Microsoft.AspNetCore) e vamos ver como funciona seu  Request Pipeline (Fluxo que uma requisição HTTP).
- **Program.cs**, que faz a hospedagem da aplicacao
``` C#
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```
- **Startup.cs**, que toma as acoes necessarias para direcionar o usuario quando faz uma requisiçao

``` c#
public class Startup
    {
        // Esse metodo adiciona as configuracoes iniciais necessarias para o programa responder a requisicao
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllersWithViews();
        }

        // Esse metodo direciona o usuario com base na requisicao
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            else
            {
                app.UseExceptionHandler("/Home/Error");
                app.UseHsts();
            }

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllerRoute(
                    name: "default",
                    pattern: "{controller=Home}/{action=Index}/{id?}");
            });
        }
    }
```

- **Resposta** Com metodo WriteAsync
``` c#
public class Startup
{
    // Aqui configura todas as respostas que a aplicacao, todas elas passam por aq
    public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        app.Run(RESPOSTA);//Direcionamos o inicio da aplicação
    }
    public Task RESPOSTA(HttpContext context)
    {
        return context.Response.WriteAsync("Ola Mundo!");//Escrevemos no navegador implementando "WriteAsync"
    }
}
```
- **Idenficando caminho da URL** Com metodo Request, pegando o caminho passado na URL
``` c#
public class Startup
{
    public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        app.Run(ROTEAMENTO);//Direcionamos o inicio da aplicação
    }
    public Task ROTEAMENTO(HttpContext context)
    {
        return context.Response.WriteAsync(context.Request.Path);//Escrevemos o caminho passado na URL no navegador implementando "WriteAsync"
    }
}
``` 

- **Properties**
> No arquivo launchSettings.json podemo configurar informacoes sobre o inicio da aplicacao, como porta, o servidor

- **Roteamento** Com RouteBuilder, identifica um caminho na URL e direciona um Metodo
``` c#
public class Startup
{
    // Metodo necessario para aplicar a chamada "app.UseRouter(rotas);" usada no Configure que inicia a aplicação
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddRouting();
    }

    public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        var routeBuilder = new RouteBuilder(app);
        routeBuilder.MapRoute("CAMINHO/CAMINHO", METODO);// Entre aspas passamos o caminho esperado na URL e ele vai identificar se foi ele foi utilizado
        routeBuilder.MapRoute("CAMINHO2/CAMINHO2", OUTROMETODO);
        var rotas = routeBuilder.Build();

        app.UseRouter(rotas); 
    }
}
```
- **Roteamento com Template** Com RouteBuilder, identifica um caminho na URL , direciona um Metodo e define  variaveis na URL
``` c#
public class Startup
{
    // Metodo necessario para aplicar a chamada "app.UseRouter(rotas);" usada no Configure que inicia a aplicação
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddRouting();
    }

    public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        var routeBuilder = new RouteBuilder(app);
        routeBuilder.MapRoute("CAMINHO_ESPERADO/{VARIAVEL1}/{VARIAVEL2}", METODO);// Caminho esperado e atribuimos aqui o nome das variaveis para as posições de Roteamento que vamos usar

        app.UseRouter(rotas); 
    }
}

private Task METODO(HttpContext context)
{
    CLASSE c = new CLASSE
    {
        Var1 = Convert.ToString(context.GetRouteValue("VARIAVEL1")),
        Var2 = Convert.ToString(context.GetRouteValue("VARIAVEL2")),
    };
    return context.Response.WriteAsync("Leitura efetuada com sucesso!");
}
```
- **StatusCode** Status de resposta do servidor
``` c#
public class Startup
{
    public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        app.Run(StatusERRO);//Direcionamos o inicio da aplicação
    }
    public Task StatusERRO(HttpContext context)
    {        
        context.Response.StatusCode = 404;
        return context.Response.WriteAsync(ERRO);
    }
}
```
- **Route Constraints** Definimos o tipo de variavel que vamos receber pela URL 
``` c#
public void Configure(IApplicationBuilder app) //Recebemos o inicio da aplicação
    {
        var routeBuilder = new RouteBuilder(app);
        routeBuilder.MapRoute("CAMINHO_ESPERADO/{VARIAVEL1:int}/{VARIAVEL2:string}", METODO);// Aqui definimos o tipo de varaivel

        app.UseRouter(rotas); 
    }
```
- **Desenhando a tela** Podemos desenhar a tela com WriteAsync, so chamar o METODO com a rota (URL), correta
``` c#
private Task METODO(HttpContext context)
{
    var html = @"<html>
    <form>
        <input />
        <input />
        <button>Gravar</button>
    </form>
    </html>";
    return context.Response.WriteAsync(html);
} 
```

- **Implementando o ASP .Net MVC**
``` c#
Install-Package Microsoft.AspNetCore.Mvc -Version 2.0.2

// No Startup
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
}

public void Configure(IApplicationBuilder app)
{
    app.UseMvcWithDefaultRoute();
}
```
- **Implementando o ASP .Net MVC**
    - Botao direito no projeto:
        - Editar NOME.csproj:
            - Adiciona dentro de PropertyGroup:
```c#
 <PreserveCompilationContext>true</PreserveCompilationContext>
```

- **Habilitando Stack Error, USE APENAS PARA DESENVOLVER NAO PUBLICA ESSA OPCAO HABILITADA**

```C#
public void Configure(IApplicationBuilder app)
{
    // parametro
    app.UseDeveloperExceptionPage();
    // parametro
    app.UseMvcWithDefaultRoute();
}
```

### **View**
> Responsavel por conter o HTML/CSS da pagina, ou seja seu conteudo que é visualizado pelo usuário
- **Identificar/Receber objetos do controller**
``` c#
// No Controller
public IActionResult Index()
{
    return View(CLASS.GETLIST());
}

// Na view
@model List<CLASS>;
@foreach (var item in CLASS)
{
    //codigo
}
```
- **_ViewImports**
    - Importa as classes que serao utilizadas pelas views
    
- **_ViewStart**
    - Define variaveis globais para toda a aplicação

- **Link**
```c#
@html.ActionLink("Mensagem", "Metodo", "NomeDoController")
```
### **Razor**
> É uma sintaxe de programação ASP.NET usada para criar páginas da web dinâmicas com as linguagens de programação C #.

- **Obervação** para usarmos objetos diferentes do que recebemos na referencia do @modal temos que atribuir eles no _ViewImports

#### **Aplicações**
- **C# .NET**

    Podemos adicionar codigo c# ou usar tags do .NET  atribuindo o '@' e o parametro do codigo, lembrando que dentro de um bloco de execução podemos adicionar tags HTML ou codigo C# (com o @)

- **@Html**

    Podemos gerar eventos com o '@Html.' isso facilita bastante tratar as telas [**Documentação**](https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.html?view=aspnet-mvc-5.2)

    - **Action** Chama um metodo do mesmo ou de outro Controller

    - **ActionLink** Podemos criar um link no HTML para retornar o metodo do mesmo ou de outro Controller

    
- **Texto no bloco de execução** dentro de um bloco como 'Foreach' por exemplo para adicionar um texto temos que usar '@:TEXTO' para o Razor entender que não tem que executar aquele trexo.

- **@RenderBody()**

    A partir dessa tag definimos o lugar que o Razor vai atribuir o codigo das Views que herdam do Layout. Na View temos que definir o local onde criamos o Layout que ela vai usar.

- **@Html.Partial("_NOME")**

    Assim atribuimos uma Partial View ao cshtml na hora de criar o front

    Melhor usar um Metodo ActionResult que retorna a View

#### **Views Parciais**
> Normalmente são criadas com o nome _NOME.cshtml e ficam na pasta Shared se forem genericas. Caso contrario criamos na pasta referente aquela View

- **Criando**, recebe html normalmente na hora de criar

- **Chamando**

    @Html.Partial("_NOME")

#### **Bundle Juntando referencias**
> Podemos juntar referencias para carregar apenas um arquivo como juntar CSS e Bootstrap ou diferentes repositorios Jquery. Dentro do **BundleConfig.cs** no metodo RegisterBundles

- **Criando**
```c#
StyleBundle estilos =  new StyleBundle("~/bundles/estilos");
estilos.include("~/Content/bootstrap/css/bootstrap.css");
estilos.include("~/Content/Style.css");
bundles.add(estilos);
```

- **Chamando CSS**
``` c#
@Styles.Render("~/bundles/estilos")
``` 

- **Chamando JS**
``` c#
@section Scripts{
    @Scripts.Render("~/bundles/scripts")
}
``` 
---


### **Controller**
> BackEnd da pagina responsavel por tratar os dados (ou seja atende as requisiçoes), nesse exemplo utilizamos o controller apenas como meio para conectar o WCF e a pagina WEB

``` C#
// Redirect para pagina
public ActionResult Index()
{
    return View("NomeView");
}

// Retornar a pagina mas sem redirecionar, comum na abertura de popups
public PartialViewResult GetModalNome()
{
    return PartialView("_Nome"); // o _Nome seria a view
}

// Recebe um Objeto Dto e devolve uma lista de obj json sem valor max
public JsonResult ListaNome(NomeDto dto)
{
    var lista = NomeProxy.ListaNome(dto);
    return new JsonResult()
    {
        Data = new
        {
            lista
        },
        JsonRequestBehavior = JsonRequestBehavior.AllowGet,
        MaxJsonLength = int.MaxValue
    };
}

// Recebe um Dto e devolve um objeto json
public JsonResult Excluir(int Id)
{
    return Json(NomeProxy.Excluir(Id) NomeProxy.ListaModal(), JsonRequestBehavior.AllowGet);
}

// Metodo padrão
public ActionResult NOME()
{
    return RedirectToAction("Action/Metodo", "NOMEdoController(Sem o Controller so o nome)");
}
```

- **ViewBag & ViewData**
> Podemos transitar dados do controller para o form atraves dela, lembrando que o nome que atribuimos e muito importante pois diferencia elas, para retornarmos ela para o controller temos que salvar o dado quando ele chega no form _(html)_ e buscar pelo nome ou Id dentro do controller 

**ViewData**
```c#
//Criando na Controller
ViewData["Title"] = "MyPag";

//Usando na View
@ViewData["Title"]

```

**ViewBag**
``` c#
//Atribuindo no controller o ViewBag
ViewBag.Operacao = "I";

//Salvando em um campo dentro do HTML o valor
<input type="hidden" name="Operacao" value="@ViewBag.Operacao" />

///Validando a ViewBag no form
@if (ViewBag.Operacao == "I")
{
   //codigo
}

//Pegando o dado de volta no controller e salvando em uma NOVA ViewBag pq a primeira morreu no final da criacao do form
ViewBag.Operacao = Operacao; //Operacao e o nome que demos no HTML
```

- **SelectListItem**
> Objeto do asp para criar um drop de maneira agil 

- **Injecao de dependencia**
    - Adicionas as propriedades necessarias no construtor do controller e elas serao adicionadas na chamada... lembre-se de adicionar as variaveis dentro da classe e apenas preencher elas com o contrutor

- **Rout** Atributo que define como acessar aquele metodo dentro do controller pela url
    - **Criar** para funcionar precisamos editar o arquivo:
        - **RouteConfig.cs**
``` c#
// Adiciona como primeira linha do metodo RegisterRoutes
routes.MapMvcAttributeRoutes();
```
``` c#
[Route("NOME")]
public ActionResult NOME()
{
    // Codigo
}

// Pegando variaveis pelo Route
// A URL ficaria www.SITE.com/Controller/NOMEVAR ... ou seja nao teria o query string, mas funciona como se fosse outra chamada de metodo
[Route("NOME/{NOMEVAR}")]
public ActionResult NOME(string NOMEVAR)
{
    // Codigo
}
```

- **Autorização**
``` c#
// Criar
public class AutorizacaoFilterAttribute : ActionFilterAttribute
{
    public override void OnActionExecuting(ActionExecutingContext filterContext)
    {
        object usuario = filterContext.HttpContext.Session["usuario"]; // busca na sessao o usuario
        if (usuario == null) // se nao encontra vai na tela abaixo 
        {
            filterContext.Result = new RedirectToRouteResult(
                new RouteValueDictionary(
                    new
                    {
                        controller = "Login",
                        action = "Index"
                    }));
        }
    }
}

```
``` c#
// Usando por Metodo(Action)
[AutorizacaoFilter]
public ActionResult Index()
{
    // Codigo
}
```
``` c#
// Atribuindo de forma Global
// Adiciona a referencia no FilterConfig, lembrando que le tem que estar referenciado no GlobalAsex
filters.Add(new AutorizacaoFilterAttribute());
// Adiciona referencia na base do controller
[AutorizacaoFilter]
public class NOMEController : Controller
{
    // Actions
}
```

### **Model**
> Responsavel pela regra de negocio, podemos atribuir informacoes na hr de criar o obj para poder retornar mensagens de validacao e tornar os campos obrigatorios
``` c#
// Atributos das variaveis do banco (entity) obriga essa variavel a:
[Required] //  vir preenchida da View no form
[StringLenght(10)] // ter no max 10 caracters
public int Nome {get;set;}

// Usando no Controoler seus atributos
public ActionResult Salvar(CLASSE c)
{
    if (ModelState.IsValid) // Valida os atributos do model
    //codigo
}

// Mensagem no HTML
<label>...
<input>...
@Html.ValidationMessage("Atenção este campo e obrigatorio!")
```

- **NOMEViewModel**
    - DTO do mvc criado no model e usado para passar informacoes para tela
- **Sem Mapeamento**
    - Podemos usar o LINQ com INCLUDE E INCLUDETHEN para salvar no banco os objetos referenciados 

### **Solucoes**
- [**SolucoesWEB**](https://github.com/luizgustavo77/Notes/blob/master/Developer/FullStack/Solu%C3%A7%C3%B5esWEB.md)

---
## **WCF & MVC**

**NAO PASSA
MOS ENTITYDADE PARA TELA SO DTO**

### **WEB** file
 > Nele adicionamos as camadas do MVC juntos das ferramentas WEB como o javascript, html, ...

### **WCF** file
> Camada de negocio onde trabalhamos as variaveis (entity), interface, classe, conecao com o banco (data.interface / data.nhibernate), dal, bll, injecao

### **Common** 
> Dentro de common adicionamos classe para criar as variaveis necessarias nos metodos e elas vao transitar entre o WCF e o WEB

### **ORDEM INICIO APP WEB**
1. Controller: Incia aplicacao por padrao pelo Index
2. View: Tras a pagina com html, css...
3. Controller: o html chama uma API pelo controller e ele repassa
4. Model: aqui tratamos os dados 
5. Controller: devolve oque o view pediu
6. View: exibe oque recebeu do controller
``` html
<a onclick="Evento();" id="Unico" href="~/Controller">Link</a>
```
-    - Esse "Controller" dentro de "href" aponta para um cshtml dentro do "View" "**_return View("NOME");_** " aqui temos o nome do arquivo cshtml sem precisar da extensao
7. Javascript: faz a chamada para o controller dos metodos criados no WCF      

### **WCF.Business.Entity**
- **BusinessDto/Schema**
> Salvamos as tabelas presentes no banco que usamos, As **_foreign key_** devem ser criadas em outra _Entity_ para serem instancidas, Primeira letra maiuscula, adiciona o _{ get; set; }_ e adicionar _**virtual**_ para funcionar com as transacoes WEB
``` c#
public class Usuario
    {
        // primary key
        public virtual int? Id { get; set; }
        public virtual string PassUsuario { get; set; }
        public virtual string LoginUsuario { get; set; }
        // foreign key
        public virtual Pessoa.Pessoa Pessoa { get; set; }
    }
/// Salvar uma nova pessoa
Usuario retorno = new Usuario();
retorno.Pessoa = new Pessoa.Pessoa() {
	Id = dto.Pessoa// salvamos apenas o ID mas poderiamos ter salvo qual quer coisa
};
```
### **WCF.DataInterface**
> Atribuimos os metodos do Entity que vao rodar no banco.  
- **Acesslayer/SCHEMA**
> Camada de acesso de dados (faz as coneccoes com o banco), ja recebe as variaveis criadas no Entity mapeadas pelo NHibernete
``` c#
public interface IUsuarioDal : IDalHelper<Usuario>
    {
        Usuario PesquisarPorId(int id);
    }
```
### **WCF.NHibernate**
 - **AcessLayer/SCHEMA**
 > Aqui criamos o Dal que ira fazer as buscas dentro do Banco mais tarde quando instanciarmos ele no Bussiness
``` c#
public class UsuarioDal : DalHelper<Usuario>, IUsuarioDal
{
        public Business.Entity.Acesso.Usuario PesquisarPorId(int id)
        {
            return Pesquisar().Where(p => p.Id.Value.Equals(id)).FirstOrDefault();// p
        }
}
```
- **Maps/SCHEMA**  
> Aqui apresentamos para o **Entity** para nossas tabelas no banco
**ATENCAO:** Quando fazemos referencia de outra tabela como lista nao podemos usar o LIST mas sim o **ILIST**

``` c#
// EX: Maps
using FluentNHibernate.Mapping;

 public class UsuarioMap : ClassMap<Usuario>
 {
    public UsuarioMap()
    {
        this.Schema("acesso"); //nome do schema

        this.Table("Usuario"); //nome da tabela

        this.Id(x => x.Id)//primary key
            .Column("Id_Usuario")//coluna
            .GeneratedBy 
            .Sequence("SeqUsuario");// sequences

        this.References(x => x.Pessoa) //usado para foreign key
            .Column("Id_Pessoa")
            .Not
            .Nullable();

        this.Map(x => x.LoginUsuario) //mapeia uma coluna
            .Column("Login_Usuario")
            .Length(255)
            .Not
            .Nullable();
	    
	this.HasMany(x => x.ListaPerfil)
	    .Cascade
	    .AllDeleteOrphan()
	    .Inverse()
	    .KeyColumn("Funcionalidade");
    }
}
```

### **WCF.BusinessInterface**
- **SCHEMA** 
> Aqui adicionamos os metodos que vao tratar os dados (REGRA DE NEGOCIO)
```c#
public interface IUsuarioBll
    {
        IList<UsuarioListaDto> Pesquisar(UsuarioPesquisaDto dtoPesquisa);
    }
```

### **WCF.Business**
- **SCHEMA** 
> Aqui adicionamos os metodos que vao tratar os dados (REGRA DE NEGOCIO)
```c#
public class UsuarioBll : IUsuarioBll
    {
        [Inject]
        public IUsuarioDal UsuarioDal { get; set; }

        public IList<UsuarioListaDto> Pesquisar(UsuarioPesquisaDto dtoPesquisa)
        {
            IList<UsuarioListaDto> retorno = new List<UsuarioListaDto>();
            // CODIGO

            return retorno;
        }
    }
```
**IQueryable**
> Cria um sql sem executar podendo referenciar ao Entity como _class_ e usar os metodos do **DalHelper**
``` c#
IQueryable<Usuario> query = this.UsuarioDal.Pesquisar();
```

### **WCF.ServicesInjecaoDependencia**
- **Modules/Business:** 
> Adicionamos os dal
```C#
    public class AcessoBusinessModule : NinjectModule
    {
        public override void Load()
        {
            Bind<IUsuarioDal>().To<UsuarioDal>();
            Bind<IDalHelper<Usuario>>().To<DalHelper<Usuario>>();
        }
    }
```
-  **Modules/WCF:**
> Adicionamos os bll
``` C#
public class AcessoServiceModule : NinjectModule
    {
        public override void Load()
        {
            Bind<IUsuarioBll>().To<UsuarioBll>();
        }
    }
```
- **InfraestrutureSetup** 
> Aqui adicionamos no Ninject os atalhos para os _"DAL"_ 
``` c#
public class InfrastructureSetup
    {
        public static void RegisterServices(StandardKernel kernel)
        {
            // WCF
            kernel.Load<AcessoServiceModule>();        
            
            // Bussiness
            kernel.Load<AcessoBusinessModule>();    
        }
    }
```

### **WCF.Services:**
- **SCHEMA**
> Aqui adicionamos a chamada dos Objetos da camada de negocio 

***lEMBRE-SE QUE PARA ADICIONAR O WCF SERVICE TEMOS QUE COMENTAR O _ninject_ DENTRO DO  Web.config DO Services***

- **Criando:** Com o mause adicionamos o **"WCF Service"**

```c#
// Interface
[ServiceContract]
	public interface INomeService
	{
        [OperationContract]
        Metodo; // so adicionar um metodo aq ex:IList<Usuario> PesquisarUsuarioLogin(UsuarioPesquisaDto dto);
 }
```
``` c#
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerCall)]
[NHibernateContext]
public class NomeService : INomeService
{
    [Inject]
    public INomeBll NomeBll { get; set; }

    public IList<Usuario> PesquisarUsuarioLogin(UsuarioPesquisaDto dto)
    {
        return this.UsuarioBll.PesquisarUsuarioLogin(dto);
    }
}
```
### **WEB.Reference**  
> Primeiro adicionamos o caminho dos metods com o _mause_ podemos adicionar o service reference (**WCF**)

### **WEB.Proxy**
- **Caminho:** SCHEMA
- **Reference:** SCHEMA.DescricaoService
> Aqui herdamos os metodos da BLL, orbigatorio adicionar o static para nao instanciar

```c#
public static UsuarioCadastroDto PesquisarId(int dtoPesquisaId)
        {
            UsuarioCadastroDto retorno = new UsuarioCadastroDto();
            UsuarioServiceClient client = null;

            try
            {
                client = new UsuarioServiceClient();
                retorno = client.PesquisarId(dtoPesquisaId);
            }
            finally
            {
                if (client.State == System.ServiceModel.CommunicationState.Faulted)
                {
                    client.Abort();
                }
                else
                {
                    client.Close();
                }
            }

            return retorno;
        }
```
- **Proxy/app.config >> Web/web.config**: entramos no app.config e copiamos o cliente/endpoint e depois adicionamos no web.config dentro de client
``` c#
// Proxy/app.config
...
<endpoint address="http://localhost:8080/Acesso/UsuarioService.svc"
                binding="basicHttpBinding" bindingConfiguration="basicHttp"
                contract="Acesso.UsuarioService.IUsuarioService" name="BasicHttpBinding_IUsuarioService" />
...
```
```C#
// WEB/web.config
...
<endpoint address="http://localhost:8080/Acesso/UsuarioService.svc"  behaviorConfiguration="infoBehavior" binding="basicHttpBinding" bindingConfiguration="basicHttp" contract="Acesso.UsuarioService.IUsuarioService" name="BasicHttpBinding_IUsuarioService" />
...
```
### **WEB.Pages.Controllers** 
- **Controllers/SCHEMA/NomeController.cs**
> Aqui criamos os metodos que vao ser usados pelo front
```c#
public JsonResult Pesquisar(UsuarioPesquisaDto dtoPesquisa)
        {
            IList<UsuarioListaDto> dto = UsuarioProxy.Pesquisar(dtoPesquisa);
            return new JsonResult()
            {
                Data = new
                {
                    dto
                },
                JsonRequestBehavior = JsonRequestBehavior.AllowGet,
                MaxJsonLength = int.MaxValue
            };
        }
```

### **WEB.Pages.Views**
- **Caminho front:** Views/Nome/Tela.cshtml
- **Caminho javascript:** Script/adicional/schema/nome.js
> o front (cshtml) chama um javascript que por sua vez acessa o _Controller_ para enviar os dados por **Ajax** e depois receber eles tratados
```html
<!-- Adiciona o caminho do javascript para executar-->
<script src="~/Scripts/adicional/acesso/usuario.js"></script>
```
``` html
<!-- Usei um botao para exemplificar como iriamos chamar o metodo   -->
<div class="div-botao">
    <button type="button" class="btn btn-primary" onclick="usuario.pesquisar(); return false;">Pesquisar</button>
</div>
```
``` javascript
var pesquisar = function () {
    $.ajax({
                type: "POST",
                url: base_path + "Usuario/Pesquisar", //caminho do controller
                data: { // dados
                    'dtoPesquisa': getFiltros() //outro metodo que usa os id do html para apontar os inputs com dados
                },
                cache: false,
                complete: function (XMLHttpRequest, textStatus) {
                }
            }).done(function (data) {
                // adiciona function para mostrar os dados ou devolver um popup com o ok
            }).fail(function (XMLHttpRequest, textStatus, errorThrown) {
                // adiciona function que devolve um popup com o erro
            });
}
```

### **WCF.Business.Dto**

- **Caminho:** BusinessDto/Schema
-  **DTO:** data transfere object
>Camada onde criamos as variaveis para cada metodo da Bll com base no que vai receber da WEB, Primeira letra maiuscula e adiciona o _{ get; set; }_

``` c#
public class UsuarioListaDto
    {
        public int Id { get; set; }
        public string LoginUsuario { get; set; }
        public string NomePessoa { get; set; }
    }
```
--- 
## **Variaveis de Sessão**

### **Session**
> Variavel que normalmente guarda informações da pagina aberta para agilizar processor ou personalizar o conteudo. **Como funciona?** salva um estado, variavel ou objeto enquanto o navegador estiver aberto.

- **Com o .Net WebForms** 
``` c#
Session["FirstName"] = firstName;   
  
firstName = (string)(Session["FirstName"]); 
```

- **Sem o .Net WebForms** 
``` C#
HttpContext context = HttpContext.Current;  
context.Session["FirstName"] = firstName;  
firstName = (string)(context.Session["FirstName"]);  
```

### **Coockie**
> Variavel que normalmente referencia uma sessão entre o usuario e o servidor com no máximo 4 KB separados por ponto e vírgula e salva no lado do usuario. **Como funciona?** Quando um navegador solicita uma página da Web de um servidor, os cookies pertencentes à página são adicionados à solicitação. Dessa forma, o servidor obtém os dados necessários para "lembrar" as informações sobre os usuários.
- **Create**
``` javascript
function setCookie(cname, cvalue, exdays) {
  var d = new Date();
  d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
  var expires = "expires="+d.toUTCString();
  document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
}
```
- **Get**
``` javascript
function getCookie(cname) {
  var name = cname + "=";
  var ca = document.cookie.split(';');
  for(var i = 0; i < ca.length; i++) {
    var c = ca[i];
    while (c.charAt(0) == ' ') {
      c = c.substring(1);
    }
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length);
    }
  }
  return "";
}
``` 
- **Check**
``` javascript
function checkCookie() {
  var user = getCookie("username");
  if (user != "") {
    alert("Welcome again " + user);
  } else {
    user = prompt("Please enter your name:", "");
    if (user != "" && user != null) {
      setCookie("username", user, 365);
    }
  }
}
```
- **Delete**
> Basta definir o parâmetro expires para uma data passada
``` javascript
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```

### **View State**
> Variavel que normalmente guarda informações da pagina aberta para agilizar processor ou personalizar o conteudo. **Como funciona?** salva um estado, variavel ou objeto enquanto nâo trocar de pagina.

- **Salvar**
```c#
 ViewState["Nome"] = Nome;
```
- **Ler**
```C#
Nome = ViewState["Nome"].ToString();
```

### **QueryString**
> Podemos atribuir variaveis na URL e chama-las no nosso codigo
``` c#
// Exemplo de URL
"https://URL?VARIAVEL=VALOR"

// Chamando
string VARIAVEL = Request.QueryString["VARIAVEL"])
```

---
## **WebConfig**
- **AppSettings**
> Podemos salvar variaveis como string no WebConfig para não ter que abrir o codigo fonte na hora de editar alguma coneccao.

``` c#
// Chamando no Codigo
string SENHA = ConfigurationManager.AppSettings["NOME"];

// Atribuindo no WebConfig
  </system.serviceModel>// Essa tag e padrão do WebConfig e colocamos o "appSettings" com as variaveis que quisermos dentro
  <appSettings>
    <add key="NOME" value="SENHA"/>
  </appSettings>
</configuration>// Essa tag por padrão fecha o WebConfig
```
---


### **Resources File**
- [**ResourcesFile**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/ResourcesFile.md)

---

## **Solucoes**
- [**SolucoesWEB**](https://github.com/luizgustavo77/Notes/blob/master/Developer/FullStack/Solu%C3%A7%C3%B5esWEB.md)
