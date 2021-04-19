# **Soluções WEB**

### **ValidateAntiFogeryToken**
> Bloqueia o acesso a aplicacoes externas
- **Para requisições Ajax**
    - **Controller**
    - [ValidateAntiFogeryToken] 
        - impede acesso externo a aplicacao
    - **View**
    - Para permitir o acesso via Ajax dentro da pagina a metodos do controler protegidor de acesso externo na pagina adicionamso o HTML abaixo:
``` html
<!-- View -->
<form method="post" asp-action="carrinho">
</form>
```
``` javascript
// Ajax

let token = $('[name=__RequestVerificationToken]')
let headers = {};
headers['RequestVerificationToken'] = token;

$ajax({
    url:'/pedido/updatequantidade',
    type: 'POST',
    data: JSON.stringify(data),
    headers: headers
})done(function (response) { 
```

- **Padrão ASP.Net**
``` c#
// Controller
[ValidateAntiForgeryToken, HttpPost]
public ActionResult Salvar(CLASSE c)
{
    // Codigo
}
```
``` html
<!-- View -->
<form action="/Produto/Adiciona" method="post">
    @Html.AntiForgeryToken() // Adiona chave para requisição
    <label for="nome">Nome:</label>
    <input id="nome" name="produto.Nome" class="form-control" />
</form>
```
---

### **ModelState.AddModelError**
> Podemos atribuir um **asp-validation-for="NOME"** no HTML e depois validar ele no Controller apartir de um **ModelState.AddModelError**
```c#
//Adicionando no form
<label for="NOME" class="control-label">Descricao Ferramenta</label>
<input type="text" Name="NOME" value="ID" class="form-control" />
<span asp-validation-for="NOME" class="text-danger"></span>

//Dentro do controller
private void ValidaDados(CLASSE Objeto)
{            
   if (Objeto.NOME <= 0)
       ModelState.AddModelError("NOME", "Preencha NOME.");
}
```
> Outra forma de montar essa validação
``` c#
<style>
.field-validation-error {
    color: red;
}
</style>
@Html.PasswordFor(model => model.ConfirmarSenha, new { @minLength = "6", @id = "confirmarSenhaAluno", @class = "form-control input-lg", @placeHolder = "Confirmar Senha" })
@Html.ValidationMessageFor(x => x.ConfirmarSenha)

// No controller
public ActionResult Cadastro(RedefinirSenhaViewModel model)
{
  if (!model.Senha.Equals(model.ConfirmarSenha))
  {
    ModelState.AddModelError("ConfirmarSenha", "As senhas estão divergentes.");
  }

  if (!ModelState.IsValid)
  {
    return PartialView("Index", model);
  }
// ...
```
---
### **Inserir imagens no banco com WEB**

- **HTML**

```html
 <div class="col-lg-2 col-md-2 col-sm-12 col-xs-12">
	<div class="form-group">
		<div id="insertImage" style="margin-top:25px;">
			<img id='fotoPessoa' src='~/Content/images/user/generic.jpg' width='100' height='100' alt='Foto' />
		</div>
		<div id="AlteraImgHide">
			<label class="btn btn-primary center-block text-center" for="btnAlteraImg">Alterar</label>
			<input id="btnAlteraImg" type="file" onchange="usuario.Cadastro.alterarFoto(event); return false;" multiple style="display:none;">
		</div>
	</div>
</div>
```

- **JavaScript**
``` javascript
var alterarFoto = function (event) {
            var selectedFile = event.target.files[0];
            var reader = new FileReader();
            var imgtag = $(controles().fotoPessoa); //ID DA IMG 
            imgtag.title = selectedFile.name;
            reader.readAsDataURL(selectedFile);

            reader.onloadend = function () {
                $(controles().insertImage).empty(); //ID DA DIV QUE MANTEM A IMG
                $(controles().insertImage).append("<div class='moldura' style='background-image: url(" + reader.result + ");'></div>");
                ArquivoFoto = {
                    Nome: selectedFile.name,
                    ContentType: selectedFile.type,
                    Conteudo: reader.result.slice(reader.result.indexOf(",") + 1)
                };
            }
        }
```

- **Banco**
```sql
CREATE TABLE [core].[Arquivo](
	[Id_Arquivo] [int] NOT NULL,
	[Arquivo] [varbinary](max) NOT NULL,
	[Extensao] [varchar](5) NULL,
	[Nome] [varchar](8000) NULL,
 CONSTRAINT [PK_Arquivo] PRIMARY KEY CLUSTERED 
(
	[Id_Arquivo] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]

GO

SET ANSI_PADDING ON
GO

ALTER TABLE [core].[Arquivo] ADD  CONSTRAINT [DF__Arquivo__Id_Arqu__1E6F845E]  DEFAULT (NEXT VALUE FOR [core].[SeqArquivo]) FOR [Id_Arquivo]
GO

```
--- 
- **Requisição WEB**
``` c#
static void Main(string[] args)
{
    HttpClient cliente = new HttpClient();
    var textoDoSite = cliente.GetStringAsync("http://www.caelum.com.br");
    Console.WriteLine(textoDoSite);
    Console.ReadKey();
}
```

- **Baixando Imagem**
```c#
WebClient client = new WebClient();
client.DownloadFile("http://server1/image1.jpg", "C:\\file1.jpg");
client.Dispose();
```

- **Consumindo Json**
``` c#
 static async Task XMain(string[] args)
        {
            //TAREFA:
            //CONSULTAR OS DADOS DO CEP 04101-300
            //NO SERVIÇO DA http://viacep.com.br
            //E EXIBIR SEUS DADOS

            string cep = "04101300";
            string url = $"http://viacep.com.br/ws/{cep}/json/";

            using (var cliente = new HttpClient())
            {
                var json = await cliente.GetStringAsync(url);

                var endereco = JsonConvert.DeserializeObject<Endereco>(json);


                Console.WriteLine(
                    $"Logradouro: {endereco.logradouro}" +
                    $"\nBairro: {endereco.bairro}" +
                    $"\nMunicípio: {endereco.localidade}" +
                    $"\nUF: {endereco.uf}" +
                    $"\nCEP: {endereco.cep}");
            }

            Console.ReadKey();
        }
    }

    class Endereco
    {
        public string cep { get; set; }
        public string logradouro { get; set; }
        public string bairro { get; set; }
        public string localidade { get; set; }
        public string uf { get; set; }
    }
```
- **Verificando URL Exist**
```
private static bool RemoteFileExists(string url)
{
    try
    {
	HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;
	request.Method = "HEAD";
	using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
	{
	    return (response.StatusCode == HttpStatusCode.OK);
	}
    }
    catch
    {
	return false;
    }
}
```
---
## **Ajax SZ WebForms**

- **COMO CRIAR O METODO**
``` c#
[System.Web.Script.Services.ScriptMethod()]
[System.Web.Services.WebMethod]
public static int MEUMETODO(string VARIAVEL)
{
    //VALIDA RE DIGITADO
    int retorno = 0;
    SqlDataReader reader = cls_Funcao.reader(VARIAVEL);
    if (reader.Read())
        retorno = 1;

    if (reader != null)
        ((IDisposable)reader).Dispose();

    return retorno;
}
```

- **COMO CHAMAR NO JAVASCRIPT**
``` javascript
function MEUMETODO(VALOR) {
    $.ajax({
        cache: false,
        async: true,
        type: 'POST',
        data: JSON.stringify({ 'VARIAVEL': VALOR }),
        url: '/CAMINHO/PAGINA.aspx/METODO',
        dataType: 'json',
        contentType: "application/json; charset=utf-8",
        error: function (XMLHttpRequest) {
            alert("Erro !");
        },
        success: function (data) {
            return data;
        }
    });
}
```
