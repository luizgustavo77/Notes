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
}


```

- **Insert**
    - **Chamando:** com a configuração acima criada, basta usarmos as ferramentas do entity
```c#
CLASSE c = new CLASSE();
using (var contexto = new NOMEContext())
{
    contexto.CLASSEs.Add(c);
    contexto.SaveChanges();
}
```

- **Select**
    - **Chamando** com a configuração criada, basta usarmos as ferramentas do entity
``` c#
using (var contexto = new NOMEContext())
{
    IListCLASSE lista = contexto.CLASSEs.ToList();
}
```

- **Delete**  
     - **Chamando** com a configuração criada, basta usarmos as ferramentas do entity
``` c#
using (var contexto = new NOMEContext())
{
    CLASSE item = contexto.CLASSEs.First();
    contexto.CLASSEs.Remove(item);        
    contexto.SaveChanges();
}
```

- **Update**  
     - **Chamando** com a configuração criada, basta usarmos as ferramentas do entity
``` c#
using (var contexto = new NOMEContext())
{
    CLASSE item = contexto.CLASSEs..First();
    item.variavel = "Atualizado";
    contexto.CLASSEs.Update(item);
    contexto.SaveChanges();
}
```
### **DAO**
 Para podermos criar um padrao na hora de usar criamos o DAO

- **Interface:** Deve ser herdada para garantir a criação desse CRUD
```c#
 interface ICLASSEDAO
{
    void Adicionar(CLASSE item);
    void Atualizar(CLASSE item);
    void Remover(CLASSE item);
    IListCLASSE CLASSEs();
}
```
- **Implementação:** Adicionar as ferramentas 
``` c#
class CLASSEDAOEntity : ICLASSEDAO, IDisposable
{
    private NOMEContext contexto;

    public CLASSEDAOEntity()
    {
        this.contexto = new NOMEContext(); 
    }

    public void Dispose()
    {
        contexto.Dispose();
    }

    public void Adicionar(CLASSE item)
    {
        contexto.CLASSEs.Add(item);
        contexto.SaveChanges();
    }

    public void Atualizar(CLASSE item)
    {
        contexto.CLASSEs.Update(item);
        contexto.SaveChanges();
    }

     public void Remover(CLASSE item)
    {
        contexto.CLASSEs.Remove(item);
        contexto.SaveChanges();
    }

    public IListCLASSE CLASSEs()
    {
        return contexto.CLASSEs.ToList();
    }
}
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

### **Create Database**
> Para adicionar uma criacao do banco caso ele não exista

- **DataService.cs**
    - **Create**
``` c#
class DataService : IDataService
{
    private readonly ApplicationContext contexto;

    public DataService(ApplicationContext contexto)
        this.contexto = contexto;
    }

    public void InicializaDB()
    {
        contexto.Database.EnsureCreated();
    }        
}
```

- **Startup.cs**
    - **ADD** 
``` C#
//ConfigureServices
services.AddTransient<IDataService, DataService>();

//Configure
serviceProvider.GetService<IDataService>().InicializaDB();
```

