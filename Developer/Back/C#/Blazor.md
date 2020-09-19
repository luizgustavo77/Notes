# **Web Assembly**
> Enquanto arquivos .js tem 5 (parse, compila, otimiza, executa, GC), etapas para serem compilador pelo navegador o .wasm tem 3 (Decodifica, Compila/Otimiza, Executa) tornando-o mais rapido.

**SignalIR** - conexao que trata comunicacao em tempo real

---

## **Material Design**
> Framework da Google para Design Front-End que tenta trazer as caracteristicas do mundo real para as formas do front.

- **Aplicando**
> Podemos baixar ou referenciar no HTML (Lembre-se que todas as paginas devem receber a referencia)

```html
<!--Carrega os icones-->
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
<!--Por padrão podemos importar as classes com um padrão de cores primarias e secundarias, para customizar https://getmdl.io/customize/index.html-->
<link rel="stylesheet" href="https://code.getmdl.io/1.3.0/material.indigo-pink.min.css">
<!-- Carrega os arquivos js -->
<script defer src="https://code.getmdl.io/1.3.0/material.min.js"></script>
```

---

## **MatBlazor**
> Framework que une o Blazor ao Material Design

- [**Documentação**](https://www.matblazor.com/)
---

## **Blazor**
> Possibilita usar C# para trabalhar os elementos da pagina, só esta disponivel na versão 3.1 ou maior do ASP NET Core

- **Desvantagem**

    Baixar todas as DLL do .net

###  **Blazor WerbAssembly VS Blazor Server**

|Caracteristica|Blazor WerbAssembly (cliente)|Blazor Server (servidor)|
|---|---|---|
|Utiliza c#|X|X|
|Dowload rapido de arquivos|Precisa baixar as Dll|X|
|Trabalha bem com dispositivos lentos|Todo codigo carrena no dispositivo|X|
|Maior velocidade de execução|X|Maior latencia|
|Serveless|X|Precisa de servidor|
|Não depende do ASP NET CORE|X|Precisa do ASP .NET CORE|
|Nao depende do WebAssembly|Precisa de WebAssembly|X|
|Maior escabilidade|X|Prejudicada, servidor gerencia muita coisa|
|Pode ser servidor CDN|X|Precisa de um servidor|

---
## **Blazor Server App VS Blazor WebAssembly APP**
> Ambos sao projetos blazor, mas o framework oferece essas duas opcoes. Voltadas para projetos monoliticos


- **Blazor Server App**, Client-Side

    Apenas arquivos staticos e codigos C#, podemos fazer requisicoes WEB API

    - **Data** Funciona como Model e Controller
    - **Pages/_Host.cshtml** Inicia o projeto 
    - **Appsettings.json** Tem configuracoes da requisicao    
    - **Program.cs** Define a utilizacao do Startup e o HostBuilder

    - **Startup.cs** 
        - Precisamos adicionar no ConfigureServices:
    
            **"services.AddServerSideBlazor();"** para adicionar o Blazor

            **"services.AddSingleton<NOMEService>();"** adicionamos os servicos (ou controllers) 

        - Configure nos UseEndepoints tem dois valores importantes:

            **"MapBlazorHub();"** Define as configuracoes do SignalIR

            **"MapFallbackToPage("/_Host")";** Define pagina que o programa vai iniciar

    - **_Host** Define o App.razor 
    - **App.razor** Define o roteamento para as paginas

- **Blazor WebAssembly**, Server-Side (Client-Side + .Net Core)

    Faz o cliente-side e chama as API de um ASP NET Core

    - **wwwroot/index.html** Inicia o projeto 
    - **Program.cs** Define a utilizacao do arquivo raiz App.razor

---
## **Blazor WebAssembly APP + Progressive Web Application**
> Para paginas simples o projeto iniciasem uma opção para tratar dados. Somente telas.

- **wwwroot/index.html** Inicia o projeto 
- **Program.cs** Define a utilizacao do arquivo raiz App.razor

---

## **Blazor WebAssembly App + ASP.NET Core hosted**
> Modelo pronto para Microservicos

- **Instalando o Template usando o Developer Command Prompt**
    - dotnet new --install Microsoft.AspNetCore.Blazor.Templates::3.1.0-preview4.19579.2

### **Client**
> Aqui temos a aplicação Blazor e as paginas com Razor
- **Arquitetura**    
    - **Properties/launchSettings.json** Define configurações sobre como vai trabalhar
    - **wwwroot**
        - **css** arquivos de css
        - **index.html** Inicia o projeto 
    - **Pages** Paginas Razor
    - **Shared** Paginas comuns do site
    - **_Imports.razor** Tem os namespaces comuns do projeto
    - **App.razor** Configura as rotas solicitadas pela URL
    - **Program.cs** Define a utilizacao do arquivo raiz App.razor

### **Server**
> Aqui criamos as WEB API's e conectamos a Base de dados 
- **Dependencias**, para usar banco de dados e code first
    - Microsoft.EntityFrameworkCore.SqlServer
    - Microsoft.EntityFrameworkCore.Tools

- **Arquitetura**
    - **dbContext** adicionamos a conexão com o banco. Use Entity Framework
    - **Models/NOME** entidades que espelham oque temos no banco. Use Entity Framework
    - **Services/NOME** criamos o tratamento de dados com as bll
    - **Controllers** aqui vamos expor nossa aplicação
    - **Properties/launchSettings.json** Define configurações sobre como vai trabalhar
    - **appsettings.json** adicionamos a string de conexao

- **Migrations**
    - **Default project** NOME.Server

- **Adicionar configurações abaixo**
``` c#
// No appsettings.json
  . . .
  "ConnectionStrings": {
    "DefaultConnection": "CONEXAO"
  }
}

// No Startup
public class Startup
{
    public IConfiguration Configuration { get; }
    public Startup(IConfiguration configuration)
    {
        this.Configuration = configuration;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.addDBContext<dbContext>(options => 
        options.UseSqlServer(configuration.GetConnectionString("DefaultConnection")));
```

### **Shared**
> É um mediador que tem codigos compartilhados com Client e Server
- **Arquitetura**
    - **ModelsDTO/NOME** Criamos os DTO's e componentes comuns como disparo de EMail

---

## **Paginas padrão de projetos Blazor**


- **_Host.cshtml / index.html** Dentro dele temo um script que habilita o SignalIR  no blazor "< script src="_framework/blazor.webassebly.js"></script>" e ponta e carrega o App.razor

- **App.razor** Configura as rotas solicitadas pela URL

- **MainLayout.razor** Define o layout da pagina e nele adicionamos outras paginas

- **NavMenu.razor** Aqui criamos o menu da aplicação com seus itens e o MainLayout carrega ele

- **_Imports.razor** Tem os namespaces comuns do projeto
---
## **Diretivas**
> Determina a pagina vai ser compilada, e devem ser adicionados no inicio da pagina

- **@page** Define qa rota de requisições do browser. 

- **@Body** Define o local onde vamos renderizar as paginas que chegam dentro do MainLayout

- **@Code {}** Aqui dentro podemos declarar variaveis, metodos, classes..

- **@using** Utilizada para importar um namespace.

- **@inject** Essa diretiva serve para injetarmos serviços no nosso componente. 

- **@layout** Especifica qual o Layout que será utilizado para renderizar o componente.

- **@implements** Usado para implementar um inherits.

- **@inherits** Usado para ser herdado de outro componente

- **@typeparam** Serve para definir um Tipo Genérico para o Componente.

- **@functions** É utilizada para incluir um bloco de código C# dentro do componente. 

---
## **Diretivas de atributos**
> Tags blazor que atribuem as ferramentas do blazor nos atributos HTML

- **@bind** Cria o Two-Way databind

- **@on(EVENTO)** Adiciona um tratamento para o evento

- **@ref** Captura uma referencia para o componente

- **@atributes** Renderiza um dicionario de atributos


---
## **First Loading**
> Assim que você abre a pagina no seu navegador esse evento dispara, é bom trabalhar bem ele pois se for o primeiro acesso pode levar alguns segundos

- **Como atribuir**
   - No seu index tem uma tag chamada "<app><app>" que por padrão vem escrito "Loading. . .", podemos trocar o texto por um gif ou outro elemento para deixar essa espera mais bonita

---
## **Razor SZ Blazor**
> Razor no Blazor e diferente do ASP NET, la sao usadas apenas na View e gera o NOME.cshtml, no blazor geramos um NOME.razor, é executado no navegador e a pagina se atualiza dinamicamente sem voltar ao servidor.

- Chamando Razor
    - **@**
    - ***@( . . . )***

### **Exemplos de codigo**

``` html
<!-- Para ver o log abra no Chrome: Web Developer > Console do Navegador-->
<button @onclick="@(()=> Console.WriteLine("log do console"))">
```

``` c#
// Tudo no HTML
@page '/LG'

<h1>20 + 10 = @Calculo.Somar(20, 10) </h1>
<h1>20 - 10 = @Calculo.Subtrair(20, 10)</h1>

@code{
    public class Calculo
    {
        public static int Somar (int n1, int n2) => n1+n2;
        public static int Subtrair (int n1, int n2) => n1-n2;
    }
}
```

``` c#
// Criamos uma classe e metodos em outro lugar
public class Calculo
{
    public static int Somar (int n1, int n2) => n1+n2;
    public static int Subtrair (int n1, int n2) => n1-n2;
}

// Adicionamos com o using aqui ou no _Imports.razor
@page '/LG'
@using NAMESPACE.PASTA

<h1>20 + 10 = @Calculo.Somar(20, 10) </h1>
<h1>20 - 10 = @Calculo.Subtrair(20, 10)</h1>

@code{

}
```
---
## **Parameter**
- **Chamando Pagina Razor**
   - **Instanciar**, Podemos instanciar/referenciar uma pagina NOME.razor para mostrar na tela
   - **Parametros**, passamos parametros que devem ser passados na chamada da pagina 

``` HTML
<!-- Instanciar pagina razor -->
< NOME />

<!-- Parametros -->
<!-- Adiciona o parametro na pagina razor -->
@code {
    [Parameter]
    public string Msg { get; set; }
}
<!-- Instanciar pagina razor -->
< NOME Msg="Carregando" />


```

---
## **DataBinding**
> Estabelece um canal de sincronização entre variavel e elemento HTML ou componente

### - **One-Way**, dados unidirecional
   - **Como funciona?**
      - Evento ou Ação do usuario > Atualiza valor > Renderiza
   - **Usando**
``` c#
<h1>@Msg</h1>

@code {
    private string Msg { get; set; } = "Ola Mundo";
}
```

### - **Two-Way**, dados bidirecional
   - **Como funciona?**
      - Podemos passar uma variavel/Objeto como parametro que vai ser atualizada em tempo real quando o valor mudar
   - **Usando**
``` blazor
<!-- O campo texto joga a entraga da titulo -->

<h1>@Msg</h1>
<input @bind="Msg">

@code {
    private string Msg { get; set; } = "Ola Mundo";
}
```
### **Bind & Bind-Value**
> Diferença entre os dois

- **Bind**

    Por padrão atualiza o valor da variavel em tempo real, ou seja mudou no campo muda no blazor

- **Bind-Value**

    Passamos para ele o evento que vai acionar essa alteração, por padrão é o input e funciona da mesma forma que o Bind

``` c#
// Nesse evento usamos os dois para mostrar que como herdam do mesmo objeto podemos apenas sobrescrever o Bind para adicionar
<input @bind="@CurrentValue" 
       @bind-value:event="oninput" />
```
---
## **Eventos**
### **EventCallBack**
> Podemos chamar metodos de outra pagina. Acionar metodos do Pai na chamada do Filho para que o filho possar executar o metodo do Pai como se fosse uma herança

- **Pagina Pai**
``` c#
// Nome dessa pagina é PAI

<FILHO METODO="METODOPAI" />

@code {
    public void METODOPAI()
    {
        // codigo
    }
}
```

- **Pagina Filho**
```c#
// Nome dessa pagina é FILHO

<button @click"@(() => METODO.InvokeAsync())"> </button>

@code {
    // Adicionamos o evento aqui para ter uma referencia que quando criarmos o filho temos que passar esse metodo
    [Parameter]
    public EventCallback<CLASSE> METODO {get; set;}
```
### **Argumentos**
- [**Documento**](https://docs.microsoft.com/pt-br/aspnet/core/blazor/components/event-handling)

---

## **RenderFragment & ChildContent**
> Permite adicionar dados, elementos, atributos e conteudo.

- **Pagina Filho**, está que deve ser instanciada
``` c#
// Nome da pagina é FILHO

// Adiciona o conteudo aqui
@ChildContent1

@ChildContent2

@code {
    [Parameter]
    public RenderFragment ChildContent1 {get;set;}
    
    [Parameter]
    public RenderFragment ChildContent2 {get;set;}
}
```

- **Pagina Pai**
``` c#
<FILHO> 
    <childcontent1> <h1> OLA, EU ESTOU APARECENDO NA PAGINA FILHO </h1> </childcontent1>

    <childcontent2> <h1> EU TAMBEM, MAS LOGO ABAIXO </h1> </childcontent2>
</FILHO>
```
---
## **CascadingValue**
> Podemos passar um valor para diversas paginas no Blazor com o CascadingValue, e fica a disposição na pagina usar ou não.

- **Passando valor:**
``` c#
. . .
    <div class="content px-4">
    // Assim todos elementos que entrarem no @Body podem ter acesso a classe "config"
        <CascadingValue Value="@config" >
                @Body
        </CascadingValue>
    </div>
</div>

@code{
    Config config = new Config();
}
```
- **Acessando o valor:**
``` c#
. . . 
<p>Current value: @config.value</p>

@code{
    [CascadingParameter] Config config { get; set; }
}

```
---
## **Ref**
> Podemos instanciar um objeto da pagina e passar ele como parametro na hr de montar essa pagina, isso permite trabalharmos os metodos que essa pagina tem na pagina pai

- **Adicionando o @ref no Pai**
``` c#
. . .
// Esse botton vai chamar um metodo no Filho
<button class="btn btn-primary" @onclick="filho.Exibir">Mostra filho</button>

// Aqui informamos que ao intanciar essa pagina vamos referencia o objeto "FILHO filho" que criamos abaixo
<FILHO @ref="filho" />

@code{
// tendo esse objeto aqui podemos chamar os metodos e variaveis publicos criados nessa interface
    FILHO filho;
. . .
```

- **Criando essa referencia no Filho**
``` c#
. . . 

@if(ExibirPagina)
{
    . . . // html que queremos exibir
}

@code {
    public bool ExibirPagina { get; set; } = false;
    public void Exibir() => ExibirPagina = true;

    . . .
```
---
## **Helpers HTTPClient Json**
> Metodos para fazer requisições no padrão REST e retornar os em Json.

- GetJsonAsync())
- PostJsonAsync
- PutJsonAsync
- DeleteAsync, esse ultimo não faz parte mas ele fecha os requisitos para ser um REST

---
## **Formulario** EditForm
> Formulario no blazor usando componente **EditForm** que possui o parametro **Model** que valida a entrada

- **Tipos de submissão**
    - **OnSubmit**

        Quando envia para o servidor

    - **OnValidSubmit**

        Quando posta um formulario valido

    - **OnInvalidSubmit**

        Quando posta um formulario invalido

### **Criando**
- **Models**
```c#
public class Usuario
{
    public int Id { get; set; }

    [Required(ErrorMessage ="O nome deve ser informado")]
    [StringLength(10,ErrorMessage ="O nome não pode exceder 10 caracteres")]
    public string Nome { get; set; }

    [Required(ErrorMessage = "O email deve ser informado")]
    [EmailAddress(ErrorMessage ="Formato do email é inválido")]
    public string Email { get; set; }

    [Range(18,80,ErrorMessage ="A idade deve estar entre 18 e 80")]
    public int Idade { get; set; }
}
```

- **Page**
    - **DataAnnotationsValidator** Atribui a validação criada no objeto
    - **ValidationSummary** Mostra as mensagens de validação na tela

``` html
@page "/formulario"

<h1>Meu primeiro formulário Blazor</h1>

<EditForm Model="@usuario"  OnInvalidSubmit="@Send">
    <!-- Atribuindo validação -->
    <DataAnnotationsValidator />
     <ValidationSummary/>

    <div class="form-group">
        <label form="nome">Nome</label>
        <InputText id="nome" @bind-Value="usuario.Nome" class="form-control" />
    </div>
    <div class="form-group">
        <label form="email">Email</label>
        <InputText id="email" @bind-Value="usuario.Email"  class="form-control"/>
    </div>
    <div class="form-group">
        <label form="idade">Idade</label>
        <InputNumber id="idade" @bind-Value="usuario.Idade"  class="form-control"/>
    </div>
        <input type="submit" value="Enviar Formulário" class="btn-primary" />
</EditForm>

@code {
    Usuario usuario = new Usuario();

    protected void Send()
    {

    }
}

```
---
## **Ciclo de vida dos Componentes**
> Metodos especias que podemos sobrescrever para capturar o ciclo de vida do componente

- **On OnInitializedAsync**, evento que roda ao terminar de carregar a pagina de forma Async
   - protected override async Task OnInitializedAsync(){}

- **OnParametersSetAsync**, evento quando recebemos os parametros do Pai

- **OnAfterRenderAsync**, evento de termino da renderização do componente

- **IDisposable**, desconstrução do componente

---
## **Tempo de vida de um serviço**
> Existem 3 formas de vincular o tempo de vida de um serviço, seja um objeto, metodo ou variavel.

- **Scoped:** Esse objeto está presente em todas as paginas

- **Singleton:** Esse objeto está presente em todas as paginas

- **Transient:** Esse objeto pode ser requisitado e sempre ira iniciar um novo objeto desse tipo

- **Criando:** Para definirmos esses comportamentos temos que adicionar no **Startup** do projeto a chamada para o objeto e na chamada definimos o tipo de instancia que desejamos criar.

``` c#
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddSingleton<CLASSESingleton>();
        services.AddScoped<CLASSEScoped>();
        services.AddTransient<CLASSETransient>();
    }
. . .
```
---
## **LocalStorage && SessionStorage**
> Salvando dados no lado do cliente

### **Local Storage** chave e valor
> Fica salvo enquanto o cliente via codigo ou o navegador não limpar os dados. Usamos o pacote Blazored.LocalStorage

- **Usando**
``` c#
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Adiciona referencia do serviço no Statup
        services.AddBlazoredLocalStorage();
    }
. . .
```

``` c#
@page "/"
// Adicionando a referencia
@inject Blazored.LocalStorage.ILocalStorageService localStore

@code{
    string value = "";
    protected override async Task OnInitializedAsync()
    {
        // Pegando um valor a partir da chave
        value = await localStore.GetItemAsync<string>("Chave");
    }

    public async void AtualizaLocalStorage()
    {
        // Atualiza ou adiciona um LocalStorage
        await localStore.SetItemAsync(notaKey, minhasNotasPessoais);
    }

    public async void LimpaLocalStorage()
    {
        // Limpa todo o LocalStorage
        await localStore.ClearAsync();
    }
. . .
```

### **Session Storage**
> É apagado assim que a sessão é fechada expirada


---
## **Rotas**
> Na diretiva "@page" podemos adicionar outras rotas que retornam a mesma pagina e tambem receber variaveis por ela.

- **NotFound**
    - No "App.razor" podemos definir a pagina que sera mostrada quando não existir rota dentro de **"< NotFound>"**

- **Sobrecarga do endereço**

``` c#
@page "/page"
@page "/pagina"
@page "/pag"
```

- **Query String** não é case sensitive mas deve ter o mesmo nome de parametro e no @page
    - Para chamar o exemplo abaixo ficaria ". . ./pag/10" assim passamos o valor de 10 para variavel
    - Somente o ". . ./pag" não encontra essa pagina para isso precisamos definir essa entrada no @page
``` c#
@page "/pag/{valor:int}"

@code {
    [Parameter]
    public int Valor {get;set;}
}
```

- **NavLink** redirecionamos para uma pagina e o elemento no html permanece selecionado, usado para adicionar links no menu
    - **@NavLinkMatch.All>** Determina que quandoa URL for exatamente igual a no "href" esse item vai ficar selecionado
``` html
<div class="@NavMenuCssClass" @onclick="ToggleNavMenu">
    <ul class="nav flex-column">
        <li class="nav-item px-3">
            <NavLink class="nav-link" href="" Match="NavLinkMatch.All">
                <span class="oi oi-home" aria-hidden="true"></span> Home
            </NavLink>
        </li>
        <li class="nav-item px-3">
            <NavLink class="nav-link" href="counter" Match=@NavLinkMatch.All>
                <span class="oi oi-plus" aria-hidden="true"></span>Counter
            </NavLink>
            <ul class="nav flex-column">
                <li class="nav-item px-3">
                    <NavLink class="nav-link" href="counter/1" Match=@NavLinkMatch.All>
                        <span class="oi oi-plus" aria-hidden="true"></span>Counter/1
                    </NavLink>
                </li>
            </ul>
        </li>
    </ul>
</div>
```

- **NavigationManager** biblioteca que nos auxilia a manusear a url da aplicação.

``` c#
. . .
@inject NavigationManager navigation

. . . 

@code {
    public void Navegar1()
    {
        // redirecionar para pagina externa
        navigation.NavigateTo("http://www.google.com");
    }

    public void Navegar2()
    {
        // redirecionar para pagina da aplicação
        navigation.NavigateTo("/counter");
    }

    public void ValorUri()
    {
        // pega url inteira da pagina atual
        navigation.Uri.ToString();
    }
    public void ValorBaseUri()
    {
        // pega somente a base para a pagina atual
        navigation.BaseUri.ToString();
    }
}
```

---
## **Code-Behind**
> Quando temos a interface e o comportamento linkados mas não necessariamente na mesma pagina, isso facilita na manutanção e uso futuro póis separamos as responsabilidades .

- **Interface:** aqui vamos criar a visualização e refereciar o comportamento
``` html
<!-- Nome dessa pagina e Contador.razor -->

@page "/minhapagina"
<!-- Assim adicionamos a referencia para o comportamento -->
@inherits ContadorBase

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button class="btn btn-primary" 
        @onclick="IncrementCount">Click me</button>
```

- **Comportamento:** aqui vamos adicionar a tratativa de dados 
``` c#
// Nome da pagina é Contador.razor.cs

// O nome da classe fica NOMEBase e herda da diretva "ComponentBase"
public class ContadorBase : ComponentBase
{
    // Variaveis tem que tera proteção "protected" ou "public" para serem vista na interface
    protected int currentCount = 0;
    
    protected void IncrementCount()
    {
        currentCount++;
    }
}
```
---

## **Debug**
### **No Chrome**
- Terminal de desenvolvedor
    - Source > file//
        - Pages > PAGINA QUE ESTA O CODIGO
            - Adiciona o breakpoint

### **No VS2019** a partir da versão 3.2 do blazor
> Funciona normalmente no **Blazor WebAssembly APP** com a opção **ASP.NET Core hosted** marcada.

---

## **Metodos**
> Algumas dicas de como trabalhar com metodos e os principais metodos

- **Como chamar metodos dentro do evento HTML**
   - < button @onclick="MeuMetodo">Botao</ button>

- **Chamando API/Arquivo**, aqui recupera um arquivo dentro de "wwwroot" e converte para uma lista de CLASSE
   - @inject HttpClient http
   - await http.GetJsonAsync<List< CLASSE>>("arquivo.json");

---

## **JavaScript SZ Blazor**
> Chamando Js no Blazor

- **Criando o Arquivo:**
    - Cria o arquivo js no wwwroot
    - Definir funções usando o escopo window
    - Referenciar o arquivo no Index.html/_Host.html
``` js
// Criando o arquivo no wwwroot
window.FUNÇÃO_NO_JS = (message) => {
    alert(message);
}
```

- **Referencia:**
```html
<!-- Referenciando no Index.html -->
<!DOCTYPE html>
<html>
<head>
    . . .
    <!-- Adicionando o arquivo.js -->
    <script src="JSFunctions.js"></script>
</head>
<body>
    <app>Loading. . .</app>
    <script src="_framework/blazor.webassembly.js"></script>
</body>
```
``` c#
// Adicionando a referencia para o Js na Pagina.razor
@inject IJSRuntime js
. . .
```

- **Usando:**
```c#
await js.InvokeAsync<object>("FUNÇÃO_NO_JS", "ARGUMENTOS");
await js.InvokeVoidAsync("FUNÇÃO_NO_JS", "ARGUMENTOS");
var resultado = ((IJSInProcessRuntime)js).Invoke<bool>("FUNÇÃO_NO_JS", "ARGUMENTOS");
```

--- 

## **Exemplos**
> Códigos prontos para reutilizar

- **Popup** Usando bootstrap

``` c#
// Criando
@if (ExibirConfirmacao)
{
    <div class="modal-backdrop show"></div>

    <div class="modal" tabindex="-1" role="dialog"
         aria-hidden="true" style="display:block;">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">@Titulo</h5>
                    <button @onclick="onCancela" type="button" class="close"
                            data-dismiss="modal" aria-label="Fechar">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    @ChildContent
                </div>
                <div class="modal-footer">
                    <button @onclick="onCancela" type="button" class="btn btn-secondary"
                            data-dismiss="modal">
                        Cancelar
                    </button>
                    <button @onclick="onConfirma" type="button"
                            class="btn btn-primary">
                        OK
                    </button>
                </div>
            </div>
        </div>
    </div>
}

@code {

    [Parameter] public bool ExibirConfirmacao { get; set; } = false;
    [Parameter] public string Titulo { get; set; };    
    [Parameter] public RenderFragment ChildContent { get; set; }
    [Parameter] public EventCallback onConfirma { get; set; }
    [Parameter] public EventCallback onCancela { get; set; }

    public void Exibir() => ExibirConfirmacao = true;
    public void Ocultar() => ExibirConfirmacao = false;
}

// Usando
<a class="btn btn-danger" @onclick="@(()=> AbrirPopup())">Abrir Popup </a>

<Confirma @ref="confirma" onCancela="@CancelaConfirma" onConfirma="@SalvarConfirma">
    <div> OQUE EU QUISER DENTRO DO POPUP </div>
</Confirma>

@code {

    Confirma confirma;

    void AbrirPopup(int categoriaId)
    {
        confirma.Exibir();
    }

    async Task SalvarConfirma()
    {
        confirma.Ocultar();
    }

    void CancelaConfirma()
    {
        confirma.Ocultar();
    }
}
```

- **Paginação** Usando bootstrap. Podemos definir a quantidade de itens que um metodo vai retornar e carregar os proximos depois
``` c#
// Dentro de Shared/Recursos
public class Paginacao
{
    public int Pagina { get; set; } = 1;
    public int QuantidadePorPagina { get; set; } = 5;
}

// Dentro de Server/Utils
public static class QueryableExtensions
{
    public static IQueryable<T> Paginar<T>(this IQueryable<T> queryable, Paginacao paginacao)
    {
        return queryable
            .Skip((paginacao.Pagina - 1) * paginacao.QuantidadePorPagina)
            .Take(paginacao.QuantidadePorPagina);
    }
}

public static class HttpContextExtensions
{
    public async static Task InserirParametroEmPageResponse<T>(this HttpContext context,
        IQueryable<T> queryable, int quantidadeTotalRegistrosAExibir)
    {
        if (context == null)
        {
            throw new ArgumentNullException(nameof(context));
        }

        double quantidadeRegistrosTotal = await queryable.CountAsync();
        double totalPaginas = Math.Ceiling(quantidadeRegistrosTotal / quantidadeTotalRegistrosAExibir);

        //salvando as informações no header do response
        context.Response.Headers.Add("quantidadeRegistrosTotal", quantidadeRegistrosTotal.ToString());
        context.Response.Headers.Add("totalPaginas", totalPaginas.ToString());
    }
}

// Dentro do Server
[HttpGet]
public async Task<ActionResult<List<CLASSE>>> Get([FromQuery] Paginacao paginacao)
{
    var queryable = context.CLASSESs.AsQueryable();
    
    await HttpContext.InserirParametroEmPageResponse(queryable, paginacao.QuantidadePorPagina);
    
    return await queryable.Paginar(paginacao).ToListAsync();
}

// Dentro do Cliente
// Shared
@code {

    [Parameter] public int paginaAtual { get; set; } = 1;
    [Parameter] public int QuantidadeTotalPaginas { get; set; }
    [Parameter] public int Raio { get; set; } = 3;
    [Parameter] public EventCallback<int> PaginaSelecionada  { get; set; }

    List<LinkModel> links;

    class LinkModel
    {
        public LinkModel(int page) : this(page, true)
        { }

        public LinkModel(int page, bool enabled) : this(page, enabled, page.ToString())
        { }

        public LinkModel(int page, bool enabled, string text)
        {
            Page = page;
            Enabled = enabled;
            Text = text;
        }

        public string Text { get; set; }
        public int Page { get; set; }
        public bool Enabled { get; set; } = true;
        public bool Active { get; set; } = false;
    }

    protected override void OnParametersSet()
    {
        CarregaPaginas();
    }


    private void CarregaPaginas()
    {
        links = new List<LinkModel>();

        //tratar o link da pagina anterior
        var isLinkPaginaAnteriorHabilitado = paginaAtual != 1;
        var paginaAnterior = paginaAtual - 1;

        links.Add(new LinkModel(paginaAnterior, isLinkPaginaAnteriorHabilitado, "Anterior"));

        //trata os links das paginas especificas
        for(int i=1; i<= QuantidadeTotalPaginas; i++)
        {
            if (i >= paginaAtual - Raio && i <= paginaAtual + Raio)
            {
                links.Add(new LinkModel(i)
                {
                    Active = paginaAtual == i
                });
            }
        }

        //trata o link para a proxima pagina
         var isLinkProximaPaginaHabilitado = paginaAtual != QuantidadeTotalPaginas;
        var proximaPagina = paginaAtual + 1;

        links.Add(new LinkModel(proximaPagina, isLinkProximaPaginaHabilitado, "Próximo"));
    }
}
// Pages
<hr />

<Paginacao  QuantidadeTotalPaginas="QuantidadeTotalPaginas" paginaAtual="paginaAtual"
           Raio="2" PaginaSelecionada="PaginaSelecionada">
</Paginacao>


@code {

    List<CLASSE> CLASSEs { get; set; }

    private int QuantidadeTotalPaginas;
    private int paginaAtual = 1;

    protected override async Task OnInitializedAsync()
    {
        await CarregaCLASSEs();
    }

    private async Task PaginaSelecionada(int pagina)
    {
        paginaAtual = pagina;
        await CarregaCLASSEs(pagina);
    }

    async Task CarregaCLASSEs(int pagina=1, int quantidadePorPagina= 5)
    {

        var httpResponse =
            await http.GetAsync($"api/CLASSE?pagina={pagina}&quantidadePorPagina={quantidadePorPagina}");

        if(httpResponse.IsSuccessStatusCode)
        {
            QuantidadeTotalPaginas =
                int.Parse(httpResponse.Headers.GetValues("totalPaginas").FirstOrDefault());

            var responseString = await httpResponse.Content.ReadAsStringAsync();

            CLASSEs = JsonSerializer.Deserialize<List<CLASSE>>(responseString,
                new JsonSerializerOptions()
                {
                    PropertyNameCaseInsensitive = true
                });
        }
    }    
}
```