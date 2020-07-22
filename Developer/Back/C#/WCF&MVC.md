# **WCF** Windows Communication Foundation
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
