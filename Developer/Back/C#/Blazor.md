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
### **Blazor Server App VS Blazor WebAssembly APP**
> Ambos sao projetos blazor, mas o framework oferece essas duas opcoes

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

## **Blazor WebAssembly App**

- **Instalando** o template do Blazor WebAssembly APP
    - dotnet new --install Microsoft.AspNetCore.Blazor.Templates::3.1.0-preview4.19579.2

### **Template, Blazor WebAssembly App Com o check "ASP NET Core hosted**
> Quando marcado segue o modelo **Client-Side + .Net Core** criando Client, Server e Shared (Comom). Nessa hospedagem a aplicação nao roda offiline 

### **Client**
> Aqui temos a aplicação Blazor e as paginas com Razor


### **Server**
> Aqui criamos as WEB API's e conectamos a Base de dados 


### **Shared**
> É um mediador que tem codigos compartilhados com Client e Server

---

## **Paginas Blazor**


- **_Host.cshtml / index.html** Dentro dele temo um script que habilita o SignalIR  no blazor "< script src="_framework/blazor.webassebly.js"></script>" e ponta e carrega o App.razor

- **App.razor** Configura as rotas solicitadas pela URL

- **MainLayout.razor** Define o layout da pagina e nele adicionamos outras paginas

- **NavMenu.razor** Aqui criamos o menu da aplicação com seus itens e o MainLayout carrega ele

- **_Imports.razor** Tem os namespaces comuns do projeto

---
## **Razor SZ Blazor**
> Razor no Blazor e diferente do ASP NET, la sao usadas apenas na View e gera o NOME.cshtml, no blazor geramos um NOME.razor, é executado no navegador e a pagina se atualiza dinamicamente sem voltar ao servidor.

- Chamando Razor
    - **@**
    - ***@( ... )***

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
``` blazor
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
---
## **Diretivas**
> Determina a pagina vai ser compilada, e devem ser adicionados no inicio da pagina

- **@page** Define qa rota de requisições do browser. 

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

## **Tags Blazor**

- **@page "/CAMINHO"** define o caminho ate essa pagina

- **@Body** Define o local onde vamos renderizar as paginas que chegam dentro do MainLayout

- **< NavLink href="CAMINHO"></ NavLink>** Definimos um link para a pagina NOME.razer nesse CAMINHO

- **@Code {}** Aqui dentro podemos declarar variaveis, metodos, classes..

---
## **First Loading**
> Assim que você abre a pagina no seu navegador esse evento dispara, é bom trabalhar bem ele pois se for o primeiro acesso pode levar alguns segundos

- **Como atribuir**
   - No seu index tem uma tag chamada "<app><app>" que por padrão vem escrito "Loading...", podemos trocar o texto por um gif ou outro elemento para deixar essa espera mais bonita

---
## **Metodos**
> Algumas dicas de como trabalhar com metodos e os principais metodos

- **Como chamar metodos dentro do evento HTML**
   - < button @onclick="MeuMetodo">Botao</ button>
- **On OnInitializedAsync**, evento que roda ao terminar de carregar a pagina de forma Async
   - protected override async Task OnInitializedAsync(){}

- **Chamando API/Arquivo**, aqui recupera um arquivo dentro de "wwwroot" e converte para uma lista de CLASSE
   - @inject HttpClient http
   - await http.GetJsonAsync<List< CLASSE>>("arquivo.json");