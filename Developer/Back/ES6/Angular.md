# **Angular**
> Framework para front-end

### **Estrutura**
- **SRC** repositorio onde salvamos os arquivos
    - 

### **Componentes**
> Tudo funciona como uma componente que deve ser renderizado dentro da pagina

- **Criando**
``` html
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

### **Data Binding**
> Adiciona uma variavel dentro do dom para ter um conteudo dinamico

- **Usando**
``` html
{{ NomeVariavel }}
```
