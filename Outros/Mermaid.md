# **Mermaid**
> Linguagem para especificar diagramas, que funciona com o MarkDown,
[Site Oficial](https://github.com/mermaid-js/mermaid)
- **Criando no MarkDown:**

\``` mermaid    
TIPO DE FLUXO;   
CAMINHO   
CAMINHO   
CAMINHO   
...   
\```   

---

## **Themes:**

- default
- forest
- dark
- neutral

---

## **Live Editor:**

[Abrir](https://mermaidjs.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ2FudHRcbnNlY3Rpb24gU2VjdGlvblxuQ29tcGxldGVkIDpkb25lLCAgICBkZXMxLCAyMDE0LTAxLTA2LDIwMTQtMDEtMDhcbkFjdGl2ZSAgICAgICAgOmFjdGl2ZSwgIGRlczIsIDIwMTQtMDEtMDcsIDNkXG5QYXJhbGxlbCAxICAgOiAgICAgICAgIGRlczMsIGFmdGVyIGRlczEsIDFkXG5QYXJhbGxlbCAyICAgOiAgICAgICAgIGRlczQsIGFmdGVyIGRlczEsIDFkXG5QYXJhbGxlbCAzICAgOiAgICAgICAgIGRlczUsIGFmdGVyIGRlczMsIDFkXG5QYXJhbGxlbCA0ICAgOiAgICAgICAgIGRlczYsIGFmdGVyIGRlczQsIDFkIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifX0)

---

## **Tipos:**
### **Flowchart** Para fluxos simples  
- **Fluxo:**   
    **-->**

\``` mermaid  
graph TD  
 A-->B  
 A-->C  
 B-->D  
 C-->D  
\```  
``` mermaid
graph TD
A-->|text|B
A-->C
B-->D
C-->D
```
### **Sequence diagram** Para Fluxos complexos, e aceita quebra de linha com \<br>  
- **Fluxo:**  
    **->>: DESCRICAO** Continuo  
    **-->>: DESCRICAO** Pontilhado

- **Objetos:**  
    **participant NOME**

- **Laços de Repetição:**  
    **loop TITULO**  
        **OBJETO->>OBJETO: DESCRICAO**  
    **end**  

- **Anotações**  pode ser adicionado a direita ou esquerda do Objeto   
    **Note right/left of OBJETO: DESCRICAO**


\``` mermaid  
sequenceDiagram  
    participant Alice  
    participant Bob  
    Alice->>John: Hello John, how are you?  
    loop Healthcheck  
        John->>John: Fight against hypochondria  
    end  
    Note right of John: Rational thoughts \<br/>prevail!  
    John-->>Alice: Great!  
    John->>Bob: How about you?  
    Bob-->>John: Jolly good!  
\```
``` mermaid  
sequenceDiagram  
    participant BLL  
    participant NHibernate  
    BLL->>WEB: PROXY  
    loop Healthcheck  
        WEB->>WEB: Transações  
    end  
    Note right of WEB: MVC <br/> prevail!  
    WEB-->>BLL: Great!  
    WEB->>NHibernate: PROXY?  
    NHibernate-->>WEB: DONE!  
```

### **Gantt diagram** Diagrama de tempo  
- **Formato da data**  
    **dateFormat YYYY-MM-DD**    

- **Titulo**  
**title NOME**

- **Desprezar**   
**excludes weekdays**

- **Objetos**  
**section NOME**

- **Tasks** Sempre separado por virgula e nenhuma definição e obrigatoria  
**NOME: STATUS, ID, POSIÇÃO, PERIODO**
    - **STATUS** done, active e crit. Altera a aparencia
    - **ID** Define um nome para identificar a Task
    - **POSIÇÃO** Podemos atribuir uma Task depois da outra com "after ID"
    - **PERIODO** Podemos atribuir com inicio em fim ou so a duração
        - **Inicio/Fim**   
        **, 2014-01-06, 2014-01-08**  
        **, 2014-01-09, 3d**
        - **Duração**  
        **, 5d**  
        **, 48h**
 
\``` mermaid  
gantt  
dateFormat  YYYY-MM-DD  
title Adding GANTT diagram to mermaid  
excludes weekdays   

section A section  
Comp. task :done, des1, 2014-01-06,2014-01-08   
Active task :active, des2, 2014-01-09, 3d  
Future task : des3, after des2, 5d  
Future task2 : des4, after des3, 5d  
\```
``` mermaid
gantt 
dateFormat  YYYY-MM-DD
       title Adding GANTT diagram functionality to mermaid

       section A section
       Completed task            :done,    des1, 2014-01-06,2014-01-08
       Active task               :active,  des2, 2014-01-09, 3d
       Future task               :         des3, after des2, 5d
       Future task2              :         des4, after des3, 5d

       section Critical tasks
       Completed task in the critical line :crit, done, 2014-01-06,24h
       Implement parser and jison          :crit, done, after des1, 2d
       Create tests for parser             :crit, active, 3d
       Future task in critical line        :crit, 5d
       Create tests for renderer           :2d
       Add to mermaid                      :1d

       section Documentation
       Describe gantt syntax               :active, a1, after des1, 3d
       Add gantt diagram to demo page      :after a1  , 20h
       Add another diagram to demo page    :doc1, after a1  , 48h

       section Last section
       Describe gantt syntax               :after doc1, 3d
       Add gantt diagram to demo page      :20h
       Add another diagram to demo page    :48h
```
### **Pie chart diagrams** Grafico de Pizza  
- **Titulo**    
    **title NOME**    
- **Objetos**  
**"NOME": PORCENTAGEM**  
**"NOME": PORCENTAGEM**  
**...**

\``` mermaid  
pie  
title Pets adopted by volunteers  
    "Dogs" : 386  
    "Cats" : 85  
    "Rats" : 15   
\```  
``` mermaid
pie 
title Pets adopted by volunteers
    "Dogs": 386
    "Cats" : 85
    "Rats" : 15 
```

### **Class diagrams** Fluxo complexo
- **Visibilidade**   

| Simbolo | Modificadores  |   
| --- | --- |   
| + | Público |   
|- |Privado|   
|# |Protegido|   
|~ |Pacote|   

- **Fluxo**  
**NOME <|-- NOME**  

|Simbolo|	Descrição|
| --- | --- |     
|<\| - |	Herança  |
|* -	|Composição|  
|o--|	Agregação|  
|->|	Associação|  
|-|	Link (sólido)|  
|..>|	Dependência|  
|.. \|>|	Realização|  
|..|Link (tracejado)|  

- **Descricao**  
**classA <|-- classB : DESCRICAO**

- **Objetos**  
 **class NOME{**  
          **VISIBILIDADE VARIAVEL**  
          **VISIBILIDADE METODO()**  
      **}**

- **Relações**  
**NOME "SIMBOLO" --> "SIMBOLO" NOME**

|Simbolo|Descricao|
|---|---|
|0..1 |Zero ou um|
|1 |Apenas 1|
|0..1| Zero ou um|
|1..* |Um ou mais|
|* |Muitos|
|n n |{onde n> 1}|
|0..n |zeor para n {onde n> 1}|
|1..n |um para n {onde n> 1}|
   

\``` mermaid  
classDiagram   
      Animal o-- Duck : BEST  
      Animal .. Fish  
      Animal "1" <|-- "*" Zebra  
      class Animal{   
         +String gender  
         +isMammal()  
         +mate()   
     }  
      class Duck{  
          +String beakColor  
          +swim()  
          +quack()  
      }  
      class Fish{  
          -int sizeInFeet  
          -canEat()  
      }  
      class Zebra{  
          +bool is_wild  
          +run()  
      }  
\```  

``` mermaid
classDiagram
      Animal o-- Duck : BEST
      Animal .. Fish
      Animal "1" <|-- "*" Zebra
      class Animal{ 
         +String gender
         +isMammal()
         +mate() 
     }
      class Duck{
          +String beakColor
          +swim()
          +quack()
      }
      class Fish{
          -int sizeInFeet
          -canEat()
      }
      class Zebra{
          +bool is_wild
          +run()
      }
```
