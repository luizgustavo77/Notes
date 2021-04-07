# **Angular**
> Framework para front-end

### **Estrutura**

- **SRC** Repositorio onde salvamos os arquivos
- **angular.json** Contem configurações do projeto
    - **"styles":** Define arquivos de css comuns no projeto
    - **"scripts":** Define arquivos de js comuns no projeto
- **package.json** Contem as dependencias do projeto

- **Nomenclatura**
    - **Arquivo TS:**   nome.component.ts
    - **Classe:** NomeComponent
    - **HTML:** nome.component.html
    - **CSS:** nome.component.css
---
## **Componentes**
> Tudo funciona como uma componente que deve ser renderizado dentro da pagina e obrigatoriamente ele tem que pertencer a um modulo

- **Criando**
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


### - **Data Binding**
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
