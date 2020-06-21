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
- Desvantagem

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

- **Client-Side**, Blazor Server App

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

- **Server-Side**, Blazor WebAssembly (Client-Side + .Net Core)

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

---

## **Tags Blazor**

- **@page "/CAMINHO"** define o caminho ate essa pagina

- **< NOME />** Podemos instanciar/referenciar uma pagina NOME.razor para mostrar na tela

- **@Body** Define o local onde vamos renderizar as paginas que chegam dentro do MainLayout

- **< NavLink href="CAMINHO"></ NavLink>** Definimos um link para a pagina NOME.razer nesse CAMINHO

- **@Corde {}** Aqui dentro podemos declarar variaveis, metodos, classes..
