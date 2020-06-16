# **Prompt**
- **echo**  PALAVRA - escreve no terminal
- **dir** - lista arquivos na pasta
- **cd** PASTA - troca de pasta
- **mkdir** NOME - cria pasta
- **move** nome.txt PASTA - move aldo para pasta
- **type** NOME.txt - Mostra conteudo do arquivo no terminal
- **echo** TEXTO TEXTO > NOME.txt - Grava o conteudo no arquivo
- **cd** .. - volta uma pasta na hierarquia
- **rename** NOME1.png  NOME2.png - Renomear o nome 
- **copy** NOME1.png NOME2.png - Copiar arquivos
- **del** NOME.png - apaga arquivo
- **cls** - limpa o terminal

### **CMDER**
> Terminal personalizado do windows para o CMD 

 ### **.bat**
> Script do prompt
- **Criar** NOME.bat
- **Executar** NOME.bat

### **setx**
> Variavel de ambiente permanente

- **Criar** setx NOME "C:\CAMINHO" /M
    - Obs: o CAMINHO so precisa ir ate a pasta onde esta o .bat nao precisa adicionar ele no CAMINHO

### Processador
- **Arquitetura do processador**
    - echo %PROCESSOR_ARCHITECTURE%
- **Arquiterua do SO**
    - wmic OS get OSArchitecture

### **Chocolatey**
> Gerenciador de aplicativos
- **Instalar**
    - @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

- **Install progs**
    - choco install -y NOME 
        - **Version opcional** -version 4.2.2
- **Unistall progs**
    - choco uninstall NOME
- **Lista**
    - **Instalados pelo choco** choco list
    - **Todos os progs** choco list -l

### **OneGet** 
> Gerenciador de aplicativos nativo do Win10
