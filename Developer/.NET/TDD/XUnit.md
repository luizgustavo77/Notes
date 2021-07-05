# **[XUnit](https://en.wikipedia.org/wiki/Unit_testing)**

## **AAA** Arrange, Act e Assert
> Teste unitário é um tipo de teste de software onde uma pequena parte da aplicação, chamada de unidade, podendo ser uma função, classe ou método, é testada individualmente. Esse teste é realizado durante o processo de desenvolvimento de um software com o objetivo de verificar se cada unidade está funcionando como esperado.

- **Arrange** Onde iniciamos os objetos que vao ser passados como referencia. 
- **Act** Declaramos o metodo testado.
- **Assert** Verificamos os resultados esperados.
---
- **Assert**

     Parametro que define o retorno do teste

     - **Equals** Recebe dois parametros e para ser verdadeiro eles tem que ser iguais
     
    - **IsType<T>** Recebe dois parametros e para ser verdadeiro eles tem que ser do mesmo tipo

    - **Throws<T>** Recebe dois parametros e para ser verdadeiro eles tem que ser do mesmo tipo de excessao

- **Fact**
> Atributo que define os metodos como teste 

``` c#
[Fact]
public void MeuTeste()
{
    //Arrange
    var num1 = 2;
    var num2 = 5;
    var resultadoEsperado = 7;
    //Act
    var resultadoObtido = num1 + num2;
    //Assert
    Assert.Equal(resultadoEsperado, resultadoObtido);
}
``` 

- **Theory && InlineData**
> Atrivuto para definir o metodo como teste e adicionar entradas

``` c#
[Theory]
[InlineData(7, 2, 5)
public void RetornaSomaDeDoisNumeros(int resultadoEsperado, int num1, int num2)
{
    //Act
    var resultadoObtido = num1 + num2;
    //Assert
    Assert.Equal(resultadoEsperado, resultadoObtido);
}
```

---

# **Mock**

- **Teste de integração:** Teste com recursos pesados, como acesso ao banco, nesses casos podemos trabalhar somente essas informações em memoria.

### **- InMemory** Faz parte do entity framework e devemos instalar no projeto de teste para poder usar no lugar do banco de dados

``` C#
// Definimos isso no dbcontext para quando usarmos o InMemory ele n chamar o conexao com o banco
public class DbUsuarioContext : DbContext
{
    ...
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        if (optionsBuilder.IsConfigured) return;

        optionsBuilder.UseSqlServer("minha conexao");
    }
    ...
}

// Usando na classe de teste
[Fact]
public void MeuTeste()
{
    var options = new DbContextOptionsBuilder<DbUsuarioContext>()
        .UseInMemoryDatabase("DbUsuarioContext")
        .Options;
    var contexto = new DbUsuarioContext(options);
    var repo = new RepositorioTarefa(contexto);

    ...
}
```

### **- Configurando Mock**
> Intalar na classe de teste o Moq (feito por Daniel Cazzulino)

``` c#
// Usando na classe de teste
[Fact]
public void MeuTesteuUm()
{
    ...
    var mock = new Mock<IRepositorioTarefas>();
    var repo = mock.Object;
    var handler = new RepositorioTarefa(repo);
    ...
}


[Fact]
public void MeuTesteDois()
{
    ...
    //arrange
    var mockLogger = new Mock<ILogger>();

    var options = new DbContextOptionsBuilder<DbTarefasContext>()
        .UseInMemoryDatabase("DbTarefasContext")
        .Options;
    var contexto = new DbTarefasContext(options);
    var repo = new RepositorioTarefa(contexto);
    
    var controlador = new TarefasController(repo, mockLogger.Object);
    ...
}
```

- **mock.Setup** Podemos definir um comportamento para quando um metodo é chamado
``` c#
// Aqui deifnimos que quando o metodo "MeuMetodo" for chamado passando o parametro "Usuario[]" o mock vai lançar a Exception
mock.Setup(x => x.MeuMetodo(It.IsAny<Usuario[]>()))
        .Throws(new Exception("Houve um erro na inclusão de tarefas"));
...

// Precisa de um Assert validando o retorno
```

- **mock.Verify** Podemos vericar informações sobre um determinado metodo
``` c#
// Aqui validamos se o metodo foi chamado com o paramero "id" uma vez
mock.Verify(x => x.MeuMetodo(id), Times.Once());

// Não precisa de Assert
```

---
# **Selenium**
> Testando interfaces, para rodar o teste precisamos ter o projeto no ar

- **Instalar**
    - Selenium.WebDriver
    - Selenium.Chrome.WebDriver 

- **ClassFixture** Forma de vc compartilhar uma instancia de classe por objetos

- **Usando o Chrome:** 
    1. Para usar o Chrome precisamos passar como referencia o local dele (costuma ficar no bin/debugge)
    2. Precisamos usar o Disposable para fechar o navegador a cada teste

- **ChromeDriver** Ferramentas disponiveis apos instanciar corretamente
    - **driver.PageSource** Pega informações do html
    - **drive.Title** Pega o titulo da pagina
    - **driver.FindElement** Identifica elemento no html
        - By.Id
        - By.CssSelector
        - By.TagName

- **IAction** Ferramenta para disparar ações na tela
    - **MovetToElement** Movementa o mause para um campo na tela
    - **Build** Monta ação
    - **Perform** Executa ação

- **Selenium.Support**
    - **Options** Traz elementos de uma lista

### **- Criando** Segue a disposição por pastas
- **Fixture**
``` c#
 public class Fixture : IDisposable
{
    public IWebDriver Driver { get; private set; }

    //Setup
    public Fixture()
    {
        Driver = new ChromeDriver(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location));
    }

    //TearDown
    public void Dispose()
    {
        Driver.Quit();
    }
}
```

```c#
[CollectionDefinition("Chrome Driver")]
public class CollectionFixture : ICollectionFixture<TestFixture>
{
}
``` 

- **PageObjects**
``` c#
public class RegistroPO
{
    private IWebDriver driver;
    private By byInputEmail;
    private By byBotaoRegistro;

    public RegistroPO(IWebDriver driver)
    {
        this.driver = driver;
        byInputEmail = By.Id("Email");
        byBotaoRegistro = By.Id("btnRegistro");
    }

    public void Visitar()
    {
        driver.Navigate().GoToUrl("http://localhost:5000");
    }

    public void SubmeteFormulario()
    {
        driver.FindElement(byBotaoRegistro).Click();
    }

    public void PreencheFormulario(string email)
    {
        driver.FindElement(byInputEmail).SendKeys(email);
    }
}
```

- **Testes**
``` c#
 [Collection("Chrome Driver")]
public class TesteQualquer
{
    private IWebDriver driver;

    public TesteQualquer(Fixture fixture)
    {
        driver = fixture.Driver;
    }

    [Fact]
    public void MeuTeste()
    {
        //arrange

        //act
        driver.Navigate().GoToUrl("http://localhost:5000");

        //assert
        Assert.Contains("Próximos Leilões", driver.PageSource);
    }
}
```

### **- Usando**

- **Passando informações**
``` c#
// Input
driver.Navigate().GoToUrl("http://localhost:5000");
var inputNome = driver.FindElement(By.Id("Nome"));
inputNome.SendKeys("LG");


// Event
var botaoRegistro = driver.FindElement(By.Id("btnRegistro"));
botaoRegistro.Click();
```

- **Validando mensagem de Required**
``` c#
[Fact]
public void ValidEmailRequired()
{
    //arrange
    driver.Navigate().GoToUrl("http://localhost:5000");

    //email
    var inputEmail = driver.FindElement(By.Id("Email"));
    inputEmail.SendKeys("daniel");

    //botão de registro
    var botaoRegistro = driver.FindElement(By.Id("btnRegistro"));

    //act
    botaoRegistro.Click();

    //assert - 
    IWebElement elemento = driver.FindElement(By.CssSelector("span.msg-erro[data-valmsg-for=Email]"));
    Assert.Equal("Please enter a valid email address.", elemento.Text);
}
```

- **Abrindo meno com hover**
``` c#
// Nesse caso precisamos posicionar o mause no "meu-perfil" para abrir o menu com o item logout
public void EfetuarLogout()
{
    var linkMeuPerfil = driver.FindElement(By.Id("meu-perfil"));
    var linkLogout = driver.FindElement(By.Id("logout"));

    IAction acaoLogout = new Actions(driver)
        //mover para o elemento meu-perfil
        .MoveToElement(linkMeuPerfil)
        //mover para o link de logout
        .MoveToElement(linkLogout)
        //clicar no link de logout
        .Click()
        .Build();

    acaoLogout.Perform();
}
```

- **Pegando o texto dos options no ddl que estão habilitadas**
``` c#
public List<string> Categorias
{
    get
    {
        var elementoCategoria = new SelectElement(driver.FindElement(By.Id("Categoria")));
        return elementoCategoria.Options
            .Where(o => o.Enabled)
            .Select(o => o.Text).ToList();
    }
}
```