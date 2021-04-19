# **TypeScript**
> Auxilia na criação de codigos JavaScript com mais propriedades para as tags e a capacidade de prever erros para que não ocorrao em produção (no navegador). De forma simplificada ele torna o javascript uma linguagem mais tipada

### **Instalar e Configurar o Compilador**
> O passo a passo a seguir mostra como criar o ambiente para ser possivel escrever os codigos em TypeScript e retornar um JavaScript após a etapa de compilação

**Instalação o compilador**

- npm init
    - vai criar o arquivo package.json, e aqui vamos listar as dependencias 
- npm install typescript@NumeroVersao --save-dev
    - Adiciona ao projeto as dependencias do typescript, alem da pasta node_modules que tras o compilador do typescript para javascript
    
    Esses passos vao criar os arquivos para compilar o TypeScript 


**Configurando o compilador**
- Cria o **tsconfig.json**, lembre que sempre que alterar ele e necessario fechar e abrir o visual studio code para  configurar
``` javascript
{
    "compilerOptions": {
        "target": "es6", // Diz qual versão do JS que vai retornar
        "outDir": "app/js", // O resultado da compilação vai ser jogado aqui
        "noEmitOnError": true, // Essa propriedade garante que o projeto nao gere o compilado com erros
        "noImplicitAny": true, // Garante que as varaiveis criadas vão ter um TIPO (number, Date, ...) sabendo que se não for passar ele atribui o tipo ANY q seria equivalente a um "var"
        "removeComments": true, // Nao adiciona a saida do javascript comentarios feitos no typescrip
        "module": "system", // Adiciona o loader com o script do system.js que possibilita carregar apenas o app.js para sua pagina
        "strictNullChecks": true // Com isso o typescript reforca a validacao para as variaveis nao aceitarem o null e undefined sempre
    },
    "include": [
        "app/ts/**/*" // Diz quais arquivos deve levar em consideração
    ]
}
```

- **Altera o package.json**
``` javascript
{
  ... // acima nao importa
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "compile": "tsc", // Essa linha que vamos adicionar para que ele busque no node_modules o compilador
    "start": "tsc -w" // Com essa função nao precisamos rodar o npm run compile a cada alteração... Mas devemos rodar toda vez que formos editar o "npm start" e as aterações sao criadas no js em tempo de execucao
  },
  ... // abaixo tb nao
}
```
 - **Roda compilador**
    - npm run compile
    - npm start, essa opção precisamos ter configurado no package.json ("start": "tsc -w" )
---

- **Arquitetura**
    - app
        - css
        - js, criada quando compilamos
        - lib
        - ts
            - app.js
        - index.html
    - node_modules
    - package.json
    - tsconfig.json

---

### **Import & Export**
> É a forma de controlar a visualização do codigo

- **Export** podemos exportar uma classe ou todas as classes do mesmo arquivo

``` typescript
// uma classe
export class MeusObjeto {

}

// tem que criar um arquivo so para exportar assim
export * from './FILE'; 

```

- **Import** podemos importar uma classe ou varias do mesmo arquivo

``` typescript
import { MeuMetodo } from './FILE';

// tem que criar um arquivo chamado Index
import { MeuMetodo1, MeuMetodo2 } from '../FILE/Index';
```

---
### **Enum**
``` typescript
enum DiaDaSemana {
    Domingo,
    Segunda,
    Terca,
    Quarta, 
    Quinta, 
    Sexta, 
    Sabado, 
}
```

---
### **Model** classes
- **Class**
``` typescript
namespace NOME {
    // Criando um objeto, e o export tonar ele publico
    export class MEUobjeto 
    {
        // Aqui atribuimos o tipo da variavel e criamos dentro do construtor
        constructor(
            private _data: Date, 
            private _quantidade: number,  
            private _valor: number) {}

        // Cria um getter
        get data(){
            return this._data;
        }

        // Cria um metodo
        get volume() {
            return this._quantidade * this._valor;
        }
    }
}

// Assim criamos de maneira mais limpa o mesmo objeto de cima adicionando readonly
export class Negociacao {

    constructor(readonly data: Date, readonly quantidade: number, readonly valor: number) {}

    get volume() {

        return this.quantidade * this.valor;
    }

```

- **Lista**
``` typescript
namespace NOME {
    
        export class MeusObjetos {

        private _MEUObjetos: MEUObjeto[] = [];

        adiciona(entidade: MEUObjeto) {

            this._negociacoes.push(entidade);
        }

        // O elemento ": Negociacao[]" atribui o tipo de retorno, isso garante que nao teremos um retorno ANY. "as" Converter um objeto em um tipo específico
        paraArray() : Negociacao[] {

            return ([] as Negociacao[]).concat(this._negociacoes);
        }
    }
}

```
---
### **Controller**, recebendo Formularios
> Como pegar informações do formulario

- **Controller** podemos criar um metodo que preenche variaveis procurando o valor pelo ID na tela
    - Exemplo de como chamar na pagina.
        - Obs: Temos que referenciar todos os JS usados no HTML
``` typescript
// Controller/MeuController.js
class MEUController {    
    private _inputData: HTMLInputElement;
    private _inputQuantidade: HTMLInputElement;
    private _inputValor: HTMLInputElement;
    private _meusObjetos = new NOME.MeusObjetos();
    private _MEUView = new NOME.NegociacoesView('#MEUView');

    // Importamos o Decorator que vai gerar o Lazy Loading para os elementos abaixo
    import { domInject } from '../helpers/decorators/index';

    // Atribuimos o valor por lazy loading
    @domInject('#data')
    private _inputData: JQuery;

    // Atribuimos o valor por lazy loading
    @domInject('#quantidade')
    private _inputQuantidade: JQuery;

    // Atribuimos o valor por lazy loading
    @domInject('#valor')
    private _inputValor: JQuery;

    constructor() {        
    }

    adiciona(event: Event) {

        event.preventDefault();

        // Esse objeto foi criado previamente no models e aqui apenas instaciamos ele
        // Aqui ja esta convertendo os valores de entrada
        const meuObjeto = new MEUObjeto(
            // Precisa do replace para previnir erros
            new Date(this._inputData.value.replace(/-/g, ',')),
            parseInt(this._inputQuantidade.value),
            parseFloat(this._inputValor.value));

        this._meusObjetos.adiciona(meuObjeto);

        this._MEUView.update(this._meusObjetos);

        // Adiciona validação pelo navegador
        console.log(MEUobjeto);
    }
}

// Views/Scripts/main.js
    // Intanciando novo MEUController.js
const controller = new MEUController();

// Assim adicionamos um Listener no botão salvar para associar ao evento 'adiciona' que foi criado no MEUController.js
document
    .querySelector('.form')
    .addEventListener('submit',controller.adiciona.bind(controller));
```

---

### **View**

- Criando View com o padrao
``` typescript

namespace NOME {

    // Essa ferramenta nao é necessaria quando temos typescript definition, ja que ele pode adicionar o Jquery como se fosse um tipo de objeto
    declare var $: any;

    abstract class View<T> {

        // Salva a propriedade que vamos aplicar a VIEW
        protected _elemento: Element;

        // Recebe o ID dentro do HTML que ira atribuir o HTML criado aqui, por padrao podemos definir um valor de entrada que sera atribuido se nao passar valor na chamada
        constructor(seletor: string = "Sem valor") {
            this._elemento = $(seletor);
        }

        // Atribui o HTML do template na propriedade encontrada pelo constructor adicionando todos os Objetos que foram passados
        update(model: T) {

            this._elemento.html(this.template(model));
        }

        // Criamos o Front que vamos adicionar, nesse formato nao temos que concatenar informacao e manter as quebras de linha
        abstract template(model: T): string;
    }
}
```

- Criando View personalizada
``` typescript
class MEUView extends View<MEUSObjetos>{
    
    // Criamos o Front que vamos adicionar, nesse formato nao temos que concatenar informacao e manter as quebras de linha
    template(model: MEUSObjetos): string {

        `<table class="table table-hover table-bordered">
            <thead>
                <tr>
                    <th>DATA</th>
                    <th>QUANTIDADE</th>
                    <th>VALOR</th>
                    <th>VOLUME</th>
                </tr>
            </thead>

            <tbody>
                ${model.paraArray().map(x => 
                    `<tr>
                        <td>${x.data.getDate()}/${x.data.getMonth()+1}/${x.data.getFullYear()}</td>
                        <td>${x.quantidade}</td>
                        <td>${x.valor}</td>
                        <td>${x.volume}</td>
                     </tr>`
                     ).join('')} 
            </tbody>

            <tfoot>
            </tfoot>
        </table>`
    }
}
```

---

### **app.js**
> Ele recebe as requisições da tela

- **Criar**
``` typescript 
import { MEUController } from './controllers/MEUController';

const controller = new MEUController();
$('.form').submit(controller.adiciona.bind(controller));
$('#botao-importa').click(controller.importarDados.bind(controller));
```

---

### **TypeScript Definition**
> Existem bibliotecas para adicionar no typescript frameworks como por exemplo o Jquery que quando foi criado nao existia o typescript logo para usar dele de forma correta temos que baixar uma extensão.

- **Instalando**
    - Na raiz do seu projeto voce deve executar o comando abaixo, lembrando de trocar o BIBLIOTECA@VERSAO pelo que voce encontrou na sua pesquisa  
    ``` typescript
    npm install @types/@BIBLIOTECA@VERSAO --save-dev
    ```

---

### **Loader**
> Permite que adicionemos apenas o app.js como referencia do projeto, hoje é feito por uma biblioteca chamada system.js . Assim que é adicionada no "tscondig.json" voce deve reiniciar sua aplicacao e ela ira adicionar uma configuração em todos seus objetos criados

- **Abrindo**
    - para ver sua aplicacao rodando novamente após adicionar essa configuração você deve subir seu codigo como um servidor
        - Live Server é uma otima opção

- **Add no HTML**
``` html
<!-- outros frameworks devem ser adicionados na mao -->
<script src="lib/jquery.min.js"></script>

<script src="lib/system.js"></script>
<script>
    System.defaultJSExtensions = true;
    System.import('js/app.js').catch(err => console.error(err));
</script>
```

---

### **Decorator**, funciona como os attribute do c#
> Criamos um codigo que quando adicionado a um metodo vai ser chamado antes ou depois de toda chamada para esse metodo

- **Criando**

    Uma função que retorna outra função.

``` typescript
export function logarTempoDeExecucao(emSegundos: boolean = false) {

    // target > tipo de instancia que ele pode ser adicionado
    // propertyKey > Nome do metodo
    // descriptor > retornar as informações do metodo chamado e podemos até alterar o metodo com ele
    return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {

        // Pega o metodo original
        const metodoOriginal = descriptor.value;

        // Assim podemos sobescrever o metodo original
        descriptor.value = function(...args: any[]) {

            const retorno = metodoOriginal.apply(this, args);
            return retorno;
        }

        return descriptor;
    }
}
```

- **Adicionando**
``` typescript
// Podemos passar um parametro para o Decorator mas como criamos com valor default nao e obrigatorio
@logarTempoDeExecucao(true)
Metodo() {
    // Codigo
}
```
- **Exemplo de TimeOut**, esse timeout seria para aguardar a finalização de um evento antes de iniciar ele denovo POR SESSAO... isso evita o usuario de quebrar o site clicando muito em um botao

``` typescript
export function throttle(milissegundos = 500) {

    return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {

        const metodoOriginal = descriptor.value;

        let timer = 0;

        descriptor.value = function(...args: any[]) {

            clearInterval(timer);
            timer = setTimeout(() => metodoOriginal.apply(this, args), milissegundos);
        }

        return descriptor;
    }
}
```
---

### **LazyLoading**, aplicando decorator
> Logica para carregarmos os dados da tela somente quando forem necessarios, ou seja as variaveis que buscam o .val() de um id na tela so vao ser preenchidas quando forem solicitadas

- **Criando**
``` typescript
// Recebe como parametro de entrada o ID do campo
export function domInject(seletor: string) {

    // Key retorna o nome da variavel que vai receber o valor
    return function(target: any, key: string) {

        let elemento: JQuery;

        const getter = function() {

            if(!elemento) {
                console.log(`buscando  ${seletor} para injetar em ${key}`);
                elemento = $(seletor);
            }

            return elemento;
        }
       
       // Atribui que o Decorator vai ser chamado na propriedade Getter do objeto
       Object.defineProperty(target, key, {
           get: getter
       });
    }
}
```

- **Usando**, basta aplicarmos este decorator na criação da variavel no inicio do escopo do controller
``` typescript
@domInject('#data')
    private _inputData: JQuery;
```

---

### **Consumindo API**
> Podemos tratar essa requisição com ajax, mas o exemplo vai ser feito com "fetch"

- **Criando**
```typescript
function isOK(res: Response) {
    // Verifica se está ok, se não estiver retorna um erro
    if(res.ok) {
        return res;
    } else {
        throw new Error(res.statusText);
    }
}

fetch('http://localhost:8080/dados')
        // Chama a function acima para validar se recebeu os dados antes de continuar
        .then(res => isOK(res))
        // Convert para Json a resposta
        .then(res => res.json())
        // recebe os dados como vetor sem tipo
        .then((dados: any[]) => {
            dados
                // A partir do json cria um novo objeto, o problema e que "vezes" e "montante" sao variaveis que vem da api dentro do json então fica por nossa conta colocar o nome da variavel. Para solucionar isso podemos criar o objeto que esperamos da API e trocar o tipo "any[]" de dados pelo objeto criado
                .map(x => new MeuObjeto(new Date(), x.vezes, x.montante))
                // Adiciona o objeto a lista
                .forEach(y => this._MEUObjetos.adiciona(y));
            // Atualiza a View com a nova lista
            this._negociacoesView.update(this._negociacoes);
        })
        .catch(err => console.log(err.message));
```

---

### **Polimorfismo**, podemos herdar apenas uma vez no typescript
> Podemos herdar um objeto e sobreescrever um metodo

- **Criando**
```typescript
// Esse exemplo obriga os os objetos a sobreescerver o metodo 'Log' assim podemos criar depois um metodo que ja espera receber um objeto que possui o metodo 'Log'
export abstract class GeraLog {

    abstract Log(): void;
}
```

- **Herdando**
``` typescript
export class MeuObjeto extends GeraLog {

    // Codigo

    // Sobre escrevemos o objeto para passar as variaveis do MeuObjeto no console
    Log(): void {
        console.log('-- MeuObjeto --');
        console.log(
            `Data: ${this.data}
            Quantidade: ${this.quantidade}, 
            Valor: ${this.valor}, 
            Volume: ${this.volume}`
        )
    }
}
```

- **Usando**, podemos esperar um objeto que herde de 'GeraLog' dentro de um metodo para chamar o metodo 'Log' de uma lista

``` typescript
export function imprime(lista: GeraLog[]) {
    lista.forEach(x => x.Log());
}
```

---
### **Interface**
> Vamos usar o mesmo exemplo de cima que tem como objetivo imprimir no console um log

- **Criando**
```typescript
export interface GeraLog {

    Log(): void;
}
```

- **Herdando**
``` typescript
export class MeuCodigo implements GeraLog {

    // Codigo
    Log(): void {
        console.log('-- MeuObjeto --');
        console.log(
            `Data: ${this.data}
            Quantidade: ${this.quantidade}, 
            Valor: ${this.valor}, 
            Volume: ${this.volume}`
        )
    }
}
```
