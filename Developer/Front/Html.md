# **HTML**

## **Principais Tags de HTML**

 **Comentario**
 > Cria um comentário
``` html 
<!–- -–>  
```

**html**
> Envolve todo um documento html
``` html
<html> </html>
```
**head** 
> Envolve o cabeçalho de um documento html  
``` html
<head> </head>  
```


**meta**
> Fornece informações gerais sobre o documento
```html
<meta charset="UTF-8">
<meta name="description" content="Free Web tutorials">
<meta name="keywords" content="HTML, CSS, XML, JavaScript">
<meta name="author" content="John Doe">
<meta http-equiv="refresh" content="30">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**link**
> Faz referencia a um arquivo externo
```html
<link rel="stylesheet" href="mystyle.css">
```

**style**
> Informações de estilo
``` html
<img src="..." style="width:500px;height:600px;">
```

**script**
> Linguagem script

- noscript  
Conteúdo alternativo para quando a linguagem script não for suportada
``` html
<script> </script>
<noscript>Sorry, your browser does not support JavaScript!</noscript>
```

**title**
> O título do documento 
```html
<title>My Pag</title>
```

**body**
> Envolve o corpo (texto e tags) do documento html
```html
<body> </body>
```

- bgcolor – Cor de fundo #RRGGBB
- background – Imagem como plano de fundo
- text – Cor do texto principal
- link – Cor dos links existentes na página
- vlink – Cor do link já visitado
- alink – Cor do link que foi ativado
- marginheight – Elimina a margem esquerda apenas no Netscape
- marginwidth – Elimina a margem no topo da página apenas no Netscape
- topmargin – Elimina a margem no topo da página apenas no Internet Explorer
- leftmargin – Elimina a margem esquerda apenas no Internet Explorer

### **Cabeçalhos**
> Cabeçalho nível n para n de 1 a 6
``` html
<hn> </hn>
Cabeçalho nível n para n de 1 a 6
```

### **Parágrafos**
``` html
<p> </p>
paragrafo simples
```
- title	- Especifica informações extras sobre um elemento (exibido como tool tip)
- align – Alinhamento do parágrafo: left, right, center e justify

### **Links**
``` html
<a> </a>
Cria um link e inclui atributos em comum
```
- Target atributo pode ter um dos seguintes valores:
  - _blank - Abre o documento vinculado em uma nova janela ou guia
  - _self - Abre o documento vinculado na mesma janela / guia em que foi clicado (isso é o padrão)
  - _parent - Abre o documento vinculado no quadro pai
  - _top - Abre o documento vinculado no corpo inteiro da janela

- href – O URL do documento que será vinculado a este. Para e-mail: mailto e link externo: http
- name – O nome da âncora
- target – Identifica a janela ou local em que o link deverá ser aberto: blank, self, top, parent
- rel – Define os tipos de link que avançam
- rev – Define os tipos de link que revertem a ação
- acesskey – Atribui uma tecla de atalho para este elemento
- shape – Para uso com formas de objeto
- coords – Para uso com formas de objeto
- tabindex – Determina a ordem das guias
- onclick – É um evento JavaScript
- onmouseover – É um evento JavaScript
- onmouseout – É um evento JavaScript

### **Listas**
``` html
<ol> </ol>
Uma lista ordenada
```
- start – Define a partir de qual número a listagem começa
- type="1" -	The list items will be numbered with numbers (default)
- type="A" -	The list items will be numbered with uppercase letters
- type="a" -	The list items will be numbered with lowercase letters
- type="I" -	The list items will be numbered with uppercase roman numbers
- type="i" -	The list items will be numbered with lowercase roman numbers
```html
<ul> </ul>
Uma lista não ordenada
```

- Modelo de  marcador para a lista nao ordenada
  - disc - Sets the list item marker to a bullet (default)
  - circle	- Sets the list item marker to a circle
  - square -	Sets the list item marker to a square
  - none -	The list items will not be marked 

``` html
<li> </li>
Um item da lista
```
- value – Numeração individual do item da lista
``` html
<menu> </menu>
Um menu com uma lista de itens
```
```html
<dir> </dir>
Uma listagem de diretórios
```
```html
<dl> </dl>
Uma lista de definições ou glossário
```

```html
<dt> </dt>
Marca o texto especificado como um termo de definição de um glossário
```

```html
<dd> </dd>
Especifica o texto referente a um termo criado pela tag <dt> dentro de uma lista de definição
```

### **Formatação de caracteres**
``` html
<em> </em>
Maior ênfase em itálico
```
```html
<strong> </strong>
Maior ênfase em negrito
```
```html
<code> </code>
Amostra de código
```
```html
<kbd> </kbd>
Texto a ser digitado
```
```html
<var> </var>
Uma variável ou espaço reservado para um outro valor
```
```html
<samp> </samp>
Texto de amostra
```
```html
<dfn> </dfn>
Aplica um formatação no texto definido como termo de um glossário
```
```html
<cite> </cite>
Uma citação
```
```html
<b> </b>
Texto em negrito
```
```html
<i> </i>
Texto em itálico
```
```html
<u> </u>
Texto sublinhado
```
```html
<tt> </tt>
Fonte monoespaçada (texto semelhante à maquina de escrever)
```
```html
<pre> </pre>
Texto pré-formatado
```
```html
<strike> </strike>
Texto riscado
```
```html
<s> </s>
Texto tachado
```
```html
<sub> </sub>
Texto subscrito
```
```html
<sup> </sup>
Texto sobrescrito
```
```html
<big> </big>
Texto em fonte maior do que o padrão
```
```html
<small> </small>
Texto em fonte menor do que o padrão
```

```html
<blink> </blink>
Texto piscando somente no Nestcape
```
```html
<marquee> </marquee>
Texto animado no Internet Explorer
```

### **Outros elementos**
``` html
<hr>
Uma régua horizontal
```
- size – Espessura da linha em pixels
- width – Largura da linha em pixels ou porcentagem
- align – Alinhamento da linha em center, left, right
- color – Cor da linha em #RRGGBB
- noshade – Linha sólida
```html
<br>
Uma quebra de linha
```
```html
<center> </center>
Centralizar
```
```html
<div> </div>
Conteúdo
```

- align – Alinhamento: left, center e right
```html
<blockquote> </blockquote>
Texto com mais margem
```
```html
<address> </address>
Assinaturas ou informações gerais sobre o autor de um documento
```
```html
<font> </font>
Alterna tamanho , cor e tipo de fonte exibida
```

- size – O tamanho da fonte varia de 1 a 7
- color – A cor da fonte #RRGGBB
- face – O tipo da fonte
```html
<basefonte>
Define o tamanho padrão para a fonte na página atual
```
- size – O tamanho da fonte varia de 1 a 7

### **Imagens**
```html
<img>
Insere uma imagem in-line no documento e inclui atributos comuns
```
- usemap – Um mapa de imagens do lado cliente
```
<img src="....jpg" usemap="#workmap">

<map name="workmap">
  <area shape="rect" coords="34,44,270,350" alt="Computer" href="computer.htm">
  <area shape="rect" coords="290,172,333,250" alt="Phone" href="phone.htm">
  <area shape="circle" coords="337,300,44" alt="Coffee" href="coffee.htm">
</map>
```
- src – O URL da imagem
- alt – Uma string de texto que será exibida em navegadores que não possam suportar imagens
- align – Determina o alinhamento de uma determinada imagem: top, middle, bottom, left e right
- height – É a altura sugerida em pixels
- width – É a extensão sugerida em pixels
- vspace – O espaço entre a imagem e o texto acima e abaixo dela
- hspace – O espaço entre a imagem e o texto à esquerda e à direita dela
- border – Largura da borda

### **Frames**
``` html
<frameset> </frameset>
Define um frameset
```
- rows – Número de linhas no frame
- cols – Número de colunas no frame
- frameborder – Borda do frame
- framespacing – Espaçamento
- onload – É um evento intrínseco
- onunload – É um evento intrínseco
``` html
<frame> </frame>
Define um frameset
```
- name – É o nome do frame-alvo
- src – Chama a fonte de conteúdo do frame
- frameborder – Determina a borda do frame
- marginheight – Determina a largura das margens
- noresize – Determina a capacidade de redimensionar frames
- scrolling – Determina a capacidade de rolagem dentro dos frames: auto, yes e no
```html
<iframe> </iframe>
Define um frame in-line
```
```html
<iframe src="URL"></iframe>
```
```html
<noframes> </noframes>
Alterna o conteúdo quando os frames não são suportados
```

### **Tabelas**
``` html
<table> </table>
Cria uma tabela
```
- background – Imagem de plano de fundo
- bgcolor – Cor de plano de fundo
- border – Largura da borda em pixels
- cols – Número de colunas
- cellpadding – Espaçamento nas células
- cellspacing – Espaçamento entre as células
- width – Largura da tabela
- align – Alinhamento da tabela: left, center, right
- bordercolor – Cor na borda da tabela
```html
<caption> </caption>
A legenda para a tabela
```
```html
<tr> </tr>
Uma linha na tabela
```

- align – O alinhamento horizontal do conteúdo das células dentro dessa linha com os valores possíveis left, right, center, justify e char
- bgcolor – Cor de fundo
- valign – o alinhamento vertical do conteúdo das células dentro dessa linha com os valores possíveis top, middle, bottom e baseline
- background – Figura como plano de fundo
```html
<th> </th>
Um cabeçalho de célula da tabela
```
- align – Alinhamento horizontal
- valign – Alinhamento vertical
- bgcolor – Cor de plano de fundo
- rowspan – O número de linhas pelo qual essa célula se expandirá
- colspan – O número de colunas pelo qual essa célula se expandirá
- nowrap – Desliga o enquadramento de texto em uma célula
```html
<td> </td>
Define uma célula de dados da tabela
```
- align – Alinhamento horizontal
- valign – Alinhamento vertical
- bgcolor – Cor de plano de fundo
- rowspan – O número de linhas pelo qual essa célula se expandirá
- colspan – O número de colunas pelo qual essa célula se expandirá
- nowrap – Desliga o enquadramento de texto em uma célula
- width – Largura da célula
- height – Altura da célula

### **Formulários**
``` html
<form> </form>
Define um formulário
```
- action – Responsável por determinar o exato local para onde as informações coletadas no formulário deverão ser enviadas
- method – Método de empacotamento dos dados do formulário: get, post e enctype="multipart/form-data"
- name – Nome do objeto
``` html
<fieldset>
elemento é usado para agrupar dados relacionados em um formulário.
  <legend>
  elemento define uma legenda para o <fieldset> elemento.
```
``` html
<input>
Caixa de texto
```
- type – Tipo de dado: text, file, radio, checkbox, hidden, password, submit, reset, button, image
- name – Identificação do campo
  usamos o name tambem para garantir que nao haja suplicidade na hora de marcar uma caixa
- size – Largura
- maxlength – Número máximo de caracteres permitidos
- value – Texto que aparece dentro da caixa ou nome do botão
- checked value – Valor assumido quando este campo for selecionado
```html
<textarea> </textarea>
Permite criar elementos de entrada com características de texto
```
- rows – Tamanho da linha da caixa de texto
- cols – Tamanho da coluna da caixa de texto
- name – Identificação do campo
- wrap – Quebra de linha da caixa de texto: off, virtual, physical
```html
<select> </select>
Seleção
```
- name – Identificador
```html
<option> </option>
Opção
```
- value – Valor do campo

### **Como converter de HTML para XHTML**
- Adicione um XHTML <! DOCTYPE> à primeira linha de cada página
- Adicione um atributo xmlns ao elemento html de cada página
- Alterar todos os nomes de elementos para minúsculas
- Feche todos os elementos vazios
- Alterar todos os nomes de atributo para minúsculas
- Cite todos os valores de atributo


[Todas as Tags](https://github.com/luizgustavo77/Estudos/blob/master/Html(todas).md)
