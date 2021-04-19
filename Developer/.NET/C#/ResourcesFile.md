# **Resources File**
> Criamos um arquivo que funciona como um banco chave-valor

- **Criando**
    - Add > New Item > General > Resource File
---

### **View**
> Podemos usar para mudar o idioma da View

- **Usando**

    Ao criar um resource o c# cria toda ma estrutura que facilita na hora de chamar pois as chaves se comportam como variaveis em um objeto

``` C#
@using NOME_PROJETO.PASTA

NOME_RESOURCES.CHAVE
```

### **Idiomas**
> Podemos criar outro Resource com o mesmo nome mas que extende do idioma, assim podemos trocar o idioma alterando um atributo no webconfig

- **Criando**

```C#
// Idioma padrão
NOME.resx

// Nome em Ingles como exemplo
NOME.en-us.resx
```

- **Definindo Idioma**

    No **Web.config** dentro da tag **system.web** definimos o idioma assim e servidor vai tratar na hora de chamar o Resource. Mas lembre-se que os dois devem ter as mesmas chaves para nao gerar uma exeção

``` xml
<globalization uiCulture="en-us">
```
