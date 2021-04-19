# **Angular**
> Framework para front-end

## **Angular CLI**
> É uma ferramenta que auxilia na hora de constuir um projeto usando Angular

- **Instalando**
``` powershell
npm install -g @angular/cli
```

- **Usando**
``` powershell
ng new NOME
```

- **Iniciando servidor**

    Entre na pasta do projeto antes de rodar. EX: cd NOME\

    - **ERRO** angular-devkit/build-angular/package.json
        - **Rodar** npm install --save-dev @angular-devkit/build-angular


``` powershell
ng serve --open
```

- **Rodando novas aplicações**
``` shell
npm install

ng update

npm update
```

---

## **Adicionando dependencias no projeto**
>Entre na pasta do projeto antes de rodar. EX: cd NOME\

``` shell
npm install bootstrap@4.1.1
```

- Dessa forma adicionamos a dependencia no node_modules, agora basta referenciar no **package.json** o arquivo

``` json
"styles": [
    "src/styles.css",
    "./node_modules/bootstrap/dist/css/bootstrap.min.css"
],
```


---

## **Estrutura**

- **src** 
    - **app** Repositorio onde salvamos os arquivos
        - **nome**
            - **Arquivo TS:**   nome.component.ts
            - **Classe:** NomeComponent
            - **HTML:** nome.component.html
            - **CSS:** nome.component.css
            - **Service:** nome.service.ts
            - **Entity:** nome.ts
            - **Module:** nome.module.ts

- **angular.json** Contem configurações do projeto
    - **"styles":** Define arquivos de css comuns no projeto
    - **"scripts":** Define arquivos de js comuns no projeto
- **package.json** Contem as dependencias do projeto

---

## **Tipando**
> Entidades para nosso código

- **Criando**
``` ts
export interface Nome {
    id:number;
    postDate:Date;
    url:string;
    description:string;
    allowComments:boolean;
    likes:number;
    comments:number;
    userId:number;
}
```
---

## **Componentes**
> Tudo funciona como uma componente que deve ser renderizado dentro da pagina e obrigatoriamente ele tem que pertencer a um modulo

- **Criando** Lembre de adicionar no Module após criar
``` ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./nav-menu.component.css']
})
```

- **Criando via terminal**
``` shell
ng generate component CAMINHO/nome
```

- **Usando**
``` html
<body>
    <app-root>Loading...</app-root>
</body>
``` 

### **- Module**
> Atribui os componentes no "@NgModule" para ele ser visivel dentro da aplicação 

- **Usando**
``` ts
...
import { NomeComponent } from './nome/nome.component';

@NgModule({
    declarations: [
        NomeComponent,
...
```

- **Criando**

    Podemos criar um Module para agrupar componentes que fazer parte de um mesmo serviço. Lembrando que temos que adicionar a referencia no modulo principal da aplicação

``` ts
import { NgModule } from "@angular/core";

@NgModule({
    declarations: [ NomeComponent ], //seria um atributo privado
    exports: [ NomeComponent ], //esse torna o modulo publico
    imports: [CommonModule] // Biblioteca derivada do **BrowserModule** que o **app.component.ts** importa, ela é necessária para transformar codigos de Angular (NgIf, NgFor, NgForOf etc), em HTML
})
export class NomesModule {}

// Adicionando referencia no Modulo principal
...
import { NomesModule } from './nome/nome.module';

@NgModule({
    declarations: [
        ...
    ],
    imports: [
        BrowserModule,
        NomesModule
    ],
...
```

- **Criando via terminal**
``` shell
ng generate module nome
```

### **- Ciclo de vida**
> Metodos default ao iniciar o componente

- **ngOnInit**

``` ts
import {component, input, OnInit} from @ 'angular/core';

export class NomeComponent implements OnInit{

    ngOnInit(): void{
    ...
        // Codigo para rodar ao iniciar o componente
    ...
    }

...
}
```

- **ngOnChange**
> Recebe todas as mudanças dos InboundPropreties


``` ts
import {component, input, OnChanges, SimpleChanges} from @ 'angular/core';

export class NomeComponent implements OnChanges{
    @input() nomes: Nome[] = [];
    ngOnChanges(changes: SimpleChanges): void{
        // Valida se houve uma alteração nesse input
        if (changes.nomes)
        {

        }
    }

...
}
```
### **- ng-content**
> Quando chamamos um componente podemos incluir um conteudo dentro dele, para isso funcionar precisamos dizer no HTML onde ele vai renderizar esse conteudo que pode receber

- **Criando**
``` ts
<div>
<ng-content></ng-content>
</div>
```

- **Usando**
``` ts
<my-component> <h2>Olá</h2> </my-component>
```

 ### **- Diretiva**
> Podemos criar um componente para usar como diretiva ao instanciar outros componentes

``` ts
import { Directive, ElementRef, HostListener, Renderer, Input } from '@angular/core';

// Define que é uma diretiva e o nome para chamar ela
@Directive({
    selector: '[apDarkenOnHover]'
})
export class DarkenOnHoverDirective { 

    constructor(
        private el: ElementRef,
        private render: Renderer
    ) {}

    // HostListener captura um evento do dom
    @HostListener('mouseover')
    darkenOn() {
        this.render.setElementStyle(this.el.nativeElement, 'filter', 'brightness(20%)');
    }

    @HostListener('mouseleave')
    darkenOff() {
        this.render.setElementStyle(this.el.nativeElement, 'filter', 'brightness(100%)');
    }
}
```

- **Usando**
``` ts
...
<div class="col-4" apDarkenOnHover>
...
```
---

## **Data Binding**
> Envia uma informação do Componente para o HTML

- **Criando**
``` ts
export class NOMEComponent {
  NomeVariavel = 'app';
}
```

- **Usando**
``` ts
{{ NomeVariavel }}
```

### - **One-Way DataBiding**
> Dessa forma podemos definir valores para atributos de tags html

- **Criando**
``` ts
export class NOMEComponent {
  NomeVariavel = 'https://www.alura.com.br/assets/api/cursos/angular-fundamentos.svg';
}
```

- **Usando**
``` html
<img [src]="NomeVariavel" >
```

- **Array**
``` ts
NomeLista = [
    {
      NomeVariavel1: '',
      NomeVariavel2: ''
    },
    {
      NomeVariavel1: '',
      NomeVariavel2: ''
    }
  ];

// Adicionando itens para o array, dessa forma a tela vai pegar essa alteração
this.NomeLista = this.NomeLista.concat(novaLista);
```

### - **Inbound Properties**
> Ferramenta para poder passar um valor para componentes quando é chamado

- **Criando**
``` ts
import { Component, Input } from "@angular/core";

@Component({
    selector: 'ap-nome',
    templateUrl: 'nome.component.html'
})
export class NomeComponent {

    @Input() description='';
    @Input() url='';
}
```

- **Usando**
``` ts
<ap-nome url="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Sultan_the_Barbary_Lion.jpg/440px-Sultan_the_Barbary_Lion.jpg" description="Leão"></ap-nome>
```

---
## **Event Binding**
> Envia uma informação do HTML para o Component
- **Criando**
``` ts
<div class="text-center mt-3 mb-3">
    <form>
        <input
            class="rounded"
            type="search"
            placeholder="search..."
            autofocus
            (keyup)="filter = $event.target.value"
            >
    </form>
</div>
{{ filter }}
```
### **- Criando um novo evento**
> Podemos criar um novo evento e definir seu funcionamento
- **Criando**
``` ts
import { Component, OnInit, OnDestroy, Output, EventEmitter, Input } from '@angular/core';
...

export class SearchComponent implements OnInit, OnDestroy {
    
    @Output() onTyping = new EventEmitter<string>();
    ngOnInit(): void {
        this.debounce
        .pipe(debounceTime(300))
        .subscribe(filter => this.onTyping.emit(filter));
    } 
...   

```

- **Usando**
``` ts
<ap-nome 
    (onTyping)="filter = $event">
</ap-nome>
```

---
## **Service**

### **- HTTP**
> Como utilizar recursos **HTTP**

- **Adicionando Modulo**
``` ts
import { HttpClient } from '@angular/common/http';

...
@NgModule({
    declarations: [
        ...
    ],
    imports: [
        BrowserModule,
        NomesModule
        // Esse imports definq que quando uma classe dentro do projeto que tiver o import necessário (import { HttpClient } from '@angular/common/http';) podemos solicitar para o servidor o HttpClient que o Angular vai saber responder
    ],
...
```

- **Criando**
``` ts
import { HttpClient } from '@angular/common/http';

export class NomeComponent {

    nomeLista = [];
    constructor(http: HttpClient) {
    console.log(http);
    }

}
```

- **Get**
``` ts
// subscribe pega o retorno

import { HttpClient } from '@angular/common/http';

export class NomeComponent {
    photos: Object[] = [];

    constructor(http:HttpClient) {
       http
        .get<Object[]>('http://localhost:3000/flavio/photos')
        .subscribe(x => this.photos = x,
                        err => console.log(err));
    }
}
```
### **- Service**
- **Criando**
``` ts
import { HttpClient } from '@angular/common/http';

const API = "http://localhost:3000/";

@Injectable({ providedIn: 'root' }) 
// o @Injectable define a injeção de dependencia para esse cara
// o 'root' define que quando for criado vai ser no escopo raiz
export class NomeService {
        constructor(private http: HttpClient) {
            this.http = http;
        }

        listFromUser(userName: string) {
            return this.http
                                .get<Object[]>(userName + '/photos');
        }
}
```

- **Usando**
``` ts
// subscribe pega o retorno

export class NomeComponent {
    photos: Object[] = [];

    constructor(nomeService: NomeService) {        
    }

    ngOnInit(): void{
        this.nomeService
                .listFromUser('LG') 
                .subscribe(x => this.photos = x,
                                err => console.log(err));
    }
}
```
---

## **Laços de repetição**
### - **For**

- **Usando**
``` ts
NomeLista = [
    {
      NomeVariavel1: '',
      NomeVariavel2: ''
    },
    {
      NomeVariavel1: '',
      NomeVariavel2: ''
    }
  ];

// ------------------------------------------

<ap-photo
    *ngFor="let item of NomeLista"
    [url]="item.NomeVariavel1"
    [description]="item.NomeVariavel2"
>
</ap-photo>
```

---
## **Condicional**
- **if**
```ts
<p class="text-center text-muted" *ngIf="!nomes.length">
    Sorry, no photos
</p>

// if and else
<div class="text-center" *ngIf="hasMore; else messageTemplate">
  <button class="btn btn-primary">Load more</button>
</div>

<ng-template #messageTemplate>
  <p class="text-center text-muted">No more data to load</p>
</ng-template>
```


---
## **Rotas** Componente
- **Criando** app.routing.module.ts

     Componente de rotas que o app.module.ts vai herdar as rotas

``` ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule} from '@angular/router';

import { PhotoListComponent } from './photos/photo-list/photo-list.component';
import { PhotoFormComponent } from './photos/photo-form/photo-form.component';

const routes: Routes = [
// path: define a URL
// component: define quem vai responder a essa URL
    { path: 'user/flavio', component: PhotoListComponent },
    { path: 'p/add', component: PhotoFormComponent }
    { path: '**', component: NotFoundComponent }
];

@NgModule({
// define o de para de URL e Component
    imports: [
            RouterModule.forRoot(routes)
    ],
// Faz quem chamar esse Module herdar o RouterModule junto
    exports: [ RouterModule ]
})
export class AppRoutingModule { }
```

- **Adicionando Modulo**
``` ts
import { AppRoutingModule } from 'app.routing.module.ts';

...
@NgModule({
    declarations: [
        ...
    ],
    imports: [
        BrowserModule,
        AppRoutingModule
    ],
...
```

- **Adicionando Endereços** app.component.html
``` ts
// Adiciona
<router-outlet></router-outlet>
```

---
## **QueryParam**
- **Criando**
``` ts
...
const routes: Routes = [
    { path: 'user/:userName', component: PhotoListComponent },
    ...
];
...
```

- **Usando**
``` ts
...
import { ActivatedRoute } from '@angular/router';

export class NomeComponent {
...    

    constructor(private activatedRoute: ActivatedRoute) 
    { }

    ngOnInit(): void{
        const userName = this.activatedRoute.snapshot.params.userName;
    }
} 
...
```
---
## **Pipe**
- **Nativo**
    - **uppercase**
``` ts
// Modificando exibição
{{ NomeVariavel | uppercase }}
``` 

- **Criando** filter-by-param.pipe.ts
``` ts
// No componente
...
export class NomeComponent {
  filter: string = '';
...


// Criando o arquivo
import { Pipe, PipeTransform } from '@angular/core';
import { Nome } from '../nome/nome';

@Pipe({ name: 'filterByParam'})
export class FilterByParam implements PipeTransform {

    transform(nomes: Nome[], paramQuery: string) {
        paramQuery = paramQuery
            .trim()
            .toLowerCase();

        if(paramQuery) {
            return nomes.filter(x =>
                x.description.toLowerCase().includes(paramQuery)
            );
        } else {
            return photos;
        }
    }
}

// Adicionando referencia no Module
@NgModule({
    imports: [
            FilterByParam
    ],
```

- **Usando**
``` ts
<div class="text-center mt-3 mb-3">
    <form>
        <input
            class="rounded"
            type="search"
            placeholder="search..."
            autofocus
            (keyup)="filter = $event.target.value"
            >
    </form>
</div>

<ap-nomes [nomes]="nomes | filterByParam: filter"></ap-nomes>
```

---
## **Resolvers**
> Seria uma forma de trazer os dados antes de renderizar o componente

- **Criando** nome.resolver.td
``` ts
import { Injectable } from '@angular/core';
import { Resolve, RouterStateSnapshot, ActivatedRouteSnapshot } from '@angular/router';
import { Observable } from 'rxjs';

import { NomeService } from '../nome/nome.service';
import { Nome } from '../nome/nome';

@Injectable({ providedIn: 'root'})
export class NomeResolver implements Resolve<Observable<Nome[]>>{

    constructor(private service: NomeService) {}

    resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Nome[]> {
        const userName = route.params.userName;
        return this.service.listFromUserPaginated(userName, 1);
    }
}
```

- **Usando**
``` ts
...
import { NomeResolver } from './nomes/nomes/nome.resolver';

const routes: Routes = [
    { 
        path: 'user/:userName', 
        component: NomeComponent,
        resolve: {
            nomeParamResolve: NomeResolver
        }
    },
...

// No componente
export class NomeComponent implements OnInit{

  nomes: Nome[] = [];
  filter: string = '';
  constructor(
    private activatedRoute: ActivatedRoute
  ) { }

  ngOnInit(): void {
    this.nomes = this.activatedRoute.snapshot.data['nomeParamResolve'];
  }
```

---
## **Debounce**
> Forma de tratar um parametro quando é preenchido antes de fazer uma requisição

- **Criando**
``` ts
import { Subject } from 'rxjs';
import { debounceTime } from 'rxjs/operators';

...
export class NomeComponent implements OnInit, OnDestroy {

  filter: string = '';
  debounce: Subject<string> = new Subject<string>();
 
...
// subscribe pega o retorno

  ngOnInit(): void {
    this.debounce
      .pipe(debounceTime(300))
      .subscribe(x => this.filter = x);
  }

  ngOnDestroy(): void {
    this.debounce.unsubscribe();
  }
  
  ...
```

- **Usando**
``` ts
<div class="text-center mt-3 mb-3">
    <form>
        <input 
            class="rounded" 
            type="search" 
            placeholder="search..." 
            autofocus
            (keyup)="debounce.next($event.target.value)"
            >
    </form>
</div>

<ap-nomes [nomes]="nomes | filterByParam: filter"></ap-nomes>
```

---