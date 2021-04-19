# **Info Disk, Arquivos e Diretorios**

- **Informaçoes do disco**
``` c#
//Nome do drive
//Verificar se o drive está pronto
//Tipo do drive
//Formato do drive
//Espaço livre, em bytes, KB, MB, GB e TB

var drives = DriveInfo.GetDrives();

foreach (var drive in drives)
{
    Console.WriteLine("Nome: {0}", drive.Name);
    if (!drive.IsReady)
    {
        Console.WriteLine("O drive não está pronto.");
        continue;
    }
    Console.WriteLine("Tipo: {0}", drive.DriveType);
    Console.WriteLine("Formato: {0}", drive.DriveFormat);

    Console.WriteLine("Espaço livre:");

    long bytes = drive.TotalFreeSpace;
    Console.WriteLine("{0} bytes", bytes);

    double kb = bytes / KILOBYTE;
    Console.WriteLine("{0:N2} KB", kb);

    double mb = kb / KILOBYTE;
    Console.WriteLine("{0:N2} MB", mb);

    double gb = mb / KILOBYTE;
    Console.WriteLine("{0:N2} GB", gb);

    double tb = gb / KILOBYTE;
    Console.WriteLine("{0:N2} TB", tb);

    Console.WriteLine();
}
``` 
- **Informacoes de arquivos**
``` c#
//      Nome
//      Caminho completo (diretório + nome do arquivo)
//      Data e hora do último acesso
//      Tamanho do arquivo (bytes)
//      Atributos do arquivo
//      Adicionar atributo somente-leitura
//      Verificar os atributos novamente
//      Remover atributo somente-leitura
//      Verificar os atributos novamente

File.WriteAllText(caminho, "Texto inicial do arquivo");
FileInfo info = new FileInfo(caminho);
Console.WriteLine("Nome {0}", info.Name);
Console.WriteLine("Caminho completo: {0}", info.FullName);
Console.WriteLine("Último acesso: {0}", info.LastAccessTime);
Console.WriteLine("Tamanho: {0} bytes", info.Length);
Console.WriteLine("Atributos: {0}", info.Attributes);
info.Attributes = info.Attributes | FileAttributes.ReadOnly;
Console.WriteLine("Atributos: {0}", info.Attributes);
info.Attributes = info.Attributes & ~FileAttributes.ReadOnly;
Console.WriteLine("Atributos: {0}", info.Attributes);
```

- **Diretorios**
``` c#
//Criar um novo diretório
//Verificar se ele foi criado
//Apagar o diretório que foi criado
Directory.CreateDirectory(NomeDiretorio);
if (Directory.Exists(NomeDiretorio))
{
    Console.WriteLine("O diretório foi criado com sucesso");
}
Console.WriteLine("Atributos: {0}", localDir.Attributes);
Console.WriteLine("Último acesso: {0}", localDir.LastAccessTime);
Directory.Delete(NomeDiretorio);
Console.WriteLine("O diretório foi removido com sucesso");

//Descobrir o caminho da pasta "Meus Documentos"
//Combinar caminho da pasta "Meus Documentos" com arquivo "alura.txt"
//Obter somente o nome do diretório do arquivo
//Obter somente o nome do arquivo
//Obter a extensão do arquivo
//Modificar a extensão do arquivo
var meusDocumentos = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
Console.WriteLine("Meus Documentos: {0}", meusDocumentos);
var caminhoCompleto = Path.Combine(meusDocumentos, "alura.txt");
Console.WriteLine("Caminho Completo: {0}", caminhoCompleto);
var somenteNomeDiretorio = Path.GetDirectoryName(caminhoCompleto);
Console.WriteLine("Somente Nome do Diretório: {0}", somenteNomeDiretorio);
var somenteNomeArquivo = Path.GetFileName(caminhoCompleto);
Console.WriteLine("Somente Nome do Arquivo: {0}", somenteNomeArquivo);
var extensaoArquivo = Path.GetExtension(caminhoCompleto);
Console.WriteLine("Extensão do Arquivo: {0}", extensaoArquivo);
caminhoCompleto = Path.ChangeExtension(caminhoCompleto, "xyz");
Console.WriteLine("Nova extensão do arquivo: {0}", caminhoCompleto);
```

- **Listar formato de arquivos em diretorios**
``` c#
//Obter o diretório de início do projeto
//Listar todos os diretórios do projeto
//Listar todos os arquivos csharp (.cs) do projeto

DirectoryInfo diretorioInicial = new DirectoryInfo(@"..\..\..");
ListarDiretorios(diretorioInicial);

private static void ListarDiretorios(DirectoryInfo diretorioInicial)
{
    foreach (var diretorio in diretorioInicial.GetDirectories())
    {
        Console.WriteLine(diretorio.FullName);

        foreach (var arquivo in diretorio.GetFiles("*.cs"))
        {
            Console.WriteLine(arquivo.FullName);
        }   

        ListarDiretorios(diretorio);
    }
}
```
