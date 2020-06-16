# **Design Patterns**
> Trata-se de uma definição de alto nível a ser seguida que possibilita o crescimento do código sem grandes alterações.
- **Documentação**
    - https://www.opus-software.com.br/design-patterns/#:~:text=Design%20Patterns%20GoF,)%2C%20Behavioral%20(Comportamental).

## **Agruparam os Design Patterns em três tipos diferentes:** 
- **Creational**, Criação
- **Structural**, Estrutura
- **Behavioral**, Comportamental

---

### **Caracteristicas** 

- **Vantagens**
> Simplificar o crescimento do código

- **Desvantagem**
> Crescimento da complexidade do código e escrever mais na hora da implementação

---
Padrões seguidos a partir do livro "Design Patterns: Elements of Reusable Object-Oriented Software"
## **Padrões Behavioral**
### **Strategy**, Behavioral
> Se acrescentar ou remover um objeto do codigo gera alteração de outros metodos essa aplicação precisa do Design Partterns. A ideia é que alterações no codigo que não mudem a função principal não devem gerar grandes mudanças

- **Identificando**

``` c#
public main (CLASSE_ENTRADA entrada)
{
    // CALCULO GENERICO DA ENTRADA COM VALOR X
    // MESMO CALCULO GENERICO DA ENTRADA COM VALOR Y
    // MESMO CALCULO GENERICO DA ENTRADA COM VALOR Z
    // POUCAS VARIACOES CALCULO GENERICO DA ENTRADA COM VALOR W
    // Estamos repitindo codigo e gerando validações poluindo o codigo
}
```

- **Solução**
```c#
// Cria uma interface
public interface GENERALIZA
{
    double Retorna(CLASSE_ENTRADA entrada);
}

// Transforma as condições em uma classe
public class A : GENERALIZA
{
    public double Retorna(CLASSE_ENTRADA entrada)
    {
        // CALCULO GENERICO DA ENTRADA COM VALOR X
    }
}

// Essa classe é responsavel por receber a entrada e chamar a CLASSE
public class RealizadorCalculo
{
    public void CALCULADOR (CLASSE_ENTRADA entrada, GENERALIZA entidade)
    {
        double retorno = GENERALIZA.Retorna(entrada);
        Console.WriteLine(retorno);
    }
}

// Chamando no que seria o main da aplicação
GENERALIZA saida = new A();
RealizadorCalculo calc = new RealizadorCalculo()
cal.CALCULADOR(CLASSE_ENTRADA entrada, saida);
```

### **Chain of Responsibility**, Behavioral 
> Se os objetos vao ser chamados em cadeia dependendo de um valor passado o correto é criar um Objeto que vai iniciar essas tratativas e nele criamos os objetos em

- **Identificando**

``` c#
public main (CLASSE_ENTRADA entrada)
{
    if (entrada.valor > 0)
    {
        // Codigo
    }
    else if (entrada.valor < 0)
    {
        // Codigo
    }
    else if (entrada.valor = 0)
    {
        // Codigo
    }
    else if...
}
```

- **Solução**

``` c#
// Cria uma interface
public interface GENERALIZA
{
    double Retorna(CLASSE_ENTRADA entrada);
}

// Cada if se torna um objeto
public class MaiorQueZero : GENERALIZA
{
    // Se nao entrar no if vai para proxima interação
    public GENERALIZA Proximo { get; set; }

    public double Retorna(CLASSE_ENTRADA entrada)
    {
        if (entrada.valor > 0)
        {
            return // Codigo            
        }
        return Proximo.Retorna(entrada);
    }
}

// Cada if se torna um objeto
public class MenorQueZero : GENERALIZA
{
    // Se nao entrar no if vai para proxima interação
    public GENERALIZA Proximo { get; set; }

    public double Retorna(CLASSE_ENTRADA entrada)
    {
        if (entrada.valor < 0)
        {
            return // Codigo            
        }
        return Proximo.Retorna(entrada);
    }
}

// A corrente tem que ter um fim, então criamos um objeto que herda de GENERALIZA apenas para ser o fim dessas requisições
public class Fim : GENERALIZA
{
    public double Retorna(CLASSE_ENTRADA entrada)
    {
        return 0;
    }
}

// Agora criamos uma classe que sera a responsavel por iniciar as chamadas 
public class Calculador 
{
    public double calcula(CLASSE_ENTRADA entrada)
    {
        GENERALIZA obj1 = new MaiorQueZero();
        GENERALIZA obj2 = new MenorQueZero();
        GENERALIZA obj3 = new Fim();

        obj1.Proximo = obj2;
        obj2.Proximo = obj3;

        return obj1.Retorna(entrada);
    }
}
```


### **Template Method**, Behavioral 
> Serve para definirmos um padrão quando uma varias classes implementam o mesmo comportamento no metodo.


- **Identificando**

``` c#
// Objeto generico A
public class A
{
    public double calcula(double valor)
    {
        if (verifica_valor(valor))
        {
            // Codigo A
        }
        return 0;
        
    }

    private bool verifica_valor(valor)
    {
        if (valor > 0)
            return true;
        return false;
    }
}

// Objeto generico B
public class B
{
    public double calcula(double valor)
    {
        if (verifica_valor(valor))
        {
            // Codigo B
        }
        return 1;
    }

    private bool verifica_valor(valor)
    {
        if (valor < 0)
            return true;
        return false;
    }
}
```

- **Soluçâo**
``` c#
public abstract class Template 
{
    public double calcula(double valor)
    {
        if (verifica_valor(valor))
        {
            return tratativa(double valor);
        }
        return 0;
    }

    protected  abstract bool verifica_valor(double valor);
    protected  abstract double tratativa(double valor);
    protected  abstract double tratativaRetorno(double valor);
}

// Objeto generico A que extende de Template
public class A : Template
{
    private double tratativa(double valor)
    {
        // Codigo A
    }

    private double tratativaRetorno(double valor)
    {
        return 1;
    }

    private bool verifica_valor(double valor)
    {
        return valor > 0? true : false;
    }

}

// Objeto generico B que extende de Template
public class B : Template
{
    private double tratativa(double double valor)
    {
        // Codigo B
    }

    private double tratativaRetorno(double valor)
    {
        return 0;
    }

    private bool verifica_valor(double valor)
    {
        return valor > 0? true : false;
    }
}
```

### **State**, Behavioral 
> Quando temos estados para um objeto (Como os id's de um perfil) e vamos definir ou alterar podemos criar um objeto para cada estado que herda de uma interface com as configurações (seriam os metodos), para avançar ou voltar um estagio aplicando as validações.

### **Observer**, Behavioral 
> Sao eventos que tem que ser executados após uma ação no objeto, eles devem ser criados a parti e receber o objeto na sua chamada para iniciar o evento. Um exemplo seria um log por exemplo que é um evento que deve ser instanciado por exemplo somente no delete.

### **Memento**, Behavioral 
> Trata-se de um padrão de codigo para pegar o valor de um objeto antes que ele seja alterado para criar uma lista (ou seja um historico) das suas alterações possibilitando até voltar um estado se necessario

### **Command**, Behavioral
> Usamos ele quando temos que separar os comandos que serão executados para uma entidade em outras classes. Eu acredito que essa ja é a melhor tratava, até para evitar que junto da entidade fique algum "lixo" dos metodos que usamos na hora de enviar.

### Interpreter (DSLs), Behavioral
> Quando temos expressões que devem ser avaliadas, e a transformamos em uma estrutura de dados, e depois fazemos com que a própria árvore se avalie, damos o nome de Interpreter.

### Visitor, Behavioral 
> Quando temos uma árvore, e precisamos navegar nessa árvore de maneira organizada, podemos usar um Visitor



---

## **Padrões Structural**

### *Decorator*, Structural 
> É a criação de um construtor base na classe abstrata que as demais vao herdar que ao receber um valor para inicia chama outro metodo que vai seguir uma tratativa

- **Identificando**

``` C#
public class main()
{
    double valor = 0;

    CLASSE a = new CLASSE();
    CLASSE b = new CLASSE();

    valor += a.Calcula(valor);
    valor += b.Calcula(valor);

    Console.Write(valor); 
}
```

- **Solução**
``` c#
public abstract class TEMPLATE()
{
    public TEMPLATE outro { get; set; }

    public TEMPLATE(TEMPLATE Outro)
    {
        this.outro = Outro;
    }

    public TEMPLATE()
    {
        this.outro = null;
    }

    public override double Calcula(double valor);
    {
        return CalculaOutro();
    }

    protected double CalculoOutro(double valor);
    {
        if (this.outro == null) return 0;
        return this.outro.Calcula();
    }
}

public class A : TEMPLATE
{
    public virtual double Calcula();
    {
        double retorno = 0;
        // Calculo de A
        return retorno + base.Calcula();
    }
}
```

### **Flyweight (Singleton)**, Structural 
> Quando temos objetos repitidos sendo criados mais de uma vez podemos criar uma lista com todos objetos, ou somente este, e apenas referenciar o mesmo objeto varias vezes em vez de criar objetos iguais.


### **Adapter**, Structural
> Usado quando temos que converter um objeto de de um sistema legado para uma nova arquitetura.

### **Façade**, Structural
> Usada para isolar apenas ações daquele objeto 

###  Bridge, Structural 
> Quando temos uma hierarquia de classes que é responsável por diversas características do sistema (Mensagem e a Ferramenta de Envio da mensagem, no exemplo), podemos utilizar o padrão bridge para separar as características em diversas hierarquias ligando-as através da composição de classes.

``` c#
// Criando
public interface IEnviador
{
    void Envia(IMensagem);
}

public interface IMensagem
{
    IEnviador Enviador { get; set; }

    void Envia();

    string Formata();
}

// Usando 
IEnviador enviador = new EnviaPorEmail();
IMensagem mensagem = new MensagemAdministrativa("victor");
mensagem.Enviador = enviador;

mensagem.Envia();
```

---
## **Padrões Creational**

### **Builder**, Creational 
> Automatiza a atribuição dos elementos (logica de criação) de uma classe dentro de outra classe (nome padrão dela é NOMEBuilder) através de metodos que tem como objetivo validar o valor de entrada e tratar os dados antes de atribuir. Muito usado para centralizar a complexidade de alguns objetos 


### **Factory**, Creational
> Com esse padrão nos isolamos um trexo de codigo que vai ser reutilizado por diversas aplicações. Um exemplo de aplicação e a criação de uma classe para conectar ao banco de dados.

### **Singleton**, Creational
> Nos criamos um ponto de acesso aos comandos de uma entidade, funciona da mesma forma que usamos em arquitetura de camadas quando referenciamos o Bll no WCF.Service o WCF e um Singleton

--

## **Arquiteturas**
- Arquitetura em camadas 
    - Interface <> Fachada <> Negócio <> Dados
- MVC
    - View <> Controller <> Model