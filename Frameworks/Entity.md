# **Entity**
 Framework é um ORM (Mapeamento Objeto Relacional) para compor classes e mapear com o banco.

### - [**Documentação**](https://www.entityframeworktutorial.net/)

### **Instalando**
- **NuGet:** Ferramentas  Gerenciador de pacotes do NuGet  Console do Gerenciador de Pacotes
    - **Comando:** Install-Package Microsoft.EntityFrameworkCore.SqlServer  
        - **Help:** Get-Help EntityFramework

### **Funcionamento**
- **ChangeTracker.Entries();** Propriedade que armazena as entidades que estamos usando no projeto
    - **State** Status que descreve oque foi feito com o Objeto
        - **Unchanged** Nao foi alterado
        - **Modified** Alterado e aguardando .SaveChanges(); para salvar
        - **Added** Adicionado e aguardando .SaveChanges(); para salvar
        - **Deleted** Deletado e aguardando .SaveChanges(); para excluir
        - **Detached** Nao monitorado pelo Entity
``` c#
//Para pegar o estado dos objetos na Entidade aberta em "contexto"
foreach (var e in contexto.ChangeTracker.Entries())
    Console.WriteLine(e);

// para pegar o estado com base no objeto
var entry = contexto.Entry(CLASSE);
Console.WriteLine(entry.Entity.ToString() + " - " + entry.State); // Exemplo para mostrar o objeto e seu status
``` 

### **Chamando**

- **Coneccao** objeto
    - **Criando:** Precisa herdar da base "DbContext"
    - **Configurando:** Precisamos reescrever o "OnConfiguring" para informar a coneccao ao banco 
``` c#
using ConsoleApplication1;
using Microsoft.EntityFrameworkCore;
public class NOMEContext : DbContext
{
    public DbSet<CLASSE> CLASSEs { get; set; } // CLASSEs vai ser o nome da tabela.

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("Server=(localdb)\\mssqllocaldb;Database=MEU_BANCO;Trusted_Connection=true;");
        //optionsBuilder.UseSqlServer("Server=myServerAddress;Database=myDataBase;User Id=myUsername;password=myPassword;Trusted_Connection=False;MultipleActiveResultSets=true;")
    }

    // Este metodo serve como exemplo para criar o relacionamento de chave composta no padrao Migration
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder
            .Entity<CLASSE2>()
            .HasKey(x => new { x.CLASSE1Id, y.CLASSE2Id });
            // podemos criar as relacoes do mapeamento aqui tambem com HasMany/HasOne
        base.OnModelCreating(modelBuilder);
    }
}


```


### **DAO**
 Para podermos criar um padrao na hora de usar criamos o DAO

- **Interface:** Deve ser herdada para garantir a criação desse CRUD
```c#
 interface ICLASSEDAO
{
    RetornaAcao Adicionar(CLASSE item);
    RetornaAcao Atualizar(CLASSE item);
    RetornaAcao Remover(CLASSE item);
    bool Existe(int? Id);
    CLASSE Localizar(int? Id);
    IList<CLASSE> ListCLASSEs();
}
```
- **Implementação:** Adicionar as ferramentas 
``` c#
public class CLASSEDAO : ICLASSEDAO, IDisposable
{
    private DBContext _contexto;

    public CLASSEDAO()
    {
        this._contexto = new DBContext();
    }

    public void Dispose()
    {
        _contexto.Dispose();
    }

    public RetornaAcao Adicionar(CLASSE item)
    {
        RetornaAcao retorno = new RetornaAcao();
        try
        {
            _contexto.CLASSEs.Add(item);
            _contexto.SaveChanges();
            retorno.Retorno = true;
            retorno.Mensagem = "Salvo com sucesso!";
        }
        catch (Exception ex)
        {
            retorno.Retorno = false;
            retorno.Mensagem = "Erro! " + ex.Message;
        }
        return retorno;
    }

    public RetornaAcao Atualizar(CLASSE item)
    {
        RetornaAcao retorno = new RetornaAcao();
        try
        {
            _contexto.CLASSEs.Update(item);
            _contexto.SaveChanges();
            retorno.Retorno = true;
            retorno.Mensagem = "Atualizado com sucesso!";
        }
        catch (Exception ex)
        {
            retorno.Retorno = false;
            retorno.Mensagem = "Erro! " + ex.Message;
        }
        return retorno;
    }

    public RetornaAcao Remover(CLASSE item)
    {
        RetornaAcao retorno = new RetornaAcao();
        try
        {
            _contexto.CLASSEs.Remove(item);
            _contexto.SaveChanges();
            retorno.Retorno = true;
            retorno.Mensagem = "Excluido com sucesso!";
        }
        catch (Exception ex)
        {
            retorno.Retorno = false;
            retorno.Mensagem = "Erro! " + ex.Message;
        }
        return retorno;
    }

    public CLASSE Localizar(int? Id)
    {
        CLASSE retorno = null;
        try
        {
            retorno = _contexto.CLASSEs.FirstOrDefault(x => x.Id == Id);
        }
        catch (Exception ex)
        {

        }
        return retorno;
    }

    public bool Existe(int? Id)
    {
        bool retorno = false;
        try
        {
            retorno = _contexto.CLASSEs.Any(x => x.Id == Id);
        }
        catch (Exception ex)
        {

        }
        return retorno;
    }

    public IList<CLASSE> ListCLASSEs()
    {
        IList<CLASSE> retorno = null;
        try
        {
            retorno = _contexto.CLASSEs.ToList();
        }
        catch (Exception ex)
        {

        }
        return retorno;
    }    
}
```
- **Core**
``` c#

// Adiciona ao Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    // Injecao de dependencia do DAO e da conexao do banco
    services.AddTransient<ILoginDAO, LoginDAO>();
    services.AddDbContext<DBContext>();
    ...
```

- **Cascade**
> Exemplo de cascade
``` c#
// Objetos
public class User
{
    public int ID { get; set; }
    public string EmailAddress { get; set; }
    public virtual ICollection<Address> Addresses { get; set; }
}

public class Address
{
    public int ID { get; set; }
    public string City { get; set; }
    public string Street { get; set; }
    public string Postcode { get; set; }
}

// DBCONTEXT
class TestDbContext : DbContext
{
    public TestDbContext()
        : base("DefaultConnectionString")
    {
    }
    public DbSet<User> Users { get; set; }
    public DbSet<Address> Addresses { get; set; }
}

// SAVE
var context = new TestDbContext();
var user = context.Users.FirstOrDefault(item => item.ID == 1);
user.Addresses.Add(new Address()
{
    City = "City",
    Street = "Street",
    Postcode = "Postcode",
});
context.SaveChanges();
```

### **Migrations** Code First 
 > Extensão do Entity para sincroniza o ambiente de desenvolvimento com o Banco de Dados, ele identifica automaticamente com base no "DbSet< CLASSE > NOME"  implementados ele ou objetos telacionados no Entity ao banco 

**Sempre confira a Migration antes de rodar!**
 - **Instalando:** Ferramentas  Gerenciador de pacotes do NuGet  Console do Gerenciador de Pacotes
    - **Comando:** Install-Package Microsoft.EntityFrameworkCore.Tools

- **Relacionamento:** Por padrão o Migration entende o relacionamento entre as tabelas sozinho, basta seguir algumas regras
    - **Chave Primaria:** podemos atribuir de duas formas, ou adicionando uma variavel do tipo int com o nome **"Id"** ou atribuindo o parametro **[KEY]** acima da variavel.
    - **Chave Estrangeira:** apontando uma classe dentro da outra e adicionando uma variavel com o nome **"CLASSEId"** para ser a chave estrangeira
    - **Chave Composta:** temos que definiar a criação de chave composta no metodo de coneccao (NOMEContext), usando polimorfismo 
    - **N x N** muitos para muitos precisamos criar uma tabela que vai fazer essa relação e para as tabelas que vao compor atribuimos um **"IList< CLASSE > CLASSEId"**
``` c#
// Chave Primaria
public int Id {get; set; }
//ou
[Key]
public int Chave { get; set; }

// Chave Estrangeira
public class CLASSE1
{
    public int CLASSE2Id { get; set; }
    public CLASSE2 CLASSE2 { get; internal set; }
}

// Chave composta
using ConsoleApplication1;
using Microsoft.EntityFrameworkCore;
public class NOMEContext : DbContext
{
    public DbSet<CLASSE1> CLASSE1s { get; set; }
    public DbSet<CLASSE2> CLASSE2s { get; set; }

    // Este metodo serve como exemplo para criar o relacionamento de chave composta no padrao Migration
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder
            .Entity<CLASSE3>()
            .HasKey(x => new { pp.CLASSE1Id, pp.CLASSE2Id });
            // podemos criar as relacoes do mapeamento aqui tambem com HasMany/HasOne
        base.OnModelCreating(modelBuilder);
    }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("Server=(localdb)\\mssqllocaldb;Database=MEU_BANCO;Trusted_Connection=true;");
    }
}

// N x N
public class CLASSE1
{
    public int Id { get; set; }
    public IList<CLASSE3> CLASSE2s { get; set; }
}
public class CLASSE2
{
    public int Id { get; set; }
    public IList<CLASSE3> CLASSE1s { get; set; }
}
public class CLASSE3 // Observação que aqui usamos chave composta
{
    public int CLASSE1Id { get; set; }
    public int CLASSE2Id { get; set; }
    public CLASSE1 CLASSE1 { get; set; }
    public CLASSE2 CLASSE2 { get; set; }
}
```
- **Comandos:** Todos no Console do Gerenciador de Pacotes
    - **Script-Migration** cria um script SQL para rodar no BD
    - **Add-Migration NOME** sincronizar uma mudança de seu modelo de classes com o banco de dados e adicionar uma pasta com um **SNAPSHOT** do modelo atual de banco de dadose um projeto com os metodos **UP / DOWN**
        - **UP / DOWN** Sobe ou desce uma versão do banco de dados
        - **SYNTAX :** Add-Migration -Name String, -OutputDir String, -Context String, -Project String, -StartupProject String, -Environment String, CommonParameters
    - **Remove-Migration**   remover a última migração não aplicada no banco de dados apontado pelo contexto.
        - **SYNTAX:** Remove-Migration -Force, -Context String, -Environment String, -Project String, -StartupProject String, CommonParameters
    - **Update-Database -Verbose**  adicionar uma tabela que registra o historico de versoes 
        - **Update-Database LastGoodMigration** Retorna o estado anterior
        - **SYNTAX:** Update-Database -Migration String, -Context String, -Environment String, -Project String, -StartupProject String, CommonParameters

    - **Drop-Database**  dropar o banco de dados apontado pelo contexto.

### **Create Database Migrations**
> Para adicionar uma criacao do banco caso ele não exista quando usamos o Migrations no codigo

- **Startup.cs**
    - **ADD** 
``` C#
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Roda os Migrations caso o banco de dados não exista
    using (var serviceScope = app.ApplicationServices.GetService<IServiceScopeFactory>().CreateScope())
    {
        var context = serviceScope.ServiceProvider.GetRequiredService<DBContext>();
        context.Database.Migrate();
    }
    ...
```

