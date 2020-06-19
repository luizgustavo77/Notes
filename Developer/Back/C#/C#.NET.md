# **C#.NET**
> Linguagem feita como parte da plataforma .NET 

## **Definições**
* **C#**  Tinguagem
* **ASP** Tecnologia
* **.Net** Framework
* **ASP.Net** Tecnologia utilizando Framework.Net

## **Canal Youtube para aulas**
* [C# Ui Academy](https://www.youtube.com/channel/UCigNaporFrKIPHiF1FcWfwA)
---
## **Android IOS**
* Xamarim
---
## **Interface**
* WPF
* Winsows Form
* Web Form
---
## **Jogos**
* Unity
---
## **Compiladores**
* Ride
* MonoDevelop
* Visual Studio
---
## **Convencao de Codigo**

|Estrutura|	Nomenclatura|	Exemplo|
|---|---|---|
|Classe	|Pascal	|PessoaJuridica|
|Interface|	I + Pascal|	ICliente
Método Público , Propriedades|	Pascal|	NomeCompleto()
Método Privado|	Camel Case	|calculaDesconto()
Variável Pública|	Pascal|	SobreNome
Variável Privada	|Camel Case|	impostoPredial
Constantes|	Maiúsculas com sublinhado   	    |VALOR_DESCONTO  
---

## **Atalhos**
|Atalho|Descricao|
|---|---|
|prop + tab  + tab| cria variavel|
|ctor + tab + tab|cria construtor|
|shit+f9|quick view| 
|ctrl+k+c|Comentar|
|ctrl + k + d|identar |
|shift + alt|selecionar |
|ctrl+F12|Abrir local de Interface|

## **Escapes**
|Sequência de escape |	Nome do caractere	|
|---|---|
\'|	Aspas simples	
\"|	Aspas duplas	
\\|	Barra invertida	
\0|	Nulo	
\a|	Alerta	
\b|	Backspace	
\f|	Avanço de página	
\n|	Nova linha	
\r|	Retorno de carro	
\t|	Tabulação horizontal	
\v|	Tabulação vertical	
\u|	Sequência de escape Unicode (UTF-16)	 
\U|	Sequência de escape Unicode (UTF-32)
\x|	Sequência de escape Unicode semelhante a "\u", exceto pelo comprimento variável

- **Adicionar imagens**
``` c#
/// <image url = "$(ProjectDir)/NOME.png"/>
``` 
---
## **Comentarios**
> Existem outros atributos para criar uma "Documentacao" quando se trata de cometarios para um metodo, atributos esse onde podemos por exemplo referenciar variaveis por exemplo, tudo para deixar a documentacao completa disponivel em [Documentacao Microsoft](https://docs.microsoft.com/pt-br/dotnet/csharp/codedoc).
``` c#
// uma linha
/* abre e fecha comentatoio
*/
/// comentario para metodo 
```
---
## **Variaveis**
|Tipo de dados|	Intervalo|
|---|---|
byte	|0 ... 255
sbyte	|-128 ... 127
short	|-32,768 ... 32,767
ushort	|0 ... 65,535
int	|-2,147,483,648 ... 2,147,483,647
uint	|0 ... 4,294,967,295
long	|-9,223,372,036,854,775,808... 9,223,372,036,854,775,807
ulong	|0 ... 18,446,744,073,709,551,615
float	|-3.402823e38 ... 3.402823e38
double	|-1.79769313486232e308 ... 1.79769313486232e308
decimal|	-79228162514264337593543950335... 79228162514264337593543950335
char	|U+0000 ...  U+ffff
var | Aceita todos os tipos inclusive objetos e identifica na hora oque vai se tornar
object | classe que todas as classes herdam, dela podemos atribuir qual quer classe
string | 1.000.000.000 caracteres
DateTime | Para datas
bool | true - false

> Para tornar uma variavel constante basta adicionar um "const" no inicio no local onde e criada

> Para pegar o nome da VARIAVEL podemos usar o "nameof()"

> Use ".Replace('.', ' ,');" sempre que converter um string para **DOUBLE** porque se nao 2.50 (dois e cinquenta) vira 250 (duzentos e cinquenta)

- **Enum**
> Opcao para ter valores constantes

```c#
enum DiasDeTrabalho {
  Seg = 0, 
  Ter = 1, 
  Qua = 2, 
  Qui = 4, 
  Sex = 8, 
  Sab = 16,
  Dom = 32
}
```

- **Dynamic**
> A existência dos membros de um objeto dynamic são verificados somente em tempo de execução.
``` c#
public void Executar()
{
   object objeto = 1;
   //objeto = objeto + 3; GERA UM ERRO

   dynamic dinamico = 1;
   dinamico = dinamico + 3; // Roda normal 
   Console.WriteLine(dinamico);

}
```
---

## **Modificadores**
|Modificador|	Funcionamento|
|---|---|
public|	O acesso não é restrito.
protected	|O acesso é limitado às classes ou tipos derivados |daclasse que a variável está.
Internal	|O acesso é limitado ao conjunto de módulos(assembly) corrente.
protected internal	|O acesso é limitado ao conjunto corrente ou tipos derivados da classe recipiente.
private|	O acesso é limitado à classe que a variável está.
sealed | Proibe a heranca a partir desta class

---
## **Executando o codigo**

- **Debug** Para vermos o codigo sendo executado tempo a tempo, abaixo os atalhos do modo
    - **F9** atribui um break point na linha
    - **F10** proxima interacao pulando metodos
    - **F11** proxima interacao ponto a ponto
    - **F5** proximo break point ou executa o restante do codigo
    - **Janelas** auxiliam o modo de debug
        - **Auto** variaveis em uso no durante a execucao daquele trexo
        - **Watch** podemos definir variaveis para monitorar
    - **Debug.Write** comando usando para escrever na janela de Output (ctrl + alt + o), roda somente no modo debug
    
- **Realease** executa sem as opcoes de debug

### **Ferramentas/Codigos para auxiliar a execucao**

- **Trace** Ferramenta que lanca informacoes no output, abaixo um exemplo de como adicionar o as informacoes de trace em um arquivo de saida
    - **Trace.WriteLine** Escreve
    - **Trace.AutoFlush** definindo true podemos garantir que as informacoes irao ser passadas para o trace
    - **EventLogTraceListener** Propriedade para lancar eventos no visualizador de eventos do Windows
    - **Tipos** Informacao, Erro e Aviso
``` xml
<configuration>
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />
        <remove name="Default" />
      </listeners>
    </trace>
  </system.diagnostics>
</configuration>
```
``` c#
// Tipos
Trace.TraceError("Meu erro");

//EventLogTraceListener
TraceListener NOME = new EventLogTraceListener("NOME DO PROJETO");
Trace.Listeners.Add(NOME);
Trace.AutoFlush = true;
```

- **TraceSource** Atualizacao do Trace
    - **SourceLevels** tipos de enventos 
    - **TraceEvent** lanca um evento
        - **TraceEventType** define tipo do evento
``` c#
TraceListener traceListener = new EventLogTraceListener("NOME DO PROJETO");
Trace.Listeners.Add(traceListener);
Trace.AutoFlush = true;

TraceSource traceSource = new TraceSource("NOME DO PROJETO", SourceLevels.All);
traceSource.Listeners.Add(traceListener);

traceSource.TraceEvent(TraceEventType.Information, 1001, "A aplicação iniciou.");
``` 
- **Stopwatch** Ferramenta para medir o tempo de execucao
```  c#
Stopwatch stopwatch = new Stopwatch();
stopwatch.Start();
// Codigo para executar
stopwatch.Stop();

var tempoDecorrido = stopwatch.ElapsedMilliseconds;

Console.WriteLine($"Tempo decorrido: {tempoDecorrido} milissegundos.");
``` 

-  **EventLog** Grava um evento no visualizador de eventos do windows, e util para verificar eventos do sistema 
``` c#
 if (!EventLog.SourceExists("MinhaFonte"))// podemos derificar eventos existentes
{
    EventLog.CreateEventSource("MinhaFonte", "Application"); // application e o tipo de evento
}

// Criando um evento
EventLog eventLog = new EventLog();
eventLog.Source = "MinhaFonte";
eventLog.WriteEntry("A aplicação terminou.", EventLogEntryType.Information, 1002);

// Codigo de como listar todos os eventos
EventLog eventLog = new EventLog();
foreach (EventLogEntry entrada in eventLog.Entries)
    Console.WriteLine($"Fonte: {entrada.Source}\nTipo: {entrada.EntryType}\nHora: {entrada.TimeWritten}\nMensagem: {entrada.Message}\n");
eventLog.Close();
``` 
---
## **Convert**
|Metodo|Descricao|
|---|---|
| ToBoolean | Converte um tipo para um valor booleano, quando possível.|
| ToByte | Converte um tipo em um byte.|
| ToChar | Converte um tipo em um único caractere Unicode, quando possível.|
| ToDateTime | Converte um tipo (tipo inteiro ou string) em estruturas de data e hora.|
| ToDecimal | Converte um ponto flutuante ou tipo inteiro em um tipo decimal.|
| ToDouble | Converte um tipo para um tipo duplo.|
| ToInt16 | Converte um tipo para um inteiro de 16 bits.|
| ToInt32 | Converte um tipo em um inteiro de 32 bits.|
| ToInt64 | Converte um tipo em um inteiro de 64 bits.|
| ToSbyte | Converte um tipo para um tipo de byte assinado.|
| ToSingle | Converte um tipo em um pequeno número de ponto flutuante.|
| ToString | Converte um tipo em uma string.|
| ToType | Converte um tipo para um tipo especificado.|
| ToUInt16 | Converte um tipo para um tipo int não assinado.|
| ToUInt32 | Converte um tipo para um tipo longo não assinado.|
| ToUInt64 | Converte um tipo em um inteiro grande sem sinal.|
|VARIAVEL.parse|Convert internamente com um "try" "catch"|
| as |  Converter um objeto em um tipo específico e retorna NULL se falhar.|
|is| Verifica se um objeto pode ser convertido para um tipo específico retornando true e false|
| StringBuilder | "(Class1)Class2" Tenta converter o objeto e lança uma exceção se falhar.  
---
## **Operadores Aritimeticos**
|Operação	   | Operador|
|---|---|
|adição	       | +|
|subtração	   | -|
|multiplicação	|*|
|divisão	       | /|
|módulo	       | %|
---
## **Operador Relacional**
|Operador| Relacional Descrição|
|---|---|
|== |Igual a|
|!= |Diferente de|
|> |Maior que|
|< |Menor que|
|>= |Maior do que ou igual a|
|<= |Menor do que ou igual a|
---
## **Operador Logico**
|Operador Lógico | Descrição|
|---|---|
|&& | AND = E|
| `||` | OR = Ou|
|!  | NOT = Não|

---
## **Declarações Condicionais**
> Logicas para identificar validações dentro do codigo
* If / Else - Se condição for verdadeira 
    - **If ternario:** _entidade.Id.HasValue ? entidade.Id.Value : (int?)null;_
``` c#
if (Condition1)
{
    // Condition1 is true.
}
else if (Condition2)
{
    // Condition1 is false and Condition2 is true.
}
else if (Condition3)
{
    if (Condition4)
    {
        // Condition1 and Condition2 are false. Condition3 and Condition4 are true.
    }
    else
    {
        // Condition1, Condition2, and Condition4 are false. Condition3 is true.
    }
}
else
{
    // Condition1, Condition2, and Condition3 are false.
}
```
*  **Case**, Switch - Entra em uma condição especifica 
``` c#
int VARIAVEL = 1;
      
      switch (VARIAVEL)
      {
          case 1:
              Console.WriteLine("Case 1");
              break;
          case 2:
              Console.WriteLine("Case 2");
              break;
          default:
              Console.WriteLine("Default case");
              break;
      }
```
---
## **Laços de repetição**
> Sequência finita de ações executáveis que visam obter uma solução para um determinado tipo de problema.


* While - Faca enquanto validando antes de começar
``` c#
while (condição) // condição 
{
    //bloco de código
}
```
* Do While - Igual While mas garante que sera executado pelomenos uma vez
``` c#
do
{
  //bloco de código
} while (condição);
```
* FOR
```c#
for (inicialização; condição; atualização)
{
    // Esse código será executado enquanto a condição for verdadeira
}
```
* Foreach
``` c#
foreach(string NOME in VETOR) //nao precisar ser uma string pode ser ate um Objeto/class
{
    //bloco de código
}
```

* Break / Continue
``` c#
break; // abandona um laço de repetiçao
continue;  // passa para a proxima interacao, normalmente retorna para o inicio do laco de repeticao
```
---
## **Comandos entrada e saida**
``` c#
Console.Write(); // escreve
Console.Write("PALAVRAS {0}, {1}", VARIAVEL0, VARIAVEL1);
Console.Write($"PALAVRAS {VARIAVEL0}, {VARIAVEL1}");
Console.Write(VARIAVEL1);   
Console.Write(new string('-', 50)); // vai repetir 50 vezes o carater '-'
Console.ReadLine(); // espera proximo char ou funcao digitado pelo usuario
Console.ReadKey(); // espera a entrada (ENTER DO TECLADO) de valores 
```
---

## **Identificar cadeia de caracteres**
> Identificando principais métodos da classe String
- **Empty || NULL**
> Valida se valor da string e devolve um bool
``` c#
if (String.IsNullOrEmpty)
{
    // Code
}
```
- **Length**
> Devolve o tamanho da string com inicio no 1
``` c#
int length = stringName.Length;
```
- **Substring**
> Quebra o string para pegar partes menores, primeiro numero e onde inicia ,e se nao adicionar o segundo numero ele pega tudo depois do primeiro,o segundo seria a quantidade de caracters que deve pegar a partir dele
``` c#
string nome = nomeCompleto.Substring(0,9);
```
- **Replace**
> Busca e altera um valor dentro de um String 
``` c#
string nome = stringName.Replace("a", "b");
```
- **Remove**
> Remove uma caracters da string, tem inicio e podemos atribuir um fim ou deixar vazio e pega tudo depois do inicio
``` c#
string nome = stringName.Remove(3);
```
- **Split**
> Divide uma string em um array com base em um caracter de criterio
``` C#
string texto = "text text, 123, são paulo, brasil";
string[] colunas = texto.Split(',');
```
- **IndexOf && LastIndexOf**
> Devolve um int da posicao do campo com base na primeira aparição
``` c#
string texto = "text text, 123, são paulo, brasil";
int indice = texto.IndexOf("text");
```
- **Cointains && StartWith && EndWith**
> Retorna um boll avisando se encontrou, é case sensitive
``` C#
string texto = "text text, 123, são paulo, brasil";
bool existe  = texto.Contains("123");
bool existe  = texto.StartsWith("text");
bool existe  = texto.EndWith("brasil");
```
- **Regex**
>  Uma expressão regular é uma regra que auxilia a recuperar um valor, a entrada dos caracteres que devem ser aceitos ou procurados dentro da expressao segue o padrao da tabela [ASCII](http://www.asciitable.com/).

**IsMath:** Retorna um boll que nos diz se encontrou o valor   
**Math:** Retorna uma expressao se for encontrado a sequencia definida, pode fazer uso de **"QUANTIFICADORES"** que diminuem a repetição e codigo para pegar uma cadeia de caracters
    
``` c#
//Quantificador
string padrao = "[0-9]{4,5}-?[0-9]{4}"; // caracters de 0 ha 9 pela ASCII que se repetem 4 ou 5 vezes sem intervalos e com ou sem o '-' para separar os numeros

//Texto exemplo
string textoDeTeste = "Meu nome é Guilherme, me ligue em 4784-4546";

//IsMath
Console.WriteLine(Regex.IsMatch(textoDeTeste, padrao));

//Math
Match resultado = Regex.Match(textoDeTeste, padrao);
Console.WriteLine(resultado.Value);
```
[Exemplos](https://www.regextester.com/) e testes!  
- [StringBuilder](https://docs.microsoft.com/pt-br/dotnet/standard/base-types/stringbuilder)
- [StringWriter](https://docs.microsoft.com/pt-br/dotnet/api/system.io.stringwriter)
- [StringReader](https://docs.microsoft.com/en-us/dotnet/api/system.io.stringreader)
---

## **List**
> Cria uma lista de referencia a valores que podemos determinar (int, string, var...) ou a objetos (classes, object...);
* **TAMANHO:** A lista não conta a posicao 0 logo se o tamnho fosse 5 poderiamos usar as posições 0,1,2,3 & 4
* **Declarando:** 
    *  List< VARIAVEL > NOME = new List< VARIAVEL >();

* **Atribuindo valor em uma posição:**
    * NOME[POSICAO] = ATRIBUICAO;

* **Chamando:**
    * VARIAVEL NOME1 = NOME[POSICAO];

- **Comandos**
    -  **Add:** Adiciona na proxima posição;
    -  **AddRange:** Adiciona na proxima posição varios elementos;
        - Importante lembrar que adicionamos assim _"addRange(new VARIAVEL[]{iten1, iten2, iten3})"_
    - **Remove:** Remove um item passa o conteudo dele em vez da posição. Por exemplo em uma lista de nomes eu passaria o nome que eu desejo remover o _Remove_ ira encontrar e remover ele da lista.
    - **Length:** Retorna o tamanho da lista
    - **Sort:** Organiza sua lista, se for variaveis ele organiza com com base no padrao (int do maior para menor, string em ordem alfabetica, ...), 
    
- **TAMANHO DE LISTA DINAMICO:** 
    - **Manual:** Podemos validar e criar uma lista nova com o dobro do tamanho da atual e depois salvar a atual dentro da nova. Ou 
    - **Padrao:** List<int> list = new List<int>(); criando assim podemos adicionar, remover, contar... Sem se preocupar com o tamanho. 
---
## **Queue**
> Objetos dentro de um Queue ou Fila saem dela na ordem que entraram. Ou seja o primeiro a entrar e o primeiro a sair

``` C#
// Cria
Queue<string> fila = new Queue<string>();

// Add
fila.Enqueue("Primeiro");
fila.Enqueue("Segundo");

// Remove
fila.Dequeue(); // Remove o "Primeiro"
```
---
## **Stack**
> Objetos que entram no Stack ou Pilha saem na ordem inversa que entram. Ou seja o primeiro a entrar e o ultimo a sair

```c#
// Cria
Stack<string> pilha = new Stack<string>();

// Add
pilha.Push("Primeiro");
pilha.Push("Segundo");

// Remove
pilha.Pop(); // Remove o "Segundo"

```
---
## **LinkedList**
> Lista para adicionarmos a posição que queremos o objeto

```c#
// Cria
LinkedList<string> linklist = new LinkedList<string>();

// Adiciona
var primeiro = dias.AddFirst("Primeiro");
var terceiro = dias.AddAfter(primeiro, "Terceiro");
var segundo = dias.AddBefore(terceiro, "Segundo");
```
---
## **HashSet**
> Cria uma lista sem valores repitidos

``` C#
// Valores para inserir  repitindo 1, 4, 10
var lista1 = new List<int> { 1, 2, 4, 6, 8, 10 };
var lista2 = new List<int> { 1, 3, 4, 7, 10 };

// Cria
ISet<int> hashs = new HashSet<int>();

// Adicionando ao hashs
lista1.ForEach(n => hashs.Add(n));
lista2.ForEach(n => hashs.Add(n));

```
---
## **SortedList**
> Adiciona chave valor, ordem crescente com base na chave e acessivel por chave

``` C#
// Cria
SortedList lista = new SortedList();

// Add
lista.Add("Primeiro", "Luiz G");
```

---
## **Dictionary**
> Cria uma "lista" em que cada elemento possui dois valores, o KEY e o VALUE


- **Key:** Seria o ID do Dictionary, esse valor nao pode se repitir
- **Value:** O valor a ser guardado no Dictionary

- **Criando:**
``` c# 
Dictionary<int, CLASSE> dicionario = new Dictionary<int, CLASSE>
```

- **Adicionando:**
```c#
if (!dicionario.ContainsKey(0))//Verifica se a KEY ja existe
    dicionario.Add(0, new CLASSE {id=0, Nome= LG})
```

- **Pegando Valor:**
```c#
CLASSE retorno = new CLASSE();

dicionario.TryGetValue(0, out retorno);
```
---

## **Programacao Orientada a Objetos**
> Simula no computador objetos como no mundo real, que tem propriedades e comportamentos como no mundo real.

### **Vantagens**
- Dependencia menor entre os modulos de um sistema 
- Combina estrutura e comportamento em um unico objeto
- Compatilha comportamento com outros objetos 
- Reuso aumenta produtividade

### **Desvantagem**
- Usuario se preocupa com funcionalidades 
- Complexidade

### **Principais Metodos**

- **Herança:**
    * Herda codigo de de outra classe ou metodo
``` c#
public class CLASSE1
{
    //codigo
}
        /*----------------------------------------*/
public class CLASSE2 : CLASSE1
{
        //codigo
}
``` 
- **Polimorfismo:**
    * Reescrever um ou mais metodos.
        * **virtual:** permite ser sobreescrito 
        * **override:** define que foi sobreescrito e por padrao e um virtual tambem.
        * **base:** chama tratamento do pai
``` c#
public class CLASSE1
{
    string nome;
    private virtual void Metodo1 (string nome)
    {
        //codigo
    }
}
        /*----------------------------------------*/
public class CLASSE2 : CLASSE1
{
    string nome;
    private override void Metodo1 (string nome)
    {
        base.Metodo1()
        //codigo
    }
}
```
**Construtores:** podemos chamar o construtor da base herdando no metodo do filho
``` c#
 public ConstrutorClass() : base() // o base aqui atribui tudo que e feito no construtor pai
 {
 }
```

- **Encapsulamento:**
    * Proteger um objeto para que nao possa ser reescrito.
``` c#
public class CLASSE
{
    string nome;
    private Metodo (string nome)
    {
        //codigo
    }
}
``` 
- **Abstração:**
    - Uma classe ou metodo que so tem a funcao de ser herdada sendo assim nao pode ser instanciada.
``` c#
public abstract CLASSE
{
    //codigo
}
```
- **Interface:** 
    - Nao podemos atribuir codigos, apenas atribuimos variaveis ou metodos para forcar aqueles que herdarem dela a incluir desta forma. 
    - Muito usada para herdar caracteristicas especificas de uma classe sem herdar e nao o todo.
    - Util para instanciar um Objeto generico

``` c#
// Criando
interface Nome
{
    //metodos, propriedades, indexadores ou eventos 
}

// Usando
IEletrodomestico eletro = new Televisao();

eletro = new Abajur();
```

---

## **Classes** ou Objeto
> A classe seria então o modelo a partir do qual criamos os objetos.

- **base** é usada para acessar membros de classe base de dentro de uma classe derivada.

> UML - [_"Astah"_](https://www.youtube.com/watch?v=PT5jdpfCYHk) usado para criar uma imagem da estrutura da classe
* **Atributos ou Propriedades:**
    * Sao as variaveis criadas dentro da classe.
        - Exemplo: string NOME;

* **Construtor:** Ao instanciar um metodo com o nome da Classe dentro da Classe criamos um construtor que vai ser usado para instanciar essa classe    

   - **Exemplos:**
``` C#
// Criando
public class NomeClass
{
   public string Variavel {get;private set;}
   
   public NomeClass(string variavel)
   {
      Variavel = variavel;
   }
}

// Criando com valor default
// Podemos adicionar um valor default tambem, se no momento de criar essa classe nao for atribuido um valor para a string "var" o compilador atribui oque esta no construtor
public class NomeClass
{
   public string Variavel {get;private set;}
   
   public NomeClass(string variavel = "minha string")
   {
      Variavel = variavel;
   }
}

// Herdando construtor
// Se no futuro essa class for herdada para passar esse construtor usamos 
public class NomeClass2 : NomeClass
{
   public NomeClass2() : base ("caracters")
   {   
   }
}

// Especificando variavel
// Quando o construtor tem mais de um argumento de entrada podemos passar apenas um assim
public class NomeClass
{
   public string Variavel {get;private set;}
   public int Var1 {get; set;}
   
   public NomeClass(string variavel = "minha string", int var1 = 5)
   {
      Variavel = variavel;
      Variavel1 = variavel1
   }
}

NomeClass nomeClass = new NomeClass(var1: 10); // assim passamos o var1 = 10 e o var fica como "minha string"
```
* **Instanciando a classe:**

``` c#
CLASSE NOME; // cria objeto 
NOME = new CLASSE(); // instancia
```
* **Sobrecarga:**
    * Podemos atribuir comportamentos especificos para a mesma classe dependendo das variaveis que ela recebe
    * ***This***: trata se de uma palavra reservada onde atribuimos que o valor da variavel e a criada dentro da classe.

    * **Getter e Setter**: Trata se de de palavras reservadas usadas na construcao da classe para atribuir e consultar o valor de variaveis, a forma de construcao e simples criamos uma chamada com o nome da variavel que vamos trabalhar com a primeira letra MAIUSCULA.
        * **get:** devolve o valor com um return.
        * **set:** atribui o valor com o value.
``` c#
public class CLASSE
{
    string nome; // esse e o NOME referenciado com o this.
    //SOBRECARGA
    public CLASSE (string nome)
    {
        //THIS
        this.nome = nome; // aqui dizemos que o NOME criado na classe recebe o NOME da entrada.
    }
    //GETTER & SETTER
    public string Nome 
    {
        get {return nome;} // retorna o valor
        set {nome = value;} // atribui o valor
    }
}
```
* **Static:** 
> Nao pode ser instanciada _(ou seja so pode ser chamada uma vez)_, por padrao e privado, pode ser publica ou parametrizada.

* **Equals**
> Compara o local na memoria do objeto e retorna true/false, ou seja se duas classes estiverem apontando para o mesmo objeto na memoria o Equals retorna true
``` C#
Class1 clas = new Class1();
Class1 clas1 = new Class1();

if (clas.Equals(clas1)) //RETORNA FALSE
{}

if (clas.Equals(clas)) //RETORNA TRUE
{}
```
- **Partial**
> Modificador de classe para quando dividimos uma classe em duas mas o compilador deve entender as duas sendo a mesma classe e nao dois objetos diferentes com o mesmo nome, assim compartilhando os metodos.
```C#
partial class CLASSE
{
}

//-------------------------------------

partial class CLASSE
{
}
```
- **ExpandoObject**
> Criacao de objetos dynamic, o problema de usar isso é que precisamos conhecer e escrever corretamente o nome das variaveis na hora de usar e se tentar chamar uma variavel que nao existe gera uma execcao
---
## **Structs**
> O C# struct é uma alternativa leve para uma classe. Ele pode fazer quase o mesmo que uma classe, mas é menos "caro" usar uma struct do que uma classe contudo nao possui heranca.

``` c#
class Program
{
    static void Main(string[] args)
    {
        Car car;

        car = new Car("Blue");
        Console.WriteLine(car.Describe());

        car = new Car("Red");
        Console.WriteLine(car.Describe());

        Console.ReadKey();
    }
}

struct Car
{
    private string color;

    public Car(string color)
    {
        this.color = color;
    }

    public string Describe()
    {
        return "This car is " + Color;
    }

    public string Color
    {
        get { return color; }
        set { color = value; }
    }
}
```
---
## **Boxing & Unboxing**
- Boxing: O ato de converter um tipo de valor em um tipo de referência:
``` c#
int x = 9; 
object o = x; 
```
- Unboxing: E o ato de fazer a operacao inversa
``` c#
object o = 9; 
int x = (int)o; 
```

---
## **Metodos**
|Tipo |Definicao| 
|---|---|
|Void | nao retorna nada|
|Variaveis | retorna valor da variavel descrita|
|Objetos| retorna valor do Objeto descrita|
|Async| Faz requisicoes de forma assincrona|

* **ref:**   
> Faz referencia de outra variavel e que seja inicializada e tenha valor antes de ser passada.
``` c#
public void Metodo(ref int variavel){} // cria metodo
int variavelRef = 6; // cria variavel e precisa ter um valor default
Metodo(ref variavelRef); // chama metodo
```
* **out:**   
> Faz referencia de outra variavel e que seja inicializada antes de ser passada, MAS obrigatoriamente tem que atribuir avalor a variavel.
```c#
 public int Metodo (out int variavel )
{
    return variavel = 6; // obrigatorio ter valor atribuido
}
int variavelOut; 
Metodo(out variavelOut);
```

* **valor default:**
> Podemos atribuir um valor na chamada do metodo para default, sendo assim se nao passarmos um valor para essa variavel dentro do metodo.
``` c#
public void Metodo(int nome=0){}
```
* **Atribuindo variavel na chamada:**
> Podemos atribuir a cada qual variavel o valor se refere na chamada do metodo.
``` c#
public void Metodo(int nome1 = 0, int nome2 = 1){}// criando
Metodo(nome2: 3 )// chamando
```
* **Sobrecarga:**
> Adiciona um metodo com mesmo nome mas outras variaveis de entrada para aceitar varios formatos na hora de chamar.
``` c#
public void Metodo(int nome){}
public void Metodo(string nome){}
```

- **as**
> Tenta a converção de tipos genericos para objetos ou variaveis especificas, não devolve erro se der errado apenas null
```c#
public void Metodo (object obj)
{
    Class1 minhaClass1 = obj as Class1;
    if (minhaClass1 != null)
        Console.Write('veio um Class1')
    else
        Console.Write('não veio um Class1')
}
```

- **params**
> Modificador que permite que o Metodo receba diversos parametros daquele tipo dessa forma não precisamos criar diversas sobrecargas.
``` c#
public void Metodo(params CLASSE variavel) //assim chamamos o metodo e passamos quantos objetos do tipo CLASSE quisermos
{
    //Codigo
} 
```

- **Obsolete** para nao alterar o funcionamento de um metodo podemos atribuir alerta para quer os desenvolvedores saibam que aquele metodo esta obsoleto
```  c#
public static void Main(string[] args)
{
    Console.WriteLine("Hello World!");
    Metodo1();

    Console.ReadKey();
}

[Obsolete("Esse metodo esta obsoleto, por favor troque pelo 'Metodo2' !")]
public static void Metodo1()
{
    Console.WriteLine("Feito em 2000");            
}
```
---
## **Delegates**
- **Delegates**
> Delegates podem ser armazenados como variáveis de referência, que representam e apontam para um determinado método que tem o mesmo tipo de retorno, e são muito usados em combinação com eventos.

``` c#
class Program
{
    delegate int Operacao(int a, int b);

    static void Main(string[] args)
    {
        int a = 3;
        int b = 2;

        Operacao operacao = Somar;

        Console.WriteLine(operacao(a, b));

        operacao = Subtrair;

        Console.WriteLine(operacao(a, b));

        Console.ReadKey();
    }

    static int Somar(int a, int b)
    {
        Console.WriteLine($"A operação Somar foi chamada com a = {a} e b = {b}");
        return a + b;
    }

    static int Subtrair(int a, int b)
    {
        Console.WriteLine($"A operação Subtrair foi chamada com a = {a} e b = {b}");
        return a - b;
    }
}
```
- **Metodos Anonimos**
> Basicamente e a forma de juntar o Lambda com o delegates para criar o codigo direto no delegates
``` c#

class Program
{
    delegate int Operacao(int a, int b);

    static void Main(string[] args)
    {
        Operacao operacao = (x, y) => x + y; //expressão lambda
        Console.WriteLine(operacao(3, 2));
    }
}


```

- **Func** Emcapsula um metodo e tem que retornar algo
```c#
class Program
{
    static void Main(string[] args)
    {
        Func<int, int, int> somar = (x, y) => x + y; // Func<entrada 1, entrada 2, entrada n, retorno>
        Console.WriteLine(somar(3, 2));
    }
}

```

- **Predicate** Emcapsula um metodo e nao tem que retornar algo
```c#
class Program
{
    static void Main(string[] args)
    {
        var numeros = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        Console.WriteLine("Números divisíveis por 3:");
        Predicate<int> divisivelPor3 = (numero) => numero % 3 == 0;
        var divisiveis = Array.FindAll(numeros, divisivelPor3);

        foreach (var numero in divisiveis)
        {
            Console.WriteLine(numero);
        }
    }
}

```

- **Action** Variavel que recebe metodos void, podemos atribuir mais de um metodo a essa variavel e todos serao executados
``` c#
class Program
{
    static void Main(string[] args)
    {
        Campainha campainha = new Campainha();
        campainha.OnCampainhaTocou += CampainhaTocou1;
        campainha.OnCampainhaTocou += CampainhaTocou2;
        Console.WriteLine("A campainha será tocada.");
        campainha.Tocar();

        campainha.OnCampainhaTocou -= CampainhaTocou1;
        Console.WriteLine("A campainha será tocada.");
        campainha.Tocar();

        Console.ReadKey();

    }

    static void CampainhaTocou1()
    {
        Console.WriteLine("A campainha tocou.(1)");
    }
    static void CampainhaTocou2()
    {
        Console.WriteLine("A campainha tocou.(2)");
    }
}

class Campainha
{
    public Action OnCampainhaTocou { get; set; }

    public void Tocar()
    {
        if (OnCampainhaTocou != null)
        {
            OnCampainhaTocou();
        }
        
    }
}

/// OU COM LAMBDA
class Program
{
    static void Main(string[] args)
    {
        Action<string> imprimirMensagem 
                = (mensagem) => 
                {
                    Console.WriteLine(mensagem);
                };

        imprimirMensagem("Olá, Alura!");
    }
}
```

- **Event:**  Ele por padrao não leva informações sobre o evento
    - **Sender** Seria quele que chamou o evento e um EventArgs. 
    - **EventArgs** Aqui passamos os argumentos do evento, para criar essa propriedade devemos criar uma classe que herde do EventArgs e nela atribuimos as variaveis de argumento
```c#
class Campainha
{
    /// <summary>
    /// Criando
    /// </summary>
    public event EventHandler<CampainhaEventArgs> OnCampainhaTocou;

    public void Tocar(string apartamento)
    {
        /// Salva todos os que forem acionados durante a execucao do foreach
        List<Exception> erros = new List<Exception>();

        /// Executando todos os metodos dentro do Evento
        foreach (var manipulador in OnCampainhaTocou.GetInvocationList())// GetInvocationList: Chama os metodos como uma lista
        {
            try
            {
                manipulador.DynamicInvoke(this, new CampainhaEventArgs(apartamento)); // Chama de forma Dinamica
            }
            catch (Exception e)
            {
                erros.Add(e.InnerException);
            }
        }

        /// Ou para chamar e parar a execucao se houver um erro 
        // if (OnCampainhaTocou != null)
        // {
        //     OnCampainhaTocou();
        // }
    }
}

/// <summary>
/// Criando uma classe para ser usada no EventArgs com os argumentos do evento
/// </summary>
class CampainhaEventArgs : EventArgs
{
    public CampainhaEventArgs(string apartamento)
    {
        Apartamento = apartamento;
    }

    public string Apartamento { get; }
}

```
---
## **Atributos** 
> Define informacoes sobre um metodo/objeto

- Corpo de um atributo
``` c#
[TIPO DE ATRIBUTO]
class CLASSE
{
    // codigo
}

[TIPO DE ATRIBUTO]
public void main()
{
    // codigo
}
```

- Verificando se o atributo foi definido no objeto:
``` c#
Attribute.IsDefined(typeof(CLASSE), typeof(SerializableAttribute))
``` 

- Criar Atributo
    - **AttributeTargets** tipos que poder usar esse atributo
    - **AllowMultiple** se pode ser aplicado mais de uma vez no mesmo elemento
```c#
// Criando
[AttributeUsage(AttributeTargets.Class, AllowMultiple = false)]
class FormatoDetalhadoAttribute : Attribute
{
    public string Formato { get; }

    public FormatoDetalhadoAttribute(string formato)
    {
        this.Formato = formato;
    }
}

// Usando
 [FormatoDetalhado("Meu Formato")]
public class CLASSE
{
    public string Nome;
}

// Pegando valor da variavel dentro do atributo que criamos
Attribute a = Attribute.GetCustomAttribute(typeof(CLASSE), typeof(FormatoDetalhadoAttribute));
FormatoDetalhadoAttribute formatoDetalhado = (FormatoDetalhadoAttribute)a;
Console.WriteLine(formatoDetalhado.Formato);
```
---
### **Reflection**
> Forma de obter dentro do codigo informacoes sobre o codigo
- **Tipo** tras o namespace e o nome do objeto
```c#
Type tipo = relatorio.GetType();
Console.WriteLine(tipo);
```

- **Membros** tras variaveis, metodos e construtor
```c#
MemberInfo[] membros = tipo.GetMembers();
foreach (var membro in membros)
    Console.WriteLine(membro.ToString());
```

- **Assembly** pega as interface e herancas do objeto
```c#
Assembly esteAssembly = Assembly.GetExecutingAssembly();
var tipos = esteAssembly.GetTypes();
foreach (var tipoAssembly in tipos)
    if (typeof(IRelatorio).IsAssignableFrom(tipoAssembly))
        Console.WriteLine(tipoAssembly);
```

- Pegando informacoes sobre um projeto:
``` c#
static void Main(string[] args)
{
    //Tarefa 1: obter o nome completo do assembly atual
    Assembly assembly = Assembly.GetExecutingAssembly();
    Console.WriteLine("Nome do assembly: {0}", assembly.FullName);

    //Tarefa 2: obter a versão do assembly atual
    //Obter a identidade do assembly primeiro!

    var identidadeAssembly = assembly.GetName();
    Console.WriteLine("Versão: {0}", identidadeAssembly.Version);
    Console.WriteLine("Versão Major: {0}", identidadeAssembly.Version.Major);
    Console.WriteLine("Versão Minor: {0}", identidadeAssembly.Version.Minor);

    //Tarefa 3: descobrir se o assembly atual 
    //          está no Global Assembly Cache

    Console.WriteLine("Está no Global Assembly Cache? {0}",
        assembly.GlobalAssemblyCache);

    //Tarefa 4: descobrir todos os módulos, 
    //          tipos e membros do assembly

    foreach (var modulo in assembly.GetModules())
    {
        Console.WriteLine("Módulo: {0}", modulo);

        foreach (var tipo in modulo.GetTypes())
        {
            Console.WriteLine("\tTipo: {0}", tipo);

            foreach (var membro in tipo.GetMembers())
            {
                Console.WriteLine("\t\tMembro: {0} ({1})", membro, membro.MemberType);
            }
        }
    }

    Console.ReadLine();
}
```
- Peganco informacoes dos elementos de um objeto
```c#
static void Main(string[] args)
{
    //TAREFA 1: obter as propriedades de CarrinhoCliente
    //TAREFA 2: descobrir se podem ler ou escrever
    //TAREFA 3: descobrir seus acessadores getters e setters

    var tipo = typeof(CarrinhoCliente);
    var propriedades = tipo.GetProperties();

    foreach (var propriedade in propriedades)
    {
        Console.WriteLine("Propriedade: {0}", propriedade.Name);

        if (propriedade.CanRead)
        {
            Console.WriteLine("\tPode ler");
            Console.WriteLine("\t\tMétodo get: {0}", propriedade.GetMethod);
        }

        if (propriedade.CanWrite)
        {
            Console.WriteLine("\tPode escrever");
            Console.WriteLine("\t\tMétodo set: {0}", propriedade.SetMethod);
        }
    }

    Console.ReadLine();
}
```
---

## **Gerenciando memoria**
> Durante a depuracao podemos analisar o consulmo de memoria da aplicacao
- **Coletor de lixo (Garbage Colector):** remove da memoria tudo que nao esta em uso liberando memoria
- **Pilha (Stack):** Mostra a order de chamadas da aplicacao, para abrir a janela de pilha basta apertar
    - CTRL + D , C
- **Monte (Heap):** Amontoado de objetos que estao sendo usados pelo programa, qual quer coisa fora do monte e descartado
- **Objeto Finalizado:** Podemos adicionar um metodo ao objeto para ser executado quando ele for apagado pelo Coletor de lixo.
```c#
~NOME()
{
    Console.Write("Objeto Finalizado pelo Coletor de Lixo");
}
```
- **Diagnostico:** Podemos verificar em tempo real o uso de CPU e RAM, para abrir a janela de ferramentas de diagnostico aperte:
    - CTRL + ALT + F2
- **Dispose:** Remove um objeto apos o uso mas temos que garantir que ele sera executado
- **Finally:** Garante o codigo sera realizado ao final do bloco try-catch
- **Using:** Mantem o objeto em uso dentro das chaves
``` c#
using (RecursoDoSistema recurso = new RecursoDoSistema()) 
{
    //Codigo
}
```
---
## **Serializers**
- [**XML&&Json**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/Serializers.md)
---
### **Extensão**
> Podemo adicionar para uma classe ou variavel e são Metodos estáticos onde o primeiro parâmetro usa a palavra reservada this


``` c#
//COM VARIAVEIS
static public class CLASSE
{
    public static int Metodo_Mutiplicacao(this int variavel1, int variavel2)
    {
        return variavel1 * variavel2;
    }
}

int resultado = 5.Metodo_Mutiplicacao(6); //resposta e 30

// COM METODOS
public class CLASSE1
{
}
public static class CLASSE2
{
    public static int Soma(this CLASSE1 obj, int numero1, int numero2)
    {
        return numero1 + numero2;
    }
}
int resultado = new CLASSE1().Soma(5, 5);
Console.WriteLine(resultado);
```
---

### **T**, Soluções Genericas
> Solução generica para reutilizar tratativas passando o tipo na chamada.
```c#
// Criando metodo
// "this List<T>" usando Extensão eu adiciono ao tipo List o metodo "Metodo_MostraAntesDeADD" e so passamos o tipo na hora de chamar este metodo
// "params T[]" recebe um numero indeterminado de parametros que deve ser definido na chamada do metodo "Metodo_MostraAntesDeADD"
public static void Metodo_MostraAntesDeADD<T>(this List<T> list, params T[] itens)
{           
    foreach (T item in itens)
    {
        Console.WriteLine(item);
        list.Add(item);
    }
}

// Usando
List<int> listInt = new List<int>();
listInt.Metodo_MostraAntesDeADD(4, 5, 6, 7, 8, 9);

List<string> listString = new List<string>();
listString.MostraAntesDeADD("a", "b", "c", "d", "e", "f");
```
   - **where T : 'PARAMETRO'** Para usarmos uma solução generica com ferramentas especificas precisamos dar certeza para o Metodo que ele vai recer o parametro esperado, então.  Isso restringe o parâmetro genérico!   
        - **where T : class** Vai ser uma classe
        - **where T : struct** Vai ser uma struct
        - **where T : new()** Vai ser um Construtor 
        - **where T : IComparable**  Vai ser um IComparable interface
        - ...

``` c# 
// Exemplo abaixo insere uma entidade que fizer parte do banco indicado dentro de "ConeccaoDataContext" a partir do LinqSQL, e para dar certo temos que garantir que o parametro generico 'T' vira como Class!
public static void Insert<T>(T entidade) where T : class
{
    using (ConeccaoDataContext dc = new ConeccaoDataContext())
    {
        var table = dc.GetTable<T>();
        table.InsertOnSubmit(entidade);
        dc.SubmitChanges();
    }   
}
``` 
---
## **Trabalhando uma lista de Objetos**

- **Comparable:** Funciona como uma extensão da classe e podemos usar o sorte direto no nosso objeto (ou lista de objetos).
    - Herdamos o **_IComparable_** na nossa classe e criamos um metodo **_CompareTo_** (implementado pela interface),  para poder informar como o **Sort** deve ordenar.    
        - Se for vir depois retorna -1;
        - Se for equivalente retorna 0;
        - Se for vir antes retorna 1;
``` C#
// Criando
public static class CLASSE : IComparable
{
    public int Numero { get; set; }
    public int CompareTo(object obj)
        {
            var classe = obj as CLASSE;

            if(classe == null)
                return -1;
            
            if(Numero < classe.Numero) // Ordena crescente se inverter o sinal fica decrescente
                return -1;
            
            if (Numero == classe.Numero)
                return 0;

            return 1;
        }
}

// Chamando 
List<CLASSE> lista = new List<CLASSE>();
lista.Sort();
```

- **Comparer:** Temos que instanciar uma nova classe e passar para ela os dois Objetos que queremos comparar.
    - Criamos uma nova classe e nela herdamos o  **_IComparer< CLASSE >_** e nessa classe criamos um metodo **Compare** que recebe duas CLASSEs para comparar com base no valor que escolhermos e poder informar como o **Sort** deve ordenar.
        - Se for vir antes retorna -1;
        - Se for equivalente retorna 0;
        - Se for vir depois retorna 1;
``` C#
// Criando
public class MeuComparer : IComparer<CLASSE>
{
    public int Compare(CLASSE x, CLASSE y)
    {
        if (x == y)            
            return 0;            

        if (x == null)            
            return 1;
        

        if (y == null)            
            return -1;
        
        return x.Numero.CompareTo(y.Numero);
        
        // Abaixo segue oque o return acima faz mas feito manualmente

        if (x.Agencia < y.Agencia)
                return -1;

        if (x.Agencia == y.Agencia)
                return 0;

        return 1;
    }
}

// Usando
List<CLASSE> lista = new List<CLASSE>();
lista.Sort(new MeuComparer());
```
---
## **Lambda com Linq**
- Forma **PRIMITIVA** sem o Lambda, apenas para conhecimento
```c#
// Comeca pelo from
IEnumerable<CLASSE> consulta =
    from x in LISTA1
    join y in LISTA2
        on x.Id equals y.Id
    group x by y
        into retorno
    select new //OBJETO ANÔNIMO
    {
        Nome = retorno.Key,
        Quantidade = retorno.Count(),
        Total = retorno.Sum(f => f.Minutos),
        Min = retorno.Min(f => f.Minutos),
        Max = retorno.Max(f => f.Minutos),
        Media = (int)retorno.Average(f => f.Minutos)
    };
```

- Biblioteca de ferramenta complexas , que trabalha com "Expressões Lambda" para usar suas ferramentas o exemplo:   
``` c#
MeuObjeto.LinqMetodo.(Referencia => Referencia.Variavel);
```
- **Select:** Podemos filtrar uma lista para trazer somente um dado
```c#
IList<int> listaInt = Lista.Select(x => x.Numero);
```
- **Where:** Faz uma busca em uma lista com uma condição
``` c#
Lista.Where(x => x != null);
```
- **OrderBy:** Ordena com base no parametro passado e retorna o resultado, e ele não trata os NULL por isso 
``` c#
// Casos comuns
IOrderedEnumerable<CLASSE> = Lista.OrderBy(x => x.Numero); //Ordena crescente
Lista.OrderByDescending(x => x.Numero); //Ordena decrescente

//Validações
Lista.OrderBy(x => {
    if (x == null)
        return int.MaxValue; //Ou MinValue
    return conta.Numero;
});
```
- **FirtOrDefault:** A instrução lambda não tem como saber quantos elementos uma pesquisa retorna por maior que seja a logica de **WHERE** que tivermos, nem por mais certeza que tenhamos que ira retornar apenas um item... Entao usando está propriedade para garantir que a consulta ira devolver apenas um Objeto apenas o primeiro. Assim não precisamos estanciar uma lista de Objetos mas sim apenas um Objeto
```c#
CLASSE classe = Lista.FirstOrDefault(x => x.Numero == 5);
```
- **Take:** Extrai os primeiros 'n' elementos do início da sequência de destino e retorna uma nova sequência contendo apenas os elementos obtidos.
``` c#
List<bool> bools = new List<bool> { true, false, true, true, false };
// Will contain { true, false, true }
IEnumerable<bool> result = bools.Take(3);
```
- **Skip:** "pula" os primeiros nelementos da sequência e retorna uma nova sequência contendo os elementos restantes após os primeiros 'n' elementos.
``` c#
List<bool> bools = new List<bool> { true, false, true, true, false };
// Will contain { true, true, false }
IEnumerable<bool> result = bools.Skip(2);
```

- **Include:** Especificar os dados relacionados
    - **ThenInclude** Relações para incluir vários níveis de dados relacionados

``` c#
var Obj = contexto
                .TABELA
                .Include(x => p.TABELA2)
                .ThenInclude(y => y.ItemTABELA2)
                .FirstOrDefault();
```

---
## **Indexadores:**
> É uma ferramenta muito versatil para acessar seu objeto como uma matriz. Pode ser usada para variaveis tambem.
``` c#
public class CLASSE
    {
        private int[] array = new int[5];
        public CLASSE this[int index]   // Criando Indexador
        {
            get
            {
                return array[index];
            }
            set
            {
                array[index] = value;
            }
        }  

        public int Length
        {
            get { return array.Length; }
        }
    }
```
---
## **COMPILAÇÃO CONDICIONAL**
> Existem diretivas para o codigo identificar quando estamos compilando e quando estamos em ambiente de produção. Ou seja esse codigo só existem em ambiente de producao ou seja na DLL

- [Documentacao](https://docs.microsoft.com/pt-br/dotnet/fsharp/language-reference/compiler-directives)

- **CONSTANTES DE COMPILAÇÃO CUSTOMIZADAS** nas propriedades do projeto podemos atribuir a versao que estamos trabalhando para criar diretivas personalizadas.
    - Adicionar chave nos "Simbolos de compilacao condicional:NETCOREAPP2_0;CHAVE;NETCOREAPP2_0" 
    - Usando essa chave no codigo, somente se a CHAVE estiver como mostrado acima ele vai compilar essa condicao if 
``` C#
#if CHAVE
    //Codigo
#endif

```
- **Define** Adiciona uma CHAVE (diretiva) dentro do codigo e deve ser definido no comeco do codigo
``` c#
#define !DEGUB

using ...
using ...
```

- **Condicionando um Metodo** podemos atribuir uma chamada de metodo e no metodo adicionar a acondicao. Logo aquele metodo so e executado se existir a CHAVE nas propriedades, assim a chamada do metodo nao tem que ser alterada

```c#
 static void Main(string[] args)
{
    string palava = "Hello word";

    MetodoCondicional();

    Console.WriteLine(palava);
    Console.ReadKey();
}

[Conditional("DEBUG")]
public void MetodoCondicional()
{
    Console.WriteLine("ESTOU NO MODO DEBUG");
}
```
- **Warning** podemos atribuir um alerta no modo de compilacao
``` c#
static void Main(string[] args)
{
    #if DEBUG
    #warning  Cuidado voce esta usando o modo debug
    #endif
    Console.ReadKey();
}
```

- **Warning** podemos atribuir um erro no modo de compilacao
``` c#
static void Main(string[] args)
{
    #if DEBUG
    #error Nao e permitido usar compilacao condicional
    #endif
    Console.ReadKey();
}
```

- **Pragma** diretiva usada para suprimir alertas
    - **Usando** Error List> click com direito  no alerta > Supress > In source > Apply
``` c#
// o Metodo1 esta obsoleto entao ele gera um warning
static void Main(string[] args)
{
    #pragma warning disable ALGUM NUMERO
    Metodo1();
    #pragma warning restore ALGUM NUMERO
    Console.ReadKey();
}
```

- **Line Hidden** Faz com que parte do codigo nao seja executado no debugger, isso nao quer dizer que nao sera executado, apenas que o debugger mode vai ignorar aquele trexo
    - **DebuggerStepTrough** Esta e uma condicao que faz o mesmo do Line Hidden mas se aplica direto em um metodo
``` c#
static void Main(string[] args)
{
    #line hidden
    Metodo1(); // esse metodo foi executado mais se eu estiver depurando ele pula esse trexo 
    #line default
    Console.ReadKey();
}

// agora com DebuggerStepTrough
[DebuggerStepTrough]
static void Metodo1()
{
    Console.Write("Hello World");
}
```

---
## **Exception**
> A classe Exeption e a pai de todos as execoes dentro do .Net e todas as execoes sao lancadas desempilhando todas as chamadas do programa ate ser tratada ou devolvida como Erro critico que para a execucao do codigo
- **Message**
> Metodo do exeption que devolve a execcao ocorrida, so pode ser definida direto pelo seu construtor no momento que criamos ou capturamos a execcao.

- **StackTrace**
> o C# preenche automaticamente o caminho que levou a essa execao e salva na propriedade do StackTrace

- **Try / Catch / finally / using**  
    - **Try:** dentro dele adicionamos o codigo que queremos rodar  
    - **Catch:** dentro dele adicionamos o tratamento das execoes   
        - **Ordem:** a ordem das chamas do Catch e de cima para baixo, sendo tratada pelo primeira execcao que o erro se encaixar. Lembrando q o **Exeption** é o pai dessa classe e se ele vier por cima de outros tratamentos esses nunca serao usados.
     - **finally:** Parametro para executar algo independente de _"erros"_ dentro do programa, um bom uso para ele e atribuir o fechamento de conexoes   

    - **using:** Tratativa que visa liberar recursos, muito comum para abrir conexao com Banco de dados por exemplo.  
         - **Dispose:** Para criar uma class ou _"Objeto"_ que tem como funcao se conectar a uma ferramenta precisamos herdar o IDisposeble e definir o fechamento dessa Conexao no metodo Void Dispose 

> Sao parametros da linguagem para tratar execoes quando o programa ja esta em execucao
``` C#
try
{
    //CODIGO PARA TENTAR RODAR
}
catch (Exception)
{
    //Tratando Excecao
}
finally 
{
    //Codigo que tem q ser executado se der erro ou se nao der erro
}
--------------------------------------------------------------------

using (Conexao) //Se algo der errado na conexao ele gera a execao e preserva a ferramenta
{
    //Codigo
}
```

- **Throw**
> Retorna uma execao, podemos usar do Throw para _instanciar_ uma execao especifica ou retornar um metodo com uma execcao na camada de tratamento "**Catch**"
```c#
throw new Exception("Mensagem.");
```

- **ArgumentExeption**
    - **Message:** atribuimos uma mensagem personalizada quando instanciamos o metodo atraves do seu construtor para ser passada para o Usuario/Desenvolvedor dentro do Catch
    - **nameof:** Propriedade que usamos para passa junto do  **ArgumentExeption** a variavel que gerol esse erro ou outra caracteristica que o diferencia dos demais para poder tratar varios  **ArgumentExeption** de forma diferente no Catch ou apenas para melhorar a mensagem de erro que passamos para o usuario atrubuindo campos expecificos  
> Podemos lancar um erro quando algo esta fora da regra do negocio, pensando que isso e um erro mas nao gera uma execcao, nesses casos instanciamos um objeto do tipo **ArgumentExeption**.
``` C#
//Como atribuimos mensagem e usamos nameof
int agencia
throw new ArgumentException("Mensagem.", nameof(agencia));
// Tratando no Catch
catch (ArgumentException ex)
{
    if(ex.ParamName == "agencia")
    {
        //CODIGO
        Console.WriteLine("Argumento com problema: " + ex.ParamName);
    }
}
```
- **Criando Tratamento de Execcoes**
> Para problemas expecificos da nossa aplicacao, a nomenclatura deve ser seguida como **NomeException**, onde criamos a classe e Herdamos do Exception para criar
``` C#
public class SaldoInsuficienteException : Exception
{
    //Construtor sem mensagem
     public SaldoInsuficienteException()
    {
    }
    //Construtor com mensagem
    public SaldoInsuficienteException(string mensagem)
        : base(mensagem)
    {
    }
}
```
---
## **Multithreading**
> Capacidade do C# de realizar tarefaz assincronas 

- ### **Async** Executa Metodos de forma paralela ao codigo, ou seja não precisamos esperar o fim da sua execucao para executar o restante do codigo
    - **async** Assinatura de metodos assincronos, por padrao se um metodo foi assinado como "async Task" e porque ele tem a diretiva await dentro
        - **Task** Por padrao todo metodo async deve retornar uma Task, COM EXECAO DE EVENTOS (como click de botoes em Windows Forms)
        - **await** aguarda o fim da execucao daquele trexo de codigo

``` c#
async Task VisualizaRelogio()
{
    while (true)
    {
        await Task.Delay(100); //Com isso vamos aguardar tempo de Delay terminar mesmo se tratando de uma Task que tem o comportamento assincrono
        TimeSpan tempo = relogio.Elapsed;
        int minutos = tempo.Minutes;
        int segundos = tempo.Seconds;
        int milissegundos = tempo.Milliseconds;
        txtRelogio.Text = $"{minutos:00}:{segundos:00}:{milissegundos:000}";
    }
}
```

- ### **Task**  Tarefa que recebe como padrao uma action/metodo e trabalha de forma assincrona, trabalha com o TreadPoll (ou seja e gerenciada por ele)
    - **Oque e** Representa uma unidade de trabalho que deverá ser realizada de forma assincrona

    - **Criar** Criamos como um objeto e passamos o metodo como parametro
    - **Start** Da inicio ao Metodo referenciado
    - **Wait** Forca todo o programa a aguardar o termino daquela task antes de continuar
    - **Result** Usando uma solucao generica e possivel definir o retorno
    - **WaitAll** Aguarda a chamada de todos os metodos dentro de uma lista de tasks, com isso definimos que a partir daquele ponto vamos esperar o retorno das Tasks
    - **ContinueWith** Faz a chamada de outro metodo apos o termino do primeiro
        - **TaskContinuationOptions** Aplica condicoes para chamar o proximo metodo
            - **NotOnFaulted** Nao executa se tiver ocorrido um erro
            - **OnlyOnFaulted**
            - **Outros** Nao estao todos listados aqui
    - **Exception** Por padrao as Tasks nao geram erros mas armazenam na task oque ocorreu
        - **InnerExceptions** retorna uma lista com os erros 
    - **Factory** Ferramenta de Tasks para definir uma ordem/hierarquia para a chamada das tasks
        - **StartNew** Inicia a task
            - **TaskCreationOptions** Define o comportamento da tarefa
    - **CancellationTokenSource** Ferramenta que atribui uma flag para denifinir a parada de uma task
``` c#

// Cria tarefa
Task tarefa1 = new Task(() => ExecutaTrabalho(1));

// Criar metodo que retorna Tarefa
async Task<String> MeuMetodo ()
{
    return "Pocoyo";
}

// Inicia
tarefa1.Start();
tarefa1.Wait();

// Inicia a tarefa direto na chamada
Task tarefa2 = Task.Run(() => ExecutaTrabalho(2));

// Inicia a tarefa na chamada e define um retorno
Task<int> tarefa3 = Task.Run(() =>
{
    return CalcularResultado(2, 3);
});

// Pegando o retorno
Console.WriteLine("O resultado é: {0}", tarefa3.Result);

// WaitAll
Task[] tarefas = new Task[10];
for (int i = 0; i < 10; i++){    
    int numeroCorredor = i; //guardar o valor de i numa variável local para nao perder a referencia
    Task tarefa = Task.Run(() => Correr(numeroCorredor));
    tarefas[i] = tarefa;
}
Task.WaitAll(tarefas);

// ContinueWith
Task tarefa = Task.Run(() => Ola());
tarefa.ContinueWith((tarefaAnterior) => Mundo(), // o "tarefaAnterior" apenas encapsula a task anterior para ter a referencia de quando ela ira acabar
    TaskContinuationOptions.NotOnFaulted);
tarefa.ContinueWith((tarefaAnterior) => Erro(tarefaAnterior),
    TaskContinuationOptions.OnlyOnFaulted);

// Exception
private static void Erro(Task tarefaAnterior)
{
    var excecoes = tarefaAnterior.Exception.InnerExceptions;
    foreach (var excecao in excecoes)
        Console.WriteLine(excecao);
}

// Factory
Task tarefaMae =
    Task.Factory.StartNew(() => { // inicia a tarefa mae
        Console.WriteLine("Tarefa-mãe iniciou.");
        for (int i = 0; i < 10; i++)
        {
            int tarefaId = i; // Salva o valor em uma variavel local para nao perdera referencia
            Task tarefaFilha =
            Task.Factory.StartNew((id) => 
                Metodo1(id), // o ID aqui define a relacao de dependencia com a tarefaMae onde encapsula a tarefa
                tarefaId, // passa o valor de entrada 
                TaskCreationOptions.AttachedToParent); // define o comportamento
        }
    });
// CancellationTokenSource
static CancellationTokenSource cancellationTokenSource
            = new CancellationTokenSource(); // Cria a chave para cancelamento
cancellationTokenSource.Cancel(); // Atribui o valor que ira cancelar a tarefa
while (!cancellationTokenSource.IsCancellationRequested) // verifica se foi cancelado
{
    Console.WriteLine("Tic");
    Thread.Sleep(500);
    Console.WriteLine("Tac");
    Thread.Sleep(500);
}

```

- ### **Task Parallel** Biblioteca para fazer chamadas paralelas, ou seja nao precisa precisar uma interacao para iniciar a proxima
    - **Parallel** Objeto que ira realizar as chamadas
        - **Invoke** Chamada de metodo`s
        - **For** Laco de repeticao onde colocamos inicio e fim, depois podemos usar lambda para chamar o metodo
        - **Foreach** Passagem por todos os elementos de uma lista
        - **IsCompleted** Retorna se todas as interacoes foram chamadas
        - **LowestBreakIteration** Conta quantidade de interacoes
``` c#
// Invoke
Parallel.Invoke(() => Metodo1(),
                () => Metodo2());

// For
Parallel.For(0, 100, (i) => Metodo1(i));
// Abrindo o For
Parallel.For(0, 99, (int i, ParallelLoopState state) => 
{
    if (i == 75)
    {
        state.Break();
    }

    Metodo(i);
}
);

// Foreach
var itens = Enumerable.Range(0, 100);
Parallel.ForEach(itens, (item) => Metodo1(item));

// IsCompleted
var resultadoLoop = Parallel.For(0, 100, (i) => Metodo1(i));
Console.WriteLine("Completou sem interrupção? {0}", resultadoLoop.IsCompleted);

// LowestBreakIteration
var resultadoLoop = Parallel.For(0, 100, (i) => Metodo1(i));
Console.WriteLine("Quantos itens foram processados (parcialmente)? {0}", resultadoLoop.LowestBreakIteration);
``` 


- **Threads & TreadPoll**
    - **Threads** Trecho de código que é executado em paralelo a seu código, sendo que podem existir diversas threads executando em um dado momento.
    - **TreadPoll** Ele administra quais Threads irão executar em paralelo (normalmente esse número reflete a quantidade de núcleos do processador sabendo que cada nucleo suporta uma Threads) e também faz um reaproveitamento delas pois quando uma tarefa conclui ele não elimina a thread, apenas marca ela como “livre e pronta para ser utilizada novamente”.



- ### **Thread** Inicia uma linha de execução assincrona que trabalha mais próxima ao sistema operacional. A grande diferenca entre ela e o Async é que ela podemos acessar enquanto esta rodando pois se trata de um programa a barte.
    - **Informacoes** A Thread tem informacoes pessoais que definem ela
        - **Name** Nome da Thread
        - **CurrentCulture** Linguagem
        - **Priority** Prioridade para ser rodada
        - **ExecutionContext** Local, costuma ser o system
        - **IsBackground**
        - **IsThreadPoolThread**
    - **Criar** Muito proximo da Task, utiliza as expressoes lambda
    - **ParameterizedThreadStart** Permite a passagem de valores na chamada da execucao
    - **Parar uma Thread** O codigo abaixo nao conta com uma ferramenta como os outros mais sim com uma logica
    - **Join** Bloqueia o incio de outras Treads aguardando o final dessa assim temos um sincronismo
    - **ThreadPool** Cria uma fila de Treads para serem executadas, todas serao iniciadas antes de comecar a finalizar
    -  **Bloqueio** Defie que o codigo sera acessado somente por 1 thread por vez, isso e util quando temos muitos metodos acessado a mesma lista
        - **Lock** Bloqueia a entrada de outra Thread a uma liha de codigo simutaeamente 
        - **Monitor** Define entrada e saida do trecho de codigo, mas devemos garantir a saida do Monitor
``` c#
// Informacoes
Thread thread = new Thread(() => Metodo1());
thread.Name = "Jorginho";

// Criar
Thread thread = new Thread(() => Metodo1());
thread.Start();

// ParameterizedThreadStart
ParameterizedThreadStart ps = new ParameterizedThreadStart((p) => Metodo2(p));
Thread thread = new Thread(ps);
thread.Start(123); // Aqui podemos passar o valor, mas lembrando que na definicao do "Metodo2" a entrada e um objeto

// Parar uma Thread
bool relogioFuncionando = true;
Thread thread = new Thread(() => 
{
    ExibirThread(Thread.CurrentThread);
    while (relogioFuncionando)
    {
        Console.WriteLine("tic");
        Thread.Sleep(1000);
        Console.WriteLine("tac");
        Thread.Sleep(1000);
    }
});
thread.Start();
Console.WriteLine("Tecle algo para interromper.");
Console.ReadKey();
relogioFuncionando = false;

// Join
Thread thread = new Thread(() => Metodo1());
thread.Start();
thread.Join();

// ThreadPool, exemplo apenas chamando um metodo 50 vezes
for (int i = 0; i < 50; i++)
{
    int j = i;
    ThreadPool.QueueUserWorkItem((x) 
        => Metodo1(j));
}

// Lock
static object somaGeralObject = new object();
lock (somaGeralObject)
{
    somaGeral = somaGeral + subtotal;
}

// Monitor
static object somaGeralObject = new object();
Monitor.Enter(somaGeralObject);
try
{
    somaGeral = somaGeral + subtotal;
}
finally
{
    Monitor.Exit(somaGeralObject);
}

```
- ### **ConcurrentDictionary**, este tipo de dictionary e proprio para trabalhar com Threads, dessa forma podemos acessar a lista do dicionario de forma assincrona
    - **Criar** Formato padrao do dicionario so muda a chamada do objeto
    - **TryUpdate** Usado para alterar o valor naquela posica e retorna um bool
``` c#
Thread thread = new Thread(() =>
{
    for (int i = 0; i < NUMERO_ITENS; i++)
    {
        int valor;
        do
        {
            valor = dicionario[i];
        } while (!dicionario.TryUpdate(i, valor + 1, valor)); // +1 para cada posicao do dicionario
        Thread.Sleep(i);
    }
});
``` 

- ### **PLinq**  Forma de usar as chamadas assincronas (paralelas) junto da biblioteca do Linq
    - **AsParallel** Define o paralelismo na consulta, diferente do modelo padram do linq que comecamos com o "Select()" 
        - **WithExecutionMode** Adiciona o modo de execucao, isso define como ou se o Paralelismo ira funcionar. A decisao e com base na complexidade do codigo
            - **Default** A biblioteca do Linq decide se ira ser mais rapido a consulta paralela ou nao
            - **ForceParallelism** Ignora as recomendacoes do Linq e roda de forma paralela
        - **WithDegreeOfParallelism** Determina o numero de execucoes simultaneas que pode ter
        - **AsOrdered** Ordena a lista alfabeticamente 
        - **ForAll** Laco de repeticao onde podemos atribuir uma acao dentro dele

``` c#
//AsParallel
var consulta = LISTA.AsParallel()
                    .Select(x => x).Where(y => y.NOME == "Jorginho");

// WithExecutionMode
var consulta = LISTA.AsParallel()
                    .WithExecutionMode(ParallelExecutionMode.Default)
                    .Select(x => x).Where(y => y.NOME == "Jorginho");
var consulta = LISTA.AsParallel()
                    .WithExecutionMode(ParallelExecutionMode.ForceParallelism)
                    .Select(x => x).Where(y => y.NOME == "Jorginho");

// WithDegreeOfParallelism
var consulta = LISTA.AsParallel()
                    .WithExecutionMode(ParallelExecutionMode.ForceParallelism)
                    .WithDegreeOfParallelism(4)
                    .Select(x => x).Where(y => y.NOME == "Jorginho");

// ForAll
var consulta = LISTA.AsParallel()
                    .Select(x => x).Where(y => y.NOME == "Jorginho");
consulta.ForAll(x =>
{
    Console.WriteLine(x.NOME);
});

``` 

---
## **Descrição de arquivos, disco e diretorios**	
- [**FileInfo**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/FileInfo.md)
---
## **References**
 - **Mesmo projeto**
 > Se formos fazer referencia a um projeto / objeto dentro so mesmo projeto pasta referenciar ele clicando com o direito do mouse em "References"

 - **Projeto externo**
 > Nao faz sentido copiar um projeto inteiro para podermos utilizar no .Net entao a solucao para referenciar um projeto externo e utiliar o DLL que fica disponivel no "Bin" do projeto em questao, mas referenciar direto desse repositorio pode gerar uma serie de erros sabendo que o DLL vai ser atualizado sempre que executarmos o projeto, para solucionar isso basta criar uma copia da versao do projeto (ha DLL no momento), para uma pasta onde salvamos ele como uma biblioteca.

- **NuGet:** Instalador de dependencias do Visual Studio, por padrão quando instalamos um framework com dependencias ele ja instala as dependencias.
   - **Console:** Ferramentas > Gerenciador de pacotes do NuGet > Console do Gerenciador de Pacotes      
        - **install-package:** O Console do Gerenciador de pacotes do NuGet que utiliza **PowerShell**
            - **Projeto Padrao:** Referencia o projeto que vai receber a dependencia
        - **Comandos**
            - **Encontrar:** Find-Package NOME
            - **Instalar:** Install-Package NOME
            - **Desinstala:** Uninstall-Package NOME
            - **Atualizar:**
                - **Todos:** Get-Package -updates
                - **UM:** Update-Package NOME
            - **Help** Get-Help NOME
---
## **Stream**, Flush de Dados ou IO (Input and Output)
> Trabalhando com dados em diversos momentos não temos a opção de carregar o Arquivo inteiro para depois trabalhar essa informação. Temos que fazer tudo de forma dinamica para não oculpar toda a memoria RAM.

### **Arquivo CSV** TXT separando informações por ',' (virgula)

### **FileStream:** Para leitura de arquivos texto
- **Caminho:** Por padrão se não passar todo o caminho ele vai buscar no **bin/debug** da sua aplicação
``` c#
string Endereço = "nome.txt";
var FluxoArquivo = FileSteam(Endereço, FileMode.Open);
 ```
 - **Lendo:** Lendo arquivo parte a parte seguindo o padrão que definimos, um exemplo é que podemos ler por tamanho em **byte** ou linha
     - **UTF** - Trata-se de um padrão de conversão de bynarios  
``` c#
byte[] ArrayBytes = new byte[1024]; //1kilo byte
var bytesLidos = -1;
while(bytesLidos != 0)
{
    bytesLidos = fluxoDoArquivo.Read(ArrayBytes, 0, 1024);;// ArrayBytes - recebe a saida, 0 - deslocamento de bytes, 1024 - max de caracters , numeroDeBytesLidos - retorna 0 quando acabar os bytes
var utf8 = new UTF8Encoding(); // Encoding.Default; no lugar do UTF8Encoding(); tras o padrao do sistema operacional
var texto = utf8.GetString(ArrayBytes, 0, bytesLidos); // Recebe o array de bytes e o inicio e fim da leitura para nao repetir dados
Console.Write(texto);// Aqui o testo ja esta legivel 
}
``` 
- **Escrevendo** para salvar devemos transformar o string em um UTF, no texto abaixo foi seguido o padão UTF-8 para salvar.
``` c#
var Caminho = "NOME.csv";

using (var fluxoDeArquivo = new FileStream(Caminho, FileMode.Create))
{
    string entidade = "456,7895,4785.40,Gustavo Freitas";// valores separados por virgula
    var encoding = Encoding.UTF8; // conversor para UTF
    var bytes = encoding.GetBytes(entidade); // convertendo a string
    fluxoDeArquivo.Write(bytes, 0, bytes.Lenght); // escrevendo
}
```
- **Fechando:** Preficamos informar o codigo que ja usamos o arquivo e fechar a coneccao
``` c#
FluxoArquivo.Close();
// ou
using(var fluxoDoArquivo = new FileStream(Endereço, FileMode.Open))
{
    // Lendo arquivo
}
```
### **StreamReader:** Para leitura de arquivos texto
- **Read()** le a quantidade de linhas
- **ReadLine()** le uma linha 
- **ReadToEnd()** le tudo ate o fim, MAS usa memoria RAM de mais! Pois salva tudo nela 
- **EndOfStream** identifica o fim do arquivo 
``` c#
//EXEMPLO
var Endereco = "NOME.txt";
using (var fluxoDeArquivo = new FileStream(Endereco, FileMode.Open))
{
    using (var leitor = new StreamReader(fluxoDeArquivo))
    {
        while(!leitor.EndOfStream)
        {
            var linha = leitor.ReadLine()
            Console.WriteLine(linha);
        }
    }
}
```
- **Write** escreve arquivos
    - **Create** se existir ele apaga o conteudo e escreve
    - **CreateNew** se existir lanca uma execcao pois so trabalha com arquivos novos
    - **AppendText** adiciona conteudo sem apagar o existente no arquivo 
``` c#
var Caminho = "Nome.csv"
using (var fluxoDeArquivo = new FileStream(Caminho, FileMode.CreateNew)) //Aqui podemos alterar o metodo "CreateNew" para um dos exemplos acima
{
    using (var escritor = new StreamWriter(fluxoDeArquivo))
    {
        escritor.Write("456,65465,456.0,Pedro"); // Conteudo para o arquivo
    }
}
```
- **Copy**
``` c#
File.Copy("Arquivo.txt", "CopiaArquivo.txt", overwrite: true);
```
### **BUFFER** O sistema so vai escrever algo em arquivos ao final da execução, para despejar o BUFFER devemos usar o Flush. Com isso economizamos memoria RAM tb

- **GZipStream** trabalhando com arquivos zipados

```c#
/// Compactando
using (FileStream fluxoArquivo = new FileStream("Texto.zip", FileMode.OpenOrCreate, FileAccess.Write))
{
    using (GZipStream compactador = new GZipStream(fluxoArquivo, CompressionMode.Compress))
    {
        using (StreamWriter gravadorFluxo = new StreamWriter(compactador))
        {
            gravadorFluxo.Write("Olá, Alura! (gravado com StreamWriter)");
        }
    }
}

/// Descompactando
using (FileStream fluxoArquivo = new FileStream("Texto.zip", FileMode.Open, FileAccess.Read))
{
    using (GZipStream descompactador = new GZipStream(fluxoArquivo, CompressionMode.Decompress))
    {
        using (StreamReader leitorFluxo = new StreamReader(descompactador))
        {
            string textoLido = leitorFluxo.ReadToEnd();
            Console.WriteLine("Texto lido: {0}", textoLido);
            Console.ReadKey();
        }
    }
}
```
---

## **Banco de Dados**
- **[BD](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/BD.md)**

---
 ## **Web**
 - **[.Net Core](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/.NetCore.md)**
- [**Ajax&&WebForms**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/Ajax%26%26WebForms.md)

---
## **Criptografia C# AES com MD5**

- [**Documentação**](https://docs.microsoft.com/pt-br/dotnet/api/system.security.cryptography.aes?view=netcore-3.1)
- **Chaves**
    - **Publica** Faz a criptografia de algo
    - **Privada** Faz a descriptografia de algo
- **Certificado** Valida a chave publica

```c#
static void Main( string mensagemOriginal)
{
    string mensagemDecodificada = "";
    byte[] bytesCodificados = null;

    Cript partida = new Cript();
    Cript chegada = new Cript();

    string chavePublicaDaChegada = chegada.ChavePublica;
    bytesCodificados = partida.CodificarMensagem(mensagemOriginal, chavePublicaDaChegada);
    mensagemDecodificada = chegada.DecodificarMensagem(bytesCodificados);

    Console.WriteLine("string decifrada: {0}", mensagemDecodificada);
    Console.ReadLine();
}

public class Cript
{
    private readonly string chavePrivada;

    public string ChavePublica { get; }

    public Cript()
    {
        RSACryptoServiceProvider encriptadorRSA = new RSACryptoServiceProvider();
        ChavePublica = encriptadorRSA.ToXmlString(includePrivateParameters: false);
        chavePrivada = encriptadorRSA.ToXmlString(includePrivateParameters: true);
    }


    public byte[] CodificarMensagem(string mensagemOriginal, string chavePublicaDestinatario)
    {
        byte[] bytesCifrados;
        ASCIIEncoding conversor = new ASCIIEncoding();
        byte[] mensagemBytes = conversor.GetBytes(mensagemOriginal);
        RSACryptoServiceProvider encriptadorRSA = new RSACryptoServiceProvider();
        encriptadorRSA.FromXmlString(chavePublicaDestinatario);
        bytesCifrados = encriptadorRSA.Encrypt(mensagemBytes, fOAEP: false);
        return bytesCifrados;
    }

    public string DecodificarMensagem(byte[] bytesCifrados)
    {
        byte[] bytesDecifrados;
        RSACryptoServiceProvider decifradorRSA = new RSACryptoServiceProvider();
        decifradorRSA.FromXmlString(chavePrivada);
        bytesDecifrados = decifradorRSA.Decrypt(bytesCifrados, fOAEP: false);
        ASCIIEncoding conversor = new ASCIIEncoding();
        return conversor.GetString(bytesDecifrados);
    }
}
```
---
## **Assembly Version**
> Definimos verçoes de Dll para evitar o 'Inferno das Dll' (DLL HELL)

- **Assembly Version** Para cada projeto podemos em propriedades definir a verçao do assembly. São 4 campos com as descricoes abaixo.

    **1.** Major, novas versoes ou mudancas bruscas que quebram a compatibilidade de versoes anteriores

    **2.** Minor, colocando funcionalidades nao tao impactantes

    **3.** Build, identifica o tipo de publicacao em servidores

    **4.** Revision, qual e exatamente o codigo fonte ou versao de codigo fonte


- **Assinatura** Podemos adicionar uma assinatura com senha nos assemblys (adiciona um arquivo com a extencao 'pfx' tambem chamado **StrongName**) e o programa recebe um **PublicToken** essa chave e usada como referencia quando referenciamos esse projeto em outro projeto (com isso podemos garantir a seguranca de qual Dll nosso projeto ira receber, assim por mais que adicionem Dll com o mesmo nome o programa nao ira executar). Quanto e adicionado todos os outro projetos associados devem possuir o arquivo de assinatura tambem 'pfx'.
    - **PFX** Personal Information Exchange, ou seja, intercâmbio de informações pessoais. Serve para identificar o desenvolvedor/empresa.  
        - **PublicToken** Identifica um certificado de assinatura
        - **PrivateToken**
    - **Chave temporaria** para desenvolvimento. 
        - **Gerar** no **Developer Command Prompt** va ate o local do projeto e digite 'sn -p NOME.pfx NOMEChaveTemporaria.snk', ele deve pedir a senha e depois gerar o arquivo
        - **Desabilitar chave privada** no **Developer Command Prompt** como admin va ate o local do PROJETO/bin/debug/ e digite 'sn - Vr NOMEPROJETO.exe' isso significa verification removal, ou remoção da verificação.
        - **Usar** Em assinaturas clique na chave atual (deve ser a pfx) e procure o NOME.snk, depois marque a opcao **"Somente Assinatura Atrasada"**
- **ILDASM** 
    - **Oque e?** Código de linguagem intermediária
    - **Abrir:** **Developer Command Prompt** digitar 'ildasm', depois procurar o NOME.exe do programa que queremos observar
    - **Para que serve?** Podemos identificar o PublicToken no **MANIFEST**

- Verificando PublicToken (se programa esta assinado dentro do codigo)
``` c#
Assembly assembly = Assembly.GetExecutingAssembly();
Console.WriteLine("Nome do assembly: {0}", assembly.FullName);
```
---
### **CodeDOM**
> Gerador de codigo com codigo
- [**Documentacao**](https://docs.microsoft.com/pt-br/dotnet/framework/reflection-and-codedom/using-the-codedom)
```c#
static void Main(string[] args)
{
    //TAREFA: Utilizar código C# para gerar código C#,
    //          produzindo a classe Funcionario:
    /*
    namespace RecursosHumanos
    {
        using system;
        public class Funcionario
        {
            public string nome;
            public decimal salario;
            public Funcionario(string nome, decimal salario)
            {
            }
        }
    }
    */

    //Tarefa 1: criar uma unidade de compilação
    CodeCompileUnit unit = new CodeCompileUnit();

    //Tarefa 2: criar o namespace RecursosHumanos
    CodeNamespace codeNamespace = new CodeNamespace("RecursosHumanos");

    //Tarefa 2.1: importar o namespace System
    CodeNamespaceImport import = new CodeNamespaceImport("System");
    codeNamespace.Imports.Add(import);

    //Tarefa 2.2: criar a classe Funcionario
    CodeTypeDeclaration funcionario = new CodeTypeDeclaration("Funcionario");

    //Tarefa 2.3: criar o campo nome
    CodeMemberField nome = new CodeMemberField(typeof(string), "nome");
    nome.Attributes = MemberAttributes.Public;
    funcionario.Members.Add(nome);

    //Tarefa 2.4: criar o campo salário
    CodeMemberField salario = new CodeMemberField(typeof(decimal), "salario");
    salario.Attributes = MemberAttributes.Public;
    funcionario.Members.Add(salario);


    //Tarefa 2.5: criar o construtor da classe
    CodeConstructor construtor = new CodeConstructor();
    construtor.Attributes = MemberAttributes.Public;

    CodeParameterDeclarationExpression paramNome =
        new CodeParameterDeclarationExpression(typeof(string), "nome");
    construtor.Parameters.Add(paramNome);

    CodeParameterDeclarationExpression paramSalario =
        new CodeParameterDeclarationExpression(typeof(decimal), "salario");
    construtor.Parameters.Add(paramSalario);

    funcionario.Members.Add(construtor);

    //Tarefa 2.6 adicionar o objeto a unidade de compilacao
    codeNamespace.Types.Add(funcionario);
    unit.Namespaces.Add(codeNamespace);

    //Tarefa 3: cria o provedor de modelo de código
    CodeDomProvider provider = CodeDomProvider.CreateProvider("CSharp");

    //Tarefa 4: gerar código e salva o arquivo
    using (var streamWriter = new StreamWriter("Funcionario.cs"))
    {
        provider.GenerateCodeFromCompileUnit(unit, streamWriter,
            new CodeGeneratorOptions());
    }

}
```

---

### **Resources File**
- [**ResourcesFile**](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/ResourcesFile.md)

---

# **GUID**, globally unique identifier
> É um identificador unico composto por 32 caracters
### **Versão**
> Cada versão possibilita uma forma de gerar esse codigo, a mais atual que é a "Versão 5" que possibilita a passagem de um parametro 

- **Versão na cadeia de caracters**
    - xxxxxxxx-xxxx-Yxxx-xxxx-xxxxxxxxxxxx, o 'Y' na cadeia informa a versão

- **Exemplo**

``` c#
// Criar
Guid g = Guid.NewGuid();
Console.WriteLine(g);

// Mostrando
Console.WriteLine(Guid.NewGuid());
```
