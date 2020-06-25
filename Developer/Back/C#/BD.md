# **BANCO DADOS**

## **SqlConnection**
 - **Conexao**
 > criamos como uma classe depois instancioamos
``` c#
// CRIAMOS A CLASS
public static class ConexaoBD // Nome da Class
{
    public static SqlConnection GetConexao() // Nome do metodo
    {
        string strCon = "Data Source=LOCALHOST;Initial Catalog=BANCO;user id=USUARIO; password=123456";            
        SqlConnection conexao = new SqlConnection(strCon);
        conexao.Open();
        return conexao;
    }
}
/* Data Source=IP;
   Initial Catalog=BANCO;
   user id=USUARIO; 
   password="SENHA"; */
``` 

 - **Executando**
 > nao apropriado para consulta (select)
 ``` c#
SqlConnection conexao = ConexaoBD.GetConexao(); // Instancia a class de Conexao do banco
try
{
    string sql = String.Format("insert into alunos(id, nome, mensalidade, cidadeId, dataNascimento)"); // adicionamos a SQL

    SqlCommand comando = new SqlCommand(sql, conexao); // Insciamos um SqlCommand que e nativo do C# passando por paramentro a SQL e a conexao (classe criada)
    comando.ExecuteNonQuery(); // Executa SQL
}
finally // Para cado de ERRO
{
    conexao.Close();
}
 ```

 - **Vetor**
 > Criamos um vetor para enviar dados para o banco
 ``` c#
 SqlParameter[] parametros =
 {
    new SqlParameter("id", Jogo.Id),
    new SqlParameter("descricao", Jogo.Descricao),
    new SqlParameter("valor", Jogo.Valor),
    new SqlParameter("categoria", Jogo.Categoria),
    new SqlParameter("data", Jogo.Data)
 };
 ```

 - **Consultas**
 > Usado para consultas 
 ``` c#
 string COMANDO_EM_STRING = "select * from TABELA where id = " + ID;
 SqlAdapter adapter = new SqlAdapter (COMANDO_EM_STRING, CLASS_CONEXAO);
 DataTable tabela = new DataTable(); // cria uma tabela para salvarmos o select
 adapter.Fill(tabela); // salva na variavel que criamos "tabela" o select feito em adapter
 DataRow registro = tabela.Rows[0]; // cria array com primeira tabela criada acima
 string coluna = registro["COLUNA"].ToString(); // aqui temos que saber qual coluna ira retornar da tabela para adicionar em registros
 ```

- **Stored Procedure**
> podemos criar um metodo pronto dentro do banco para consulmir a carga dentro do servidor do banco e mandamos as variaveis do nosso programa para o banco executar o **SP**
``` C#
// CRIAMOS UM ARRAY PARA ENVIAR AS VARIAVEIS PARA O BANCO
private SqlParameter[] CriaParametros(FerramentasViewModel ferramenta)
        {
            SqlParameter[] parametros = new SqlParameter[3];
            parametros[0] = new SqlParameter("id", ferramenta.Id);
            parametros[1] = new SqlParameter("descricao ", ferramenta.Descricao);
            parametros[2] = new SqlParameter("FabricanteId", ferramenta.Fabricante);
            return parametros;
        }
// CHAMANDO A STORED PROCEDURE PASSANDO O NOME DA SP
public void Inserir(FerramentasViewModel ferramenta)
        {
            HelperDAO.ExecutaProc("spIncluiFerramenta", CriaParametros(ferramenta));
        }
//EXECUTANDO PROCEDURE 
public static void ExecutaProc(string nomeProc, SqlParameter[] parametros)
        {
            using (SqlConnection conexao = ConexaoBD.GetConexao())
            {
                using (SqlCommand comando = new SqlCommand(nomeProc, conexao))
                {
                    comando.CommandType = CommandType.StoredProcedure;
                    if (parametros != null)
                        comando.Parameters.AddRange(parametros);
                    comando.ExecuteNonQuery();
                }
                conexao.Close();
            }
        }
// RECEBENDO UMA LISTA
public List<FerramentasViewModel> Listagem()
        {
            List<FerramentasViewModel> lista = new List<FerramentasViewModel>();

            DataTable tabela = HelperDAO.ExecutaProcSelect("spListagemFerramentas", null);

            foreach (DataRow registro in tabela.Rows)
                lista.Add(Montaferramenta(registro));
            return lista;
        }
```
---

## **LinqSQL**

### **Criando**
- **Objeto do tipo LinqSQL**
> botao direito> add> LINQ to SQL Classes

- **ADD DataBase**
> A direita em "Data Conections" adicione a conecção ao servidor (Banco).

- **Map Tables**
> Arrasta as tabelas para o DataClasses. Os "dbml" (Objeto LinqSQL), podem receber mais de uma tabela entao sera necessario definir qual tabela vamos usar ao instanciar uma conecção usando ele

- **Configurando abertura conecção**
> Podemos redefinir a forma como abrimos a conecção para usar depois na Bll como mostra o exemplo abaixo:
``` c#
// os DB_NAME abaixo faz referencia a uma class do .Net
public partial class ConfiguracaoNomeDataContext
    {
        private const Connections.DB_NAME DEFAULT_CONNECTION = Connections.DB_NAME.BANCO;
        private static string connectionString = Connections.getSqlConnectionString(DEFAULT_CONNECTION);

        public ConfiguracaoNomeDataContext() : base(connectionString) { OnCreated(); }
    }
```

### **Bll - Tratando os dados**
> Aqui vamos instanciar os principais metodos para tratar os dados, lembrando que a "ConfiguracaoNomeDataContext" trata-se da abertura configurada acima e os "nome" a uma tabela.

- **Exemplos:** Completo
``` C#
public static List<Nome> List_nome()
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                List<Nome> retorno =  coneccao.Nomes.ToList();
                coneccao.Nomes.ToList();
                coneccao.Dispose();
                return retorno;
            }
        }
        catch (Exception ex)
        {
            return null;
        }
    }
    public static Nome nome(int Id)
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                Nome retorno = coneccao.Nomes.Where(x => x.Id == Id).FirstOrDefault();
                coneccao.Nomes.ToList();
                coneccao.Dispose();
                return retorno;
            }
        }
        catch (Exception ex)
        {
            return null;
        }
    }
    // por padrao se o banco gera o ID sozinho voce tera que ir ate o "ConfiguracaoNomeDataContext" e trocar a variavel "int Id" para "int? Id" e depois resolver os conflitos alterando de "int" para "int?"
    public static string Insert(Nome entidade)
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                coneccao.Nomes.InsertOnSubmit(entidade);
                coneccao.SubmitChanges();
                coneccao.Dispose();
                return null;
            }
        }
        catch (Exception e)
        {
            return e.Message;
        }
    }
    public static string Update(Nome entidade)
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                Nome retorno = coneccao.Nomes.Single(x => x.Id == entidade.Id);
                retorno.a = entidade.a;
                retorno.b = entidade.b;
                retorno.c = entidade.c;
                retorno.d = entidade.d;

                coneccao.SubmitChanges();
                coneccao.Dispose();
                return null;
            }
        }
        catch (Exception e)
        {
            return e.Message;
        }
    }
    public static bool Exist(Nome entidade)
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                Nome retorno = coneccao.Nomes.Where(x => x.Id == entidade.Id).FirstOrDefault();
                coneccao.Dispose();
                if (retorno == null)
                    return false;
                else
                    return true;
            }
        }
        catch (Exception e)
        {
            return false;
        }
    }
    public static string Delete(Nome entidade)
    {
        try
        {
            using (ConfiguracaoNomeDataContext coneccao = new ConfiguracaoNomeDataContext())
            {
                 coneccao.Nomes.Attach(entidade, false);
                coneccao.Nomes.DeleteOnSubmit(entidade);
                coneccao.SubmitChanges();
                coneccao.Dispose();
                return null;
            }
        }
        catch (Exception e)
        {
            return e.Message;
        }
    }
```
- **Exemplos:** Solução Generica, infelizmente não foi possivel deixar o mapeamento da coneccao generico tambem
``` C#
public static List<T> To_List<T>() where T : class
{
    try
    {
        using (ConeccaoDataContext dc = new ConeccaoDataContext())
        {
            return dc.GetTable<T>().ToList<T>();
        }
    }
    catch
    {
        return null;
    }
}
public static string Insert<T>(T entidade) where T : class
{
    try
    {
        using (ConeccaoDataContext dc = new ConeccaoDataContext())
        {
            var table = dc.GetTable<T>();
            table.InsertOnSubmit(entidade);
            dc.SubmitChanges();
            return null;
        }
    }
    catch
    {
        return "ERRO!";
    }
}
public static string Update<T>(T item) where T : class
{
    try
    {
        Object obj = Activator.CreateInstance(typeof(T), new object[0]);

        PropertyDescriptorCollection prop = TypeDescriptor.GetProperties(item);

        foreach (PropertyDescriptor currentProp in prop)
        {
            if (currentProp.Attributes[typeof(ColumnAttribute)] != null)
            {
                object val = currentProp.GetValue(item);
                currentProp.SetValue(obj, val);
            }
        }
        using (ConeccaoDataContext dc = new ConeccaoDataContext())
        {
            var table = dc.GetTable<T>();
            table.Attach((T)obj, true);
            dc.SubmitChanges();
        }
        return null;
    }
    catch (Exception e)
    {
        return e.Message;
    }
}
public static bool Remove<T>(T item) where T : class
{
    try
    {
        Type type = item.GetType();
        Object obj = Activator.CreateInstance(type, new object[0]);
        PropertyDescriptorCollection prop = TypeDescriptor.GetProperties(item);
        foreach (PropertyDescriptor currentProp in prop)
        {
            if (currentProp.Attributes[typeof(ColumnAttribute)] != null)
            {
                object val = currentProp.GetValue(item);
                currentProp.SetValue(obj, val);
            }
        }
        using (ConeccaoDataContext dc = new ConeccaoDataContext())
        {
            var table = dc.GetTable<T>();
            table.Attach((T)obj, true);
            table.DeleteOnSubmit((T)obj);
            dc.SubmitChanges();
        }
        return true;
    }
    catch (Exception)
    {
        return false;
    }
}
public static bool Exist<T>(T entidade) where T : class
{
    try
    {
        using (ConeccaoDataContext dc = new ConeccaoDataContext())
        {
            int retorno = dc.GetTable<T>().Count();
            if (retorno <= 0)
                return false;
            return true;
        }
    }
    catch
    {
        return false;
    }
}
```
---
## **Entity**
- [Frameworks](https://github.com/luizgustavo77/Notes/blob/master/Frameworks/Entity.md)

--- 
## **DTS** Data Transformation Services
> Executa processos de cargar, procedures, entre outros...

- **Criando:**   
    Tem uma interface muito parecida com o WindowsForms, 
    - **Create a New External Connection:**
        - **All** >> **Provider: SELECIONE O PROVEDOR**
        - **Provider SAP Config**   
            **Application Server Host:**    
             - **Application Server Host:** IP
             - **System Number:** 2  

            **Login Information**               
            - **Client:** 200
            - **Language:** PT
            - **PassWord:** SENHA
            - **User Name:** USUARIO

    - **SSIS ToolBox:**
        - **Execute SQL Task:** Executa comando SQL
            - **Properties:**   
            **Connections** Adiciona a conneccao com o banco   
            **SQLStatement** Adiciona o codigo SQL que deve rodar 

        - **Data Flow Task:** Descer dados de outros bancos, aqui adicionamos a consulta e ele nos devolve os dados.       
            - **ADO.Net Source Editor** Origem dos dados   
            **Connection Management**   
                - **ADO.NET connection manager:** Adiciona conneccao com o SAP
                - **Data acess mode:** SQL command  
                - **SQL command text:** comandos do SQL que vamos executar para pesquisar no SAP
            - **OLE DB Destination Editor** Destino dos dados no banco    
            **Connection Management**  
                - **OLE DB connetion manager:** Adiciona coneccao com o banco 
                - **Data acess mode:** Table or View - fast load
                - **Name of table or the view:**    
                Adiciona um existente do banco ou      
                Da um NEW e cria uma nova com SQL      
                **Check:** Table Lock, Check Contrains     
                **Macimum insert commit size:** 2147483647      

                **Mapping**   
                **Input Column:** Adiciona a coluna de entrada   
                **Destination Column:** Mapeia a saida do Input com base na tabela carregada ou criada
        - **Sequence Container:** Garante que todos os executaveis dentro dele sejam terminados antes de passar para proxima interação, para usar so colocar as Task dentro dele

- **Publicar:**
 Podemos adicionar um "dtsx" dentro do banco para que o DTS seja rodado por um job ou pelo usuariO
 **OBs:** Em algumas versoes do SQL Server nao descemos o package (.dtsz), quando for assim faz deploy da aplicação inteira
 ```mermaid
graph TD
Projeto-->Deploy
Deploy-->SelectSource 
SelectSource-->|SELECIONE|SelectDestination 
SelectDestination-->|INSERIR OS DADOS|Connect 
Connect-->Review 
Review-->ClickDeploy
```

- **Requisitos carga do SAP**
    - Adicionar pacote SAP Gir Bistalk
    - **Propriedades do Projeto > Configuration Propriets > Debugging:**   
    **Run64BitRuntime**  FALSE
