# **SOLID**
> Busca criar código de qualidade com facil manutenção, aqui vemos muito sobre a idéia de "cheiro ruim" no código e como previnir isso. 

### **Conceitos**
> _Quando colocamos um codigo em produção assinamos embaixo sobre a qualidade daquele codigo..._

- **DRY** - Dont Repeat Yourself
    - Não da _"CTRL+C & CTRL+V"_ no seu código...

- **Y.A.G.N.I.** - You Aint Gonna Need It
    - Não implemente funcionalidades que ainda não foram solicitadas!
---
### **S:** single responsability principle
- **Métodos** e **Classes** devem ter uma unica responsabilidade

---
### **O:** Open-Close Principle
- Criamos o código de uma forma que o tratamento de dados fica em um unico lugar. Dessa forma qual quer alteração pode ser feita ali e vai surgir efeito em toda aplicação. 

---
### **L:** Liskov Substitution Pinciple
- Não crie metodos defina interface que não está em uso, por mais que no futuro você possa usar elas deixei para criar quando houver a necessidade

---
### **I:** Interface Segregation Principle
- Tem que usar todas as referencias da interface usada 

---
### **D:** Dependency Inversion Principle
- Remove a necessidade de instanciar na mão objetos que são dependencias para realizar aquela ação
---
