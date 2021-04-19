# Namespace

Por padrão toda biblioteca deve conter um nome padrão em seu namespace. Ex.: MinhaEmpresa.SeuNameSpace  _(padrão PascalCase)_.

# Classes

As classes devem começar com letra maiúscula e para cada palavra, a primeira letra também deve ser maiúscula  _(padrão PascalCase)_.

C#

```csharp
public class Empresa { }
public class HistoricoDeCompra { }
public class ItemDaVenda { }
```

# Interfaces

As interfaces devem começar com a letra ‘I’ maiúscula e para cada palavra, a primeira letra também deve ser maiúscula  _(padrão PascalCase)_.

C#

```csharp
public class IPedidoService { }
public class IHistoricoDaCompra { }
public class IItemDoPedido { }
```

# Campos

Os campos para utilização interna devem começar com letra minúscula, e para cada palavra, a primeira letra deve ser maiúscula. Como geralmente são utilizados no escopo da classe como protected ou private, devemos iniciar seu nome com  _underscore_  “_”, e para cada palavra, a primeira letra deve ser maiúscula _(padrão_ _lowerCamelCase__)_.

C#

```csharp
protected string _nome;

private int _qtdProdutos;
private int _codProduto;

private string _cliente;

private DateTime _dtNascimento;
```

# Propriedades

As propriedades devem começar com letra maiúscula e para cada palavra, a primeira letra também deve ser maiúscula  _(padrão PascalCase)_.

C#

```csharp
public string Nome { get; set; }
public DateTime DataDeNascimento { get; set; }
public int CodigoDoProduto { get; set; }
```

# Métodos

Os métodos devem começar com letra maiúscula e para cada palavra, a primeira letra também deve ser maiúscula  _(padrão PascalCase)_.

C#

```csharp
public string GetNome()
public bool Verificar()
public void Executar()
```

# Parâmetros

Os parâmetros devem começar com letra minúscula e para cada palavra, a primeira letra deve ser maiúscula _(padrão_ _lowerCamelCase__)_.

C#

```csharp
public void SetNome(string nome)
public bool Verificar(int codigoDoCliente)
public void Executar(DateTime dataDaExecucao)
```

# Variáveis

As variáveis devem começar com letra minúscula e para cada palavra, a primeira letra deve ser maiúscula.

C#

```csharp
string nome;
var i = 0;
int quantidadeDeProdutos;
```

Quando a variável estiver no escopo da classe, sendo  _private_  ou  _protected_, ela vira um  _field_  (campo) e deve ser precedida de um "_" (_underscore_,  _padrão_ _lowerCamelCase__)_. Veja no tópico  **Campos**.

> **Nota**: Há uma discussão a respeito do  _underscore_  para campos/variáveis privados(as) no C#, como podemos ver neste link  [http://forums.dotnetfoundation.org/t/underscores-in-private-fields/731](http://forums.dotnetfoundation.org/t/underscores-in-private-fields/731). Realmente não fica claro se os padrões são para UTILIZAR (conforme especificação da equipe de desenvolvimento do .Net Core em  [https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md](https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md)) ou NÃO UTILIZAR (conforme especificado na documentação dos design guidelines do .Net Core em  [https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/general-naming-conventions](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/general-naming-conventions)). O plugin StyleCop condena o uso do  _underscore_  para campos/variáveis privados(as), mas por ser um excelente auxílio visual e por questões de costume, inclusive adotados em outras diversas linguagens de programação, adotamos o estilo de codificação utilizado pela equipe de desenvolvimento do .Net Core.

Quando a variável for uma constante ou somente leitura, o padrão deve ser  _PascalCase_.

C#

```csharp
private const string MensagemTeste = "Mensagem teste aqui";
public static readonly string AvisoErro = "Aviso de erro padrão aqui";
```
# Componentes Windows Forms

```text
Common Controls
 btn Button           chk CheckBox                ckl CheckedListBox 
 cmb ComboBox         dtp DateTimePicker          lbl Label 
 llb LinkLabel        lst ListBox                 lvw ListView 
 mtx MaskedTextBox    cdr MonthCalendar           icn NotifyIcon 
 nud NumeircUpDown    pic PictureBox              prg ProgressBar 
 rdo RadioButton      rtx RichTextBox             txt TextBox 
 tip ToolTip          tvw TreeView                wbs WebBrowser 

Container
 flp FlowLayoutPanel    grp GroupBox               pnl Panel 
 spl SplitContainer     tab TabControl             tlp TableLayoutPanel 


Menus and toolbars
 cms ContextMenuStrip 
 mns MenuStrip 
 ssr StatusStrip 
 tsr ToolStrip 
 tsc ToolStripContainer 


Information Type
 dts DataSet 
 dgv DataGridView 
 bds BindingSource 
 bdn BindingNavigator 
 rpv ReportViewer 

Dialog
 cld ColorDialog 
 fbd FolderBrowserDialog 
 fnd FontDialog 
 ofd OpenFileDialog 
 sfd SaveFileDialog 

Module
 bgw BackgroundWorker 
 dre DirectoryEntry 
 drs DirectorySearcher 
 err ErrorProvider 
 evl EventLog 
 fsw FileSystemWatcher 
 hlp HelpProvider 
 img ImageList 
 msq MessageQueue 
 pfc PerformanceCounter 
 prc Process 
 spt SerialPort 
 scl ServiceController 
 tmr Timer 

Print
 psd PageSetupDialog 
 prd PrintDialog 
 pdc PrintDocument 
 prv PrintPreviewControl 
 ppd PrintPreviewDialog 

Crystal Reports
 crv CrystalReportViewer 
 rpd ReportDocument 
 
Other
 dud DomainUpDown 
 hsc HScrollBar 
 prg PropertyGrid 
 spl Splitter 
 trb TrackBar 
 vsc VScrollBar

==============================================

<!--------------A----------------->
AdRotator                   ar


<!--------------B----------------->
Button                      btn


<!--------------C----------------->
Calender                    cal
CheckBox                    chk
CheckBoxList                chklst
Column (DataGridView的)     col
ColumnHeader (ListView 的)  ch
Combobox                    cbo
CompareValidator            cv
CrystalReportViewer         rptvew


<!--------------D----------------->
DataGrid                    dg
DataGridView                dgv
DataList                    dl
DomainUpDown                dud
DropDownList                ddl


<!--------------F----------------->
FileUpload                  ful
Form                        frm


<!--------------G----------------->
GridView                    gv
GroupBox                    grp


<!--------------H----------------->
HiddenField                 hf


<!--------------I----------------->
Image                       img
ImageButton                 imgbtn
ImageList                   il


<!--------------L----------------->
Label                       lbl
LinkButton                  lnkbtn
ListBox                     lst
ListView                    lv


<!--------------M----------------->
MenuStrip                   ms


<!--------------O----------------->
ObjectDataSource            ods


<!--------------P----------------->
PagedDataSource             pds
Panel                       pnl
PictureBox                  pic


<!--------------R----------------->
RadioButton                 rdo
RadioButtonList             rdolst
RangeValidator              rv
RegularExpressionValidator  rev
Repeater                    rpt
RequiredFieldValidator      rfv


<!--------------S----------------->
StatusLabel                 slbl
StatusStrip                 ss


<!--------------T----------------->
TabControl                  tab
Table                       tbl
TabPage                     tp
TextBox                     txt 
Timer                       tmr
ToolStrip                   ts
ToolStripButton             tsbtn
ToolStripDropDownButton     tsddb
ToolStripLabel              tslbl
ToolStripMenuItem           tsmi
TreeView                    tv/tvw


<!--------------V----------------->
ValidatorSummary            vs


<!--------------W----------------->
WebBrowser                  wbs
```
