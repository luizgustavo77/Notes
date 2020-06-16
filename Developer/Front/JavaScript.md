# JavaScript
- linguagem que executa script apartir do cliente (navegador)
- deixe sempre o JavaScript como ultimo elemento ao carregar a pagina para ter todos os elementos criados
- Codigos terminam obrigatoriamente em ;
- possui tipagem dinamica - var pode receber string, int, ...
- orientado a objeto - ou seja tem variaveis que guardam varios valores referentes a algo como uma Classe
- vetor comeca do 0
- adiciona NOME.js ao html com um <script src="NOME.js"></script>

***linguagem***  
- VAR
  - var NOME = DADO; - adiciona informacao a variavel
  - var nome= [1, 2, 3]; - vetor
  - nome[0]; - para devolver a posicao 0 do vetor
  - var NOME = {}; - para atribuir varias variaveis e criar um objeto
  - NOME.NOME - para pegar uma propriedade do objeto 
  - console.log (); - mostra informacoes no depurador de desenvolvedor do navegador

**Exemplos de comandos**  
```
function NOME(NOME1,NOME2){ - cria um metodo 
  var NOME4 = NOME1 + NOME2;
  return NOME3;
}
if (NOME == 'CHAR') { - faz um if
}
=== - checa tipo de variavel tb por ex (1 === "1") returna false
&& - and 
!== - not 
Ifternario - return (CONDICAO) ? NOME1 - se for true cai aq : NOME2 - se for false cai aq
for igual c#
foreach - for (usuario of usuarios) {}
while (CONDICAO){
  ACAO;
  VAR++;
}
setInterval (function,1000); - executa com intervalos em mili segundos
setTimeout (function, 1000); - espera um tempo para executar 
```
**Trabalhando com a DOM**  
Para chamar uma funcao dentro do HTML so precisa colocar o evento e dentro dele o NOME_DA_FUNCAO()  

> Ex: <input type="button" onclick="devolve()" value="BOTAO"//>

* **DOCUMENT**
```
document.getElementATRIBUTO('NOME1') - referencia a arvore de elementos do projeto com o id de NOME1
  TagName/ClassName: sempre retorna um vetor entao precisa colocar o []
  document.querySelector('body div#ID input') - voce pode passar o caminho ate a propriedade que deseja encontrar
  document.querySelector('input[name=NOME]') - voce pode fazer uma busca dentro dsa tag 
  document.querySelectorall('input') - assim ele devolve um objeto com todos os caminhos 
  VAR_NOME.EVENTO = function(){ ACAO } - podemos salvar um atributo da DOM em uma var e determinar acoes para ele desta forma
  Podemos pegar a tag e salvar dentro de um var para depois usar NOME.value; para recuperar oque foi inserido nela 
  Podemos adicionar uma tag no HTML com document.createATRIBUTO ex:document.createElement('a'); depois setAttribute('href','http://link');        tambem podemos fazer heranca com VAR_NOME.appenChild(VAR_NOME1);
  Pomdemos remover uma tag do HTML com o document.removeChild('#ID') - assim ela nem aparece no html
podemos adicionar style em um var Ex: NOME.style.backgroundColor= '#f00';
```

* **InnerHTML**
> Altera o texto presente dentro de uma TAG  

``` html
<script>
function myFunction() { 
  document.getElementById("demo").innerHTML = "Hello JavaScript!";
}

<!-- -->

<button id="demo" type="button" onclick="myFunction()">Click Me!</button>
```
* **NoScript**
> Em caso de falha na hora de rodar o JavaScript

<noscript>Sorry, your browser does not support JavaScript!</noscript>

- **Funcoes com JQUERY**
  - Como subir na hierarquia do HTML pelo JQuery
    - Use o Parents do JQuery passando o ID
    - JQuery Find encontra tag HTML como um input
  - class in javascript
    - para chamar os metodos dentro dela usa o this.NOME()
