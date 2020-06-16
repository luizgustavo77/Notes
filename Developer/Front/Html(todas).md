## **TODAS AS TAGS**
``` html
<!--...--> Define um comentário;
<!DOCTYPE> Define o tipo de documento;
<a> Define um hyperlink;
<abbr> Define uma abreviação
<address> Define um endereço. (Passa a ser tratado como uma seção);
<area> Define uma área dentro de um mapa de imagem;
<b> Define um texto em negrito; (Possui o mesmo nível semântico que um SPAN, e também o estilo de negrito no texto. Contudo, ele não dá nenhuma importância para o texto marcado com ele.)
<base> Define uma base URL para todos os links da página;
<bdo> Define a direção do texto apresentado;
<blockquote> Define uma citação longa;
<body> Define o corpo da página;
<br> Insere uma quebra de linha simples;
<button> Define um botão de comando;
<caption> Define o "caption" de uma tabela;
<cite> Define uma citação;
<code> Define o código texto do computador;
<col> Define os atributos da coluna da tabela;
<colgroup> Define um grupo de colunas da tabela;
<dd> Define uma descrição de definição;
<del> Define um texto deletado;
<dfn> Define um termo de definição;
<div> Define uma seção no documento;
<dl> Define uma lista de definição;
<dt> Define um termo de definição;
<em> Define um texto em ênfase;
<fieldset> Define um conjunto de campos (fieldset);
<form> Define um formulário;
<h1> até >h6> Define do cabeçalho 1 até o cabeçalho 6;
<head> Define uma informação sobre o documento. (Não aceita mais elementos Child como filho);
<hr> Define uma regra horizontal. (Tem o mesmo nível que um parágrafo, mas também é utilizado para fazer separações e quebras de linha);
<html> Define um documento html;
<i> Define um texto em itálico; (Possui o mesmo nível semântico que um SPAN. O texto continua sendo itálico e para usuários de leitores de tela, a voz utilizada é modificada para indicar ênfase. É de grande valor e utilidade para marcar, termos técnicos, termos em outras linguagens etc.)
<iframe> Define uma linhas sobre a janela (frame);
<img> Define uma imagem;
<input> Define um campo de inserção;
<ins> Define um texto inserido;
<kbd> Define um texto do teclado;
<label> Define uma "label" para o formulário;
<legend> Define um título para os campos (fields);
<li> Define os itens da lista;
<link> Define uma referência;
<map> Define uma imagem de mapa;
<menu> Define uma lista de "menus";
<meta> Define informações meta;
<noscript> Define uma seção noscript;
<object> Define um objeto incorporado;
<ol> Define uma lista ordenada;
<optgroup> Define um grupo de opção;
<option> Define uma opção em uma lista suspensa (drop-down list);
<p> Define um parágrafo;
<param> Define um parâmetro para determinado objeto;
<pre> Define um texto pré-formatado;
<q> Define uma citação curta;
<s> Define um texto que não é mais correto.
<samp> Define um código de amostra;
<script> Define um script;
<select> Define uma lista selecionável;
<small> Define um pequeno texto;
<span> Define uma seção no documento;
<strong> Define um texto forte (similar ao negrito);
<style> Define um estilo;
<sub> Define um texto subscrito;
<sup> Define um texto sobrescrito;
<table> Define uma tabela;
<tbody> Define o corpo da tabela;
<td> Define uma célula da tabela;
<textarea> Define um área de texto;
<tfoot> Define o rodapé da tabela;
<th> Define o cabeçalho da tabela;
<thead> Define o cabeçalho da tabela;
<title> Define o título do documento;
<tr> Define uma linha da tabela;
<ul> Define uma lista desordenada;
<var> Define uma variável;
```

## **Atributos Globais**

- contenteditable - especifica se o usuário está autorizado a editar um conteúdo ou não: true|false (verdadeiro|Falso).
- contextmenu - especifica um menu contexto para um elemento. menu_id.
- draggable - especifica se um usuário tem permissão para arrastar um elemento: true|false|auto (verdadeiro|falso|automático).
- dropzone - especifica o que acontece quando um dado arrastado é solto: copy|move|link (copiar|mover|linkar).
- hidden - especifica que o elemento não é relevante: hidden (oculto).
- spellcheck - especifica se o elemento deve ter sua grafia verificada: true|false (verdadeiro|falso).

## **Eventos**

### **De Janelas:**
- onafterprint - executa após o documento ser impresso.
- onbeforeprint - executa antes do documento ser impresso.
- onbeforeonload - executa antes do documento ser carregado.
- onerror - executa quando ocorre um erro.
- onhaschange - executa quando o documento sofre alteração.
- onmessage - executa quando uma mensagem é disparada.
- onoffline - executa quando o documento é desconectado da internet.
- ononline - executa quando o documento é conectado à internet.
- onpagehide - executa quando a janela é ocultada.
- onpageshow - executa quando a janela se torna visível.
- onpopstate - executa quando ocorre alteração no histórico da janela.
- onredo- executa quando é acionado o comando de repetir.
- onresize - executa quando a janela tem alteração de tamanho.
- onstorage - executa quando um documento é carregado.
- onundo - executa quando é acionado o comando de desfazer.
- onunload - executa quando o usuário sai do documento.

### **De Formulários:**
- oncontextmenu - executa quando um menu de contexto é acionado.
- onformchange - executa quando ocorre alterações no formulário.
- onforminput - executa quando o usuário dá entrada no formulário.
- oninput - executa quando um elemento dá entrada do usuário no formulário.
- oninvalid - executa quando um elemento não é válido.

### **De Mouse:**
- ondrag - executa quando um elemento é arrastado.
- ondragend - executa ao fim de uma operação de arrastar um elemento.
- ondragenter - executa quando um elemento é arrastado e solto em seu destino.
- ondragleave - executa quando um elemento é solto em um destino válido.
- ondragover - executa quando elemento é arrastado e solto ao longo de um destino.
- ondragstart - executa quando se inicia uma operação de arrastar.
- ondrop - executa quando o elemento arrastado está sendo descartado.
- onmousewheel - executa quando o scroll do mouse é girado.
- onscroll - executa quando as barras de rolagem de um elemento está sendo rolada.

### **De Multimídia:**
- oncanplay - executa quando uma mídia está sendo iniciada a tocar.
- onclanplaythrought - executa quando a mídia está sendo tocada até o fim.
- ondurationchange - executa quando o comprimento da mídia é alterado.
- onemptied - executado quando um elemento de recursos de mídia torna-se vazio.
- onended - executa quando a mídia chega ao fim.
- onerror - executa quando ocorre um erro de carregamento de um elemento.
- onloadeddata - executa quando os dados de mídia são carregados.
- onloadedmetadata - executa quando a duração de um elemento de mídia está sendo carregado.
- onloadstart - executa quando o navegador começa a carregar os dados de mídia.
- onpause - executa quando a mídia de dados está em pausa.
- onplay - executa quando a mídia de dados for começar a tocar.
- onplaying - executa quando a mídia começa a tocar.
- onprogress - executa quando o navegador está buscando os dados de mídia.
- onratechange - executa quando altera a faixa de mídia .
onreadystatechange - executa quando ocorre uma mudança de estado.
- onseeked - executa quando o atributo de busca de um elemento não é verdadeiro.
- onseeking - executa quando o atributo de busca de um elemento é verdadeiro.
- onstalled - executa quando há um erro na busca de dados de mídia.
- onsuspend - executa quando o navegador para de buscar os dados da mídia.
- ontimeupdate - executa quando a posição da mídia é alterada.
- onvolumechange - executar quando a mídia muda de volume e, também, quando o volume fica mudo.
- onwaiting - executar quando a mídia para de tocar.

## **Layout**
``` html
<article>: Define um artigo;
<aside>: Define o conteúdo além do conteúdo da página;
<embed>: Define o conteúdo interativo ou plugin externo;
<figcaption>: Define o caption de uma imagem;
<figure>: Define um grupo de média e seus captions;
<footer>: Define o rodapé de uma página;
<header>: Define o cabeçalho de uma página;
<nav>: Define os links de navegação;
<section>: Define uma área ou seção;
<wbr>: Define uma possível quebra de linha;
``` 
### **Media**
``` html
<audio>: Define o conteúdo de som;
<source>: Define recursos de mídia;
<video>: Define um vídeo;
```
### **Aplicativos Web**
``` html
<canvas>: Define gráficos;
<command>: Define um botão de comando;
<datagrid>: Referências aos dados dinâmicos em Tree View ou 
tabelas;
<datalist>: Define uma lista suspensa (DropDown);
<details>: Define detalhes de um elemento;
<output>: Define os tipos de saída (outputs);
<progress>: Define o progresso de uma tarefa qualquer;
```
## **Outros**
``` html
<dialog>: Define uma conversa ou pessoas falando;
<hgroup>: Define informações sobre uma determinada área do documento;
<keygen>: Define a key (chave) do formulário;
<mark>: Define a marcação de um texto;
<meter>: Define a medição dentro de um intervalo pré-definido;
<summary>: Define o cabeçalho de dados “detalhe”;
<time>: Define uma data ou hora;
```
