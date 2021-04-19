# **Form**
- **Tags**
    - aps-for: para atribuir valor as variaveis do obj
    - asp-validation-for: para atribuir mensagem de validacao
    - asp-controller: nome do controller
    - asp-action: nome do metodo
    
- **Method:** Por padrão o metodo é "Get" se não discrevermos no HTML, ao dar um submite no formulario nos iremos enviar os valores dos inputs por query string

```html
<!-- Envia por get (QueryString) os valores dos inputes com o nome da varivel sendo descrito no "name". Se não houver name não envia nada --->
<form action="/Cadastro/Incluir">

        <label>Título:</label>
        <input name="titulo" />
        <br />

        <label>Autor:</label>
        <input name="autor" />
        <br />

        <button>Gravar</button>
</form>

<!-- Envia por post os valores dos inputes com o nome da varivel sendo descrito no "name". Se não houver name não envia nada --->
<form action="/Cadastro/Incluir" method="post">

        <label>Título:</label>
        <input name="titulo" />
        <br />

        <label>Autor:</label>
        <input name="autor" />
        <br />

        <button>Gravar</button>
</form>
``` 
