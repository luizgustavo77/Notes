# **ASP NET Framework & ASP NET Core**
## **Model Binding**
> Tags para facilitar o pegar dados provenientes do usuario por uma requisição Get,Post, ...

### - [**Documentação**](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-3.1)

---

## **Servidor** Default no Core e nas novas versões do Framework
>Configuração Statup e Program para gerenciar as requisições

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
---
## **MVC**
> Model, View and Controller

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
- **_ViewImports** Core
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

### **Bundle**, Framework
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

--- 

## **Variaveis de Sessão**

### **Session**
> Variavel que normalmente guarda informações da pagina aberta para agilizar processor ou personalizar o conteudo. **Como funciona?** salva um estado, variavel ou objeto enquanto o navegador estiver aberto.

- **Framework** 
``` c#
Session["FirstName"] = firstName;   
  
firstName = (string)(Session["FirstName"]); 
```

- **Core** 
``` C#
HttpContext context = HttpContext.Current;  
context.Session["FirstName"] = firstName;  
firstName = (string)(context.Session["FirstName"]);  
```

### **Coockie**
> Guarda informações sobre o usuario como sites que acessa, IP, etc...

### **Cache**
> Informações sobre a pagina da internet que você está acessando

- **Exemplo**
``` c#
public class Cache
{
    //private static ObjectCache cache = MemoryCache.Default;
    private static System.Web.Caching.Cache cache = System.Web.HttpContext.Current.Cache;

    public static void Adicionar(string nomeCache, object item, int qtdHoras)
    {
        //cache.Set(nomeCache, item, DateTimeOffset.Now.AddHours(qtdHoras));
        cache.Insert(nomeCache, item, null, System.Web.Caching.Cache.NoAbsoluteExpiration, new TimeSpan(qtdHoras, 0, 0));
    }

    public static void Adicionar(string nomeCache, object item)
    {
        //cache.Set(nomeCache, item, DateTimeOffset.Now.AddDays(1));
        cache.Insert(nomeCache, item, null, System.Web.Caching.Cache.NoAbsoluteExpiration, new TimeSpan(1, 0, 0, 0));
    }

    public static T Obter<T>(string nomeCache)
    {
        return (T)cache.Get(nomeCache);
    }

    public static void Remover(string nomeCache)
    {
        cache.Remove(nomeCache);
    }
}
```

### **View State** Obsoleto
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
## **WebConfig** Framwork
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

### **Solucoes**
- [**SolucoesWEB**](https://github.com/luizgustavo77/Notes/blob/master/Developer/FullStack/Solu%C3%A7%C3%B5esWEB.md)


### **Resources File**
- [**ResourcesFile**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/ResourcesFile.md)

### **WCF** Framework
- [**WCF&MVC**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/C%23/WCF%26MVC.md)
