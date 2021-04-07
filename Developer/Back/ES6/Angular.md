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

``` powershell
ng serve --open
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

- **angular.json** Contem configurações do projeto
    - **"styles":** Define arquivos de css comuns no projeto
    - **"scripts":** Define arquivos de js comuns no projeto
- **package.json** Contem as dependencias do projeto

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

- **Usando**
``` html
<body>
    <app-root>Loading...</app-root>
</body>
``` 

### - **Module**
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
    exports: [ NomeComponent ] //esse torna o modulo publico
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

### - **Ciclo de vida**
> Metodos default ao iniciar o componente
---

## **Data Binding**
> Adiciona uma variavel dentro do dom para ter um conteudo de uma tag

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
## **HTTP**
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

---

## **Service**

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
export class NomeComponent {
    photos: Object[] = [];

    constructor(nomeService: NomeService) {
        nomeService.listFromUser('LG') 
        .subscribe(x => this.photos = x,
                        err => console.log(err));
    }
}
```

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

