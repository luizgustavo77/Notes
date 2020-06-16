# **Compiladores**
> Transforma linguagem "humana" em linguagem de maquina 
``` mermaid
graph TD
CódigoFonte-->Tradutor
Tradutor-->ProgramaIntermediário 
ProgramaIntermediário -->Interpretador
Dados-->Interpretador
Interpretador-->Resultado
```

### **Pré-Compiladores**
> Simplifica parte do codigo para evitar escrita de codigo desnecessaria
- **Exemplo:** Pro-C, para transformar linguagem c em SQL

### **Tradutor**
> Facilita a escrita de codigo
- **Exemplo:** TypeScript para Javascript

### **Tipos de Linguagem**
- **Interpretada:** É compilada toda vez que é lida, pode ter erro na hora de rodar
- **Compilada:** Gera um executavel, não tem erros pois ja foi testado 

### **Json & XML**
> Texto a ser traduzido para codigo, mas devemos seguir as regras da linguagem.
- **Parser:** Metodo para Transformar o txt em codigo, não e perfeita depende do framework que usamos para isso para dar certo em algumas tags
