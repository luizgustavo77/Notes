# **Banco de Dados**
> BANCO MICROSOFT NAO E CASE SENSITIVE OU SEJA NAO DIFERE MAIUSCULO DE MINUSCULO

- **Versao**
``` sql
use master
select @@version
```

## **Model**
> Toda vez que criamos um banco de dados ele segue o padrao do banco Model, assim se quisermos uma tabela em todos os bancos e so criar ela no model q ela vai ser re criada em todos os novos bancos

## **Estrutura do Banco**
- **Size**
> Tamanho inicial do banco, mesmo sem utilizar ele ja reserva esse espaco para o banco

- **MaxSize**
> Tamanho maximo do banco, se nao for deficnido ele nao tem limite

- **Log**
> Local do arquivo de log, nele sao armazenados informacoes sobre as transacoes 

- **Dono**
> Proprietario do banco, seria quem criou e essa pessoa tem todas permissoes 

---
## **Caracteres**
- **Char(n)** – Trata-se de um datatype que aceita como valor qualquer dígito, sendo que o espaço ocupado no disco é de um dígito por caractere. É possível utilizar até 8 mil dígitos.

- **Varchar(n)** – Também aceita como valor qualquer dígito e o espaço ocupado em disco é de um dígito por caractere. Permite usar também no máximo 8 mil dígitos. A diferença pro Char, é que o Varchar geralmente é usado quando não sei o tamanho fixo de um campo.

- **Text** – Qualquer dígito pode ser usado neste datatype, sendo ocupado 1 byte por caractere, o equivalente a 2.147.483.647 bytes.


- **Bigint** – Aceita valores entre -2^63 e 2^63-1, sendo que esse datatype ocupa 8 bytes.

- **Int** – Os valores aceitos aqui variam entre -2^31 a 2^31-1. Ocupa 4 bytes.

- **Smallint** – Aceita valores entre -32768 até 32767 e ocupa 2 bytes.

- **inyint** – Os valores aceitos aqui variam entre 0 e 255, ocupa apenas 1 byte.

- **Bit** – É um tipo de dado inteiro (conhecido também como booleano), cujo valor pode corresponder a NULL, 0 ou 1. Podemos converter valores de string TRUE e FALSE em valores de bit, sendo que TRUE corresponde a 1 e FALSE a 0.

- **Decimal(P,S)** – Os valores aceitos variam entre -10^38-1 e 10^38-1, sendo que o espaço ocupado varia de acordo com a precisão. Se a precisão for de 1 a 9, o espaço ocupado é de 5 bytes. Se a precisão é de 10 a 19, o espaço ocupado é de 9 bytes, já se a precisão for de 20 a 28, o espaço ocupado é de 13 bytes, e se a precisão for de 29 a 38, o espaço ocupado é de 17 bytes.

- **Numérico(P,S)** – Considerado um sinônimo do datatype decimal, o númerico também permite valores entre -10^38-1 e 10^38-1 e o espaço ocupado é o mesmo do anterior.
 
- **Float[(n)]** – O mesmo que double precision quando o valor de n é 53, este datatype aceita valores entre -1.79E + 308 e 1.79E + 308. O espaço ocupado varia de acordo com o valor de n. Se esse valor estiver entre 1 e 24, a precisão será de 7 dígitos, sendo que o espaço ocupado será de 4 bytes. Se o valor de n estiver entre 25 e 53, sua precisão será de 15 dígitos, assim sendo o espaço ocupado será de 8 bytes.

- **Real** – Este datatype é similar ao float(n) quando o valor de n é 24. Os valores aceitos variam entre -3.40E + 38 e 3.40E + 38. Esse datatype ocupa 4 bytes.
 
- **Money** – Este datatype aceita valores entre -2^63 e 2^63-1, sendo que 8 bytes são ocupados.

- **Smallmoney** – É possível usar valores entre -2^31 e 2^31-1, sendo que 4 bytes são ocupados.
 
- **Datetime** – Permite o uso de valores entre 1/1/1753 e 31/12/9999. Este datatype ocupa 8 bytes e sua precisão atinge 3.33 milisegundos.

- **Smalldatetime** – Aceita o uso de valores entre 1/1/1900 e 06/06/2079, sendo que sua precisão é de 1 minuto e ocupa 4 bytes em disco.

- **Unicode** - Podemos atribuir em alguns campos o 'n' na frente para aceitar mais q o A-Z ja que alguns paises tem mais caracters no alfabeto
---
## **Create Database**
```sql
CREATE DATABASE database_name
```
- **Dump** salva estrutura do banco
---
## **Create Table**
> criando tabelas
``` sql
CREATE TABLE TABELA (
    COLUNA1 int,
    COLUNA2 varchar(255));
```
> criando banco de dados
``` sql
CREATE DATABASE db_NOME;
```

- **CHECK**
> Validacao de campo antes de inserir

``` sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

---
## **Alter Table**
- **ADD**
``` SQL
ALTER TABLE TABELA
ADD COLUNA varchar(255);
```
- **DROP**
``` sql
ALTER TABLE TABELA
DROP COLUMN COLUNA;
```
- **Alter**
```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```
- **Truncate**
``` sql
TRUNCATE TABLE table_name;
```
---
## **PRIMARY KEY // FOREIGN KEY**
> identificador de coluna 

``` sql
create table NOME (
	COLUNA smallint,
 	COLUNA varchar (50),
	COLUNA int not null foreign key
		references TABELA (COLUNA),
	primary key (COLUNA)); 
create table NOME (
	COLUNA smallint primary key,
 	COLUNA varchar (50),
	COLUNA int not null foreign key
		references TABELA (COLUNA)); 
create table processo (
	processo int,
	ano smallint,
	dataAbertura smalldatetime not null,
	descricao varchar(200) default 'AQUI DESCRIPTION',
	primary key(processo, ano) ); -- CRIA COM CHAVE COMPOSTA AS CHAVES PRIMARIAS
``` 
---
## **SELECT**

> seleciona dados


```sql
select * in TABELA
``` 

- Distinct
- from TABELA
- group by 
- having CONDICAO
- orderb by 
- top

**"as" APELIDO**
``` sql
select COLUNA as APELIDO, COLUNA as APELIDO from TABELA -- NO MERCADO NAO USA O "as" pq funciona sem ele
-- Exemplo:
 select a.nome, a.rm from aluno a -- AQUI DEPOIS DO FROM DEMOS O APELIDO PARA ALUNO E USAMOS ATES O a.aluno SENDO A=ALUNO
```

---
## **DATA**

```sql
set dateformat mdy
	EX: smalldate >>> 'mes/dia/ano'
select * from TABELA where year(TABELA.COLUNA) = 1985
select * from TABELA where MONTH(TABELA.COLUNA) = 1985
select day(APELIDO.COLUNA) from TABELA APELIDO -- pegar apenas dia com apelido
```
---

## **OPERADORES**

``` sql
=, >, <.... igual c##
Is null /* e nullo */
Is not null /* nao e nulo */
``` 
---
## **Where**

> onde

```sql
select COLUNA, COLUNA from TABELA where COLUNA= INFORMACAO
select COLUNA, COLUNA from TABELA where COLUNA like 'LETRA%' -- vai pegar tudo depois da letra
```

---
## **INSERT**

> insere registro na tabela

```sql
INSERT into TABELA (COLUNA, COLUNA, COLUNA) values (INFORMACAO, 'INFORMACAO', INFORMACAO)

INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```
---
## **DELETE**

> apaga informacao

```sql
delete from TABELA where COLUNA=1 -- apaga toda coluna
delete from TABELA where COLUNA != 'INFORMACAO' -- apaga toda coluna com informacao diferente
```
---
## **UPDATE**

> atualiza valor

``` sql
update TABELA set COLUNA='INFORMACAO', COLUNA='INFORMACAO' where COLUNA='INFORMACAO'
update TABELA set COLUNA += ' INFORMACAO' where COLUNA='INFORMACAO' -- para nao editar toda a informacao mas somente uma pate
```
---
## **ORDER BY**

- **ASC** ascendente
- **DESC** decrescente 

```sql
select * from TABELA APELIDO where COLUNA>1000 order by NOME -- em vez de coluna no final deixei nome para ser explicativo
select * from TABELA APELIDO where COLUNA>1000 order by NOME desc -- de baixo para cima
select * from TABELA order by NOME, NOME desc -- ORDENA OR 2 PEGANDO PELO 2 PARAMETRO
select top 1 COLUNA from TABELA order by NOME, NOME desc -- ORDENA OR 2 PEGANDO PELO 2 PARAMETRO
```
---
## **INNER JOIN**
> tras informacoes de tabelas diferentes mas so oque existe logo nao tras TUDO

``` sql
select * from TABELA1 APELIDO inner join TABELA2 APELIDO on (APELIDO.COLUNA1 = APELIDO.COLUNA2);
	--OBS: select APELIDO.COLUNA, APELIDO.COLUNA from TABELA1 APELIDO, TABELA2 APELIDO where APELIDO.COLUNA1 = APELIDO.COLUNA2; - join sem o join
select * from TABELA1 APELIDO1 left join TABELA2 APELIDO2 on APELIDO1.COLUNA = APELIDO2.COLUNA where APELIDO.COLUNA is null -- tras campos igual a null OU SEJA TABELA FANTSMA
```

- **LEFT JOIN && RIGHT JOIN:**  left e quem vem depois de from e right e quem vem depois do join
	- **FORMA DE USAR:** 
``` sql 
select * from TABELA1 APELIDO left join TABELA2 APELIDO on APELIDO.COLUNA1 = APELIDO.COLUNA2 -- tras somente TABELA1 oq esta a esquerda
select * from TABELA1 APELIDO right join TABELA2 APELIDO on APELIDO.COLUNA1 = APELIDO.COLUNA2 -- tras todo mundo depois do join "TABELA2"
```

- **Full join**
> Tras tudo do join preenchendo oque ano atende a logica com null

``` sql
select * from TABELA1 APELIDO full join TABELA2 APELIDO on APELIDO.COLUNA1 = APELIDO.COLUNA2 -- tras todo mundo depois do join "TABELA2"
```

- **CONTANDO TODOS OS CAMPOS**
``` sql
select count(TABELA.COLUNA) from TABELA1 APELIDO right join TABELA2 APELIDO on APELIDO.COLUNA1 = APELIDO.COLUNA2 group by -- tras TODOS TODOS
```
---
## **COUNT**

> conta numero de registros

```sql
select count(*) as APELIDO, COLUNA from TABELA
select count(*) as APELIDO, COLUNA from TABELA where COLUNA='%abc%' -- todo mundo
select count(TABELA.COLUNA) as APELIDO from TABELA -- todo mundo onde nao e nulo
select count(distinct COLUNA) as APELIDO from TABELA -- pega quantos valores diferentes tem
OBS: QUANTO PROFESSOR FALAR TODOS USA LEFT, RIGHT OU FULL
```
- **Count com outra tabela**
> usando o "group by" o sql entende que deve contar com base na COLUNA referenciada
``` SQL
-- Aqui estamos contando quantas vezes cada UF aparece na tabela e adicionando uma coluna que diz se o UF e pequeno, medio ou grande com base no numero de vezes que esse UF repete
select cod_uf, count(cod_cliente) qtd,
	case 
		when count(cod_cliente) < 200 then 'pequeno'
		when count(cod_cliente) < 600 then 'medio'
		else 'grande'
	end as tamanho
from tb_clientes
group by cod_uf
```
---
## **MAX**

> maximo
```sql
select max(COLUNA) APELIDO from TABELA
```
---
## **SUM**

```sql
select sum(COLUNA) APELIDO from TABELA where COLUNA=NUMERO -- soma
```
---
## **GROUP BY**
> Agrupa valores, temos que tomar cuidado para garantir que as colunas selecionadas nao se repitam

- Normalmente usamos junto de um calculo como: Sum, Max, Min, AVG & COUNT

```sql
select COLUNA, sum(COLUNA) APELIDO from TABELA group by COLUNA
select count(*) qtd, COLUNA from TABELA group by COLUNA -- tras q quandtidade de coluna informacoes iguas
``` 

- **Having**
> Adiciona filtros no Order By


``` sql
select count(*) qtd, COLUNA from TABELA group by COLUNA having count(*) >= NUMERO -- tras q quandtidade de coluna informacoes iguas e maiores que 6
```

---
## **CALCULOS**

``` sql
select COLUNA * 2 APELIDO from TABELA -- QUANDO FAZ CALCULO OBRIGATORIO TER APELIDO PQ PERDE O NOME
```
---

## **BETWEEN**

``` sql
select COLUNA as APELIDO from TABELA where COLUNA between  and NUMERO/LETRA
```
--- 
## **UNION**
> Faz juncao de consultas, tornando suas tabelas uma, as colunas tem que ser do mesmo tipo. Se houver registros repetidos ele tras apenas um deles


---

## **CAST**

> converte para algo

``` sql
select COLUNA, 'LETRAS' + cast(COLUNA as varchar (20))
from TABELA
```
---
## **CONVERT**

```sql
select COLUNA, 'LETRAS' + convert(varchar, COLUNA)
from TABELA
```
---
## **SUBCONSULTA**

> uma consulta dentro da outra.. perde desempenho e so devolve um campo
``` sql
select COLUNA1
	(select COLUNA2 from TABELA2
	where COLUNA2 = COLUNA3) APELIDO
from TABELA1
```
---

## **Views**
> Objeto do banco para ser lido no formato de uma tabela

- **Execution plan:**
``` txt
- `crtl + L` mostra o custo para executar
    - Nao pode haver um `full scan` pois isso da muita recursividade... Para resolver usamos `indice`
- Inicia com vc_NOME
- Guarda uma consulta (select) dentro dela como se fosse uma tabela
- Atualiza sempre que tem uma alteracao no banco que faz referencia
```

- **Create**  
``` sql
create view vm_NOME as 
select * from TABELA  -- select que ficara guardado na view
where CONDICAO        -- com essa condicao

---

create view vm_NOME as
select T2.COLUNA, T2.COLUNA,COLUNA
from TABELA1 T2
inner join TABELA2 T2
    on T1.COLUNA = T2.COLUNA
```

- **Alter**
> Precisa reescrever tudo ao alterar uma view
``` sql
alter view vm_NOME as
select T2.COLUNA, T2.COLUNA,COLUNA
from TABELA1 T2
inner join TABELA2 T2
    on T1.COLUNA = T2.COLUNA
```

- **Usando**
``` sql
select * from vm_NOME
```

- ***Join entre Views***
``` sql
-- aqui nao podemos deixar um "*" pois a View e salva como uma tabela e nao podemos atribuir o COLUNA1 duas vezes como teriamos se fosse trazida de VM e T1 por isso especificamos
select COLUNA2, COLUNA3, COLUNA4, T1.COLUNA1 
from TABELA T1
inner join vm_NOME VM
    on VM.COLUNA1 = T1.COLUNA1
```
---

## **VARIAVEIS**

> Oberigatorio adicionar o @ e tem um conjunto de variaveis do BANCO que inicia com @@ como mostra a [documentacao](https://docs.microsoft.com/pt-br/sql/t-sql/functions/identity-transact-sql?view=sql-server-2017)

> Ha diversos tipos de variaveis descritas na [documentacao](https://www.promotic.eu/en/pmdoc/Subsystems/Db/MsSQL/DataTypes.htm)
- **DECLARANDO**
``` SQL
declare @NOME in -- tipos validos para campos
```
- **ATRIBUINDO VALOR**
``` SQL
-- Motifica valor
set @NOME = 10
set @NOME += 15
```
- **BUSCANDO VARIAVEL**
``` SQL
-- Exibindo variaveis
print @NOME
select @NOME
```
- **@@IDENTITY**  
> No MySQL e equivalente ao [LAST_INSERT_ID()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_last-insert-id)

Faz com que o SGBD adiciona na variavel o numero do lancamento quando se roda um comando no banco de dados
``` SQL
create table NOME(
    chave int primary key identity (1,1) );
```
- ***Variavel como VIEW***
``` SQL
declare @NOME int
set @NOME = (select count(*) from TABELA)--obrigatorio uso de ()
print 'NOSSA UM TEXTO INCRIVEL ' + cast(@NOME as varchar(255))
```
---
## **BEGIN...END**

> Abre chave fecha chave, indicando um cloco
``` SQL
if @NOME = 15 
begin
    print 'O valor vale 15'
end
else 
begin
    print 'o valor e diferente de 15'
end
```
---
## **IF...ELSE**

``` SQL
if @NOME = 15 
begin
    print 'O valor vale 15'
end
else 
begin
    print 'o valor e diferente de 15'
end
```
---
## **WHILE**

> Unico laco de repeticao
- **USANDO**
``` SQL
declare @NOME int 
set @NOME = 1
while @NOME < 10
begin 
    print 'Contador' + cast(@NOME as varchar(2)) --cast convert de int para varchar
    set @NOME +=1
end
```
---
## **CASE**
> Possue dois modelos para uso como citados abaixo

- **SIMPLE CASE:**
> Adicionamos caso a caso

``` SQL
CASE input_expression
    WHEN when_expression THEN result_expression [ ...n ]
    ELSE else_result_expression
END
```

- **SEARCHED CASE:**
>Usado por exemplo no caso de um range o 'BOOL' poderia ser > 1

``` SQL
CASE
    WHEN BOOL THEN result_expression [ ...n ]
    ELSE else_result_expression
END
```

- **COM SQL**
``` SQL
select COLUNA,
    case COLUNA
        when 'STRING' then NUMERO
        when 'STRING' then NUMERO
    end as APELIDO
    case
        when COLUNA > NUMERO then 'STRING'
        when COLUNA < NUMERO and
            COLUNA = NUMERO then 'STRING'
        else 'STRING'
    end as APELIDO -- nome da coluna que o case gera
from TABELA;
```

**Exemplo EXTRA**

``` SQL
select * 
from TABELA
order by case @NOME
            when 1 then COLUNA
            when 2 then COLUNA
            else cod_uf -- orderna pelo cod_uf
         end
-- os campos do case/order by devem ser do mesmo tipo de dados         
```
---

## **Stored Procedures - SP**

> E uma coleção de comandos em SQL, encapsula tarefas repetitivas, aceita parâmetros de entrada e retorna um valor de status.

> ##MUITO## performatica para executar codigos demorados e tratar dados direto dentro do banco  
> Ex: Calculo de notas dos alunos em uma escola

- **Create:**
``` sql
create procedure sp_NOME as
begin
    -- os comandos vao aqui
    select *
    from tb_clientes order by
        CASE WHEN (select count(*) from tb_clientes where tipo_pessoa = 'M') > (select count(*) from tb_clientes where tipo_pessoa = 'F') THEN tb_clientes.tipo_pessoa 
        else tb_clientes.cod_estado_civil
        END 
end
```

- **Create (Com parametros) && Usando:**
``` SQL
create procedure sp_NOME (@NOME varchar(2)) as -- nao precisa criar a variavel antes
begin
    -- os comandos vao aqui
    select *
    from ... -- codigo
end

--USANDO 

sp_NOME 'AA' -- passa a variavel apos chamar poderia ser int sem as ''
```

- **Usando:**
``` SQL
exec sp_NOME
-- ou
sp_NOME
```

- **Return**
> retorna um valor mais nao e obrigatorio usar mesmo se estiver no codigo
```sql
create procedure sp_NOME as
begin
    --- codigo para executar
	declare @VARIAVEL int = 14
    --- depois de executar ele pode devolver um valor 
	return @VARIAVEL
end
```
- **Alterando:**  
``` sql
alter procedure sp_NOME  as
begin
	-- os comandos vao aqui
end
```
- **Output:**
> solicita que o valor daquela variavel e temos que mencionar na chamada da SP para passar esse valor por parametro
``` sql
create procedure sp_NOME (
			@VARIVAEL1 int,	
			@VARIAVEL2 int OUTPUT) as

set @VARIAVEL2 = (select count(*) 
				from TABELA 
				where @VARIAVEL1 = COLUNA1)

--chamada
declare @VAIRAVEL int
exec sp_NOME 150, @VARIAVEL OUTPUT
print ' INFORMACAO PARA MOSTRAR NA TELA ' + 
	   cast(@VARIAVEL as varchar(3))
```
---
## **Tabelas temporarias**
> criando com um _#_ fica visivel somente na sessao corrente (sessao e cada abertura do banco idependente do usuario) e assim que fechamos ela e apagada, criando com _##_ fica visivel globalmente ate o usuario que criou apagar

> Sao salvas no tempdb.Temporary Tables.dbo.NOME

``` sql
create table #TABELA (
    COLUNA1 int,
    COLUNA2 varchar(255))
```
---
## **Trigger**
> Metodo que e adionado quando um insert, delete ou update e rodado em uma tabela especifica
- **Insert**
``` sql
alter trigger trg_NOME 
		on TABELA for insert as
begin
	
	declare @reg int
	set @reg = (select count(*) from inserted)
	if @reg > 1 begin		
		rollback tran
	end
end

--vai chamar a trigger automaticamente
insert into TABELA 
values (123, 'bla');
```
- **Delete**
```sql
create trigger trg_NOME
	on tb_TABELA delete as
begin
	declare @variavel decimal(10,2)
	--descobre a soma dos rendimentos
	set @variavel = (select sum(coluna)
					 from DELETED)
	if @variavel > 10000 begin
		rollback tran
	end
end 

--vai chamar a trigger automaticamente
delete from TABELA
where COLUNA = ID
```
- Update
```sql
create trigger trg_NOME
	on TABELA for update as
begin
	declare @antigo varchar(40)
	declare @atual varchar(40)

	set @antigo = (select COLUNA
				   from deleted)
	set @atual = (select COLUNA
				   from inserted)

	print 'Valor Antigo: ' + @antigo
	print 'Valor Atual: ' + @atual
end

--vai chamar a trigger automaticamente
update TABELA set COLUNA = 'bla'
where COLUNA = ID

```
---

## **EXCECOES**
> Tratando erros para retornar algo para usuario

``` sql
BEGIN
  BEGIN TRY
    --Codigo SQL
  END TRY
  BEGIN CATCH
      SET @MENSAGEM = 'Houve um erro número: ' + CONVERT(VARCHAR(10), ERROR_NUMBER()) + ' - '
	  SET @MENSAGEM = @MENSAGEM + 'Mensagem: ' + ERROR_MESSAGE() + ' - '
	  SET @MENSAGEM = @MENSAGEM + 'Grau de severidade do erro: ' + CONVERT(VARCHAR(10), ERROR_SEVERITY()) + ' - '
	  SET @MENSAGEM = @MENSAGEM + 'Estado do erro: ' + CONVERT(VARCHAR(10), ERROR_STATE()) + ' - '
	  SET @MENSAGEM = @MENSAGEM + 'Número da linha: ' + CONVERT(VARCHAR(10), ERROR_LINE()) + ' - '
	  SET @MENSAGEM = @MENSAGEM + 'Procedure: ' + ERROR_PROCEDURE()
  END CATCH
END
```

---
## **Cursor**
>É um objeto que aponta para uma determinada linha dentro de um conjunto.

- **Metodos**

|METODO|Descricao|
|---|---|
|FORWARD_ONLY && SCROLL|Indica a rolagem a ser definida|
|STATIC, KEYSET, DYNAMIC e FAST_FORWARD| Usado para definir o tipo do cursor |

- **TIPOS:**

|TIPO|Descricao|
|---|---|
|Static| Faz uma cópia dos dados e é sempre somente leitura|
|Keyset| Faz uma cópia dos dados e deverá ter um índice exclusivo que defina o conjunto de chaves a ser copiado|
|Dynamic| Lançada uma consulta novamente sempre que uma linha fosse referenciada|
|Firehose| Faz uma cópia dos dados e somente avança as linhas |

- **Manipulando linhas**

**Fetch** Recupera uma linha especifica do conjunto do cursor

|Fetch|Descricao|
|---|---|
|FIRST | Retorna a primeira linha da variável |
|NEXT | Retorna a linha seguinte, depois de aberto retorna a primeira linha |
|PRIOR | Retorna a linha anterior |
|RELATIVE n | Retorna a linha n |
|ABSOLUNT n | Pode especificar linhas antes da linha atual |

**UPDATE** Altera linha

 **DELETE** Deleta linha

 - **Monitoramento**

**@@FETCH_STATUS**

 |Retorno|Descricao|
 |---|---|
| 0	| O FETCH foi realizado com sucesso.|
|-1|	O FETCH falhou.|
|-2|	O registro trazido foi perdido.|

 **@@CURSOR_ROWS**
 
 |Retorno|Descricao|
 |---|---|
| -m|	O cursor ainda não foi completamente preenchido.|
|-1	| O cursor é dinâmico e o número de linhas pode variar.|
| 0	| Ou nenhum cursor foi aberto ou o mais recente não foi fechado e liberado ou o cursor contem 0 linhas.|
| N	| O número de linhas no cursor.|

- **Usando:**

|Parametros|Descricao| 
|---|---|
| **Open cursor_NOME**| Cria o conjunto de linhas que serão manipuladas|
| **Close cursor_NOME** | Libera os recursos usados para manter o conjunto do cursor |
| **Deallocate cursor_NOME** | Remove o identificador do cursor e não o cursor ou variável |

**EXEMPLO 1**
``` sql
declare cursor_NOME cursor forward_only 
for select COLUNA from TABELA

declare @VAR1 int
declare @VAR2 varchar(60)
declare @VAR3 decimal(10,2)

open cursor_NOME -- Cria o conjunto de linhas que serão manipuladas

fetch next from cursor_NOME 
	into @VAR1, @VAR2, @VAR3

while (@@FETCH_STATUS = 0 ) begin
	print  @VAR2 +  cast(@VAR3 as varchar(60))

	fetch next from cursor_NOME
		into @VAR1, @VAR2, @VAR3
end

close cursor_NOME -- Libera os recursos usados para manter o conjunto do cursor

deallocate cursor_NOME -- Remove o identificador do cursor e não o cursor ou variável
```

**EXEMPLO 2**
``` sql
declare cursor_NOME cursor keyset 
for select COLUNA from TABELA
for update

open cursor_NOME -- Cria o conjunto de linhas que serão manipuladas

fetch cursor_NOME 

update TABELA set COLUNA = 'bla' where CURRENT OF cursor_NOME 

close cursor_NOME -- Libera os recursos usados para manter o conjunto do cursor

deallocate cursor_NOME -- Remove o identificador do cursor e não o cursor ou variável
```
---
## **Funcoes**
> Ferramentas do banco de dados para auxiliar o SQL, as funcoes podem variar de banco para banco 

- [SQLServer Documentacao](https://docs.microsoft.com/pt-br/sql/t-sql/functions/functions?view=sql-server-ver15) 

- **Criando**
> Podemos criar as proprias funcoes com o esquema abaixo, e fica salvo dentro do banco na pasta programacao > funcoes

```sql
CREATE FUNCTION NOME (@VAR_ENTRADA AS INT /*Entrada*/) RETURNS TIPO_DE_RETORNO --Tipo de variavel que devemos retornar, podemos retornar tabelas tambem
AS
BEGIN
  DECLARE @RETORNO FLOAT
  --LOGICA SQL
  RETURN @RETORNO
END

--Usando
[NOME](var)
```


---
## **Indice**
> Organiza os dados para agilizar busca mais criando uma arvore mas isso diminui de mais o desempenho nas alteracoes, inclusoes ou exlusoes

- **Criacao:** Temos que criar um Indece para cada coluna

- **Destino:** Nome_BANCO > Tabelas > Nome_Tabela > Indices > Indice_Nome > 
``` sql
CREATE INDEX INDICE_NOME
ON TABELA(COLUNA)
```


---
## **Schema**
> E a ponte de associação entre o usuário e o objeto (sobrenome)
``` sql
-- CRIANDO
CREATE SCHEMA Schema_NOME

-- USANDO
CREATE TABLE Schema_NOME.TABELA (
COD INT,
NOME VARCHAR (255));
```
---
## **Sequences**
- **Caminho:** Programmability - Sequences - NOME
>É um objeto independente, que pode ser utilizado pra preencher qualquer coluna
``` sql
-- criando sequence que adiciona 1 a 1
CREATE SEQUENCE [Schema_NOME].[SeqNOME] 
 AS [bigint]
 START WITH 1
 INCREMENT BY 1
 MINVALUE -9223372036854775808
 MAXVALUE 9223372036854775807
 CACHE  10 
GO
```
- **Usando**
``` sql
ALTER TABLE SCHEMA.TABELA ADD  DEFAULT (NEXT VALUE FOR SCHEMA.SeqNOME) FOR COLUNA
GO
```
---
## **Transaquition**
- **Commit** sobe as alteracoes
- **Rollback** nao sobe nenhuma alteracao
> propriedade da Microsoft, tem por objetivo preservar a integridade e a consistência dos dados
```sql
BEGIN TRANSACTION 

update [db_demonstracao].[acesso].[Usuario]
SET [Login_Usuario] = 'zezao'
WHERE [Id_Usuario] = 1

 -- rollback tran
 commit tran
``` 
---
## **Merge**

``` sql
MERGE INTO TABELA1 apelido
USING SELECT * FROM TABELA2
    ON TABELA1.COLUNAA = TABELA2.COLUNAB
WHEN MATCHED THEN 
    --QUANDO FOR IGUAL
WHEN NOT MATCHED BY TARGET THEN
    --QUANDO FOR DIFERENTE PELA TABELA2
WHEN NOT MATCHED BY SOURCE THEN
    --QUANDO FOR DIFERENTE PELA TABELA1
```
---

## **DTS**
> Codigo SQL onde temos um fluxo a ser seguido, escrevemos ele no Visual Studio e exportamos para o Servidor do banco

- [DTS](https://github.com/luizgustavo77/Notes/blob/master/Developer/Back/BD.md#dts-data-transformation-services)

- **Caminho**   
    Integration Services Catalog > File > Projects > NomeProject  > DTS

---

## **Jobs**
> Funciona como um crontab e nele podemos agendar DTS, SP, outros.. Para rodar de tempos em tempos e tem configurações personalizadas

- **Caminho** SQL Server Agent > Job Activity Monitor
- **Novo** Jobs > click direito  > New Job
- **Configurações**
    - **General** Descricao
    - **Steps** Fluxo de scripts para executar, onde podemos passar outros DTS tambem
    - **Schedules** Cron com periodo que deve rodar
    - **Alert** Configura Alertas para diferentes retornos 

- **Start Job with Storage Procedure** 
> Para podermos startar um Job de dentro de uma aplicação a solução possivel e chamar um Storage Procedure que faça isso para nos      

**Storage Procedure que adicionamos no nosso Database**
``` SQL
-- Storage Procedure que adicionamos no nosso Database
CREATE PROC spStartMyJob @MyJobName sysname -- Espera o nome completo do Job
AS
DECLARE @ReturnCode tinyint -- 0 (success) or 1 (failure)
EXEC @ReturnCode=msdb.dbo.sp_start_job @job_name=@MyJobName;
RETURN (@ReturnCode)
GO
```
**Storage Procedure que inicia o Job**
``` sql
-- Storage Procedure que inicia o Job
USE [msdb]
GO
/****** Object:  StoredProcedure [dbo].[sp_start_job]    Script Date: 30/01/2020 08:50:41 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER OFF
GO
ALTER PROCEDURE [dbo].[sp_start_job]
  @job_name    sysname          = NULL,
  @job_id      UNIQUEIDENTIFIER = NULL,
  @error_flag  INT              = 1,    -- Set to 0 to suppress the error from sp_sqlagent_notify if SQLServerAgent is not running
  @server_name sysname          = NULL, -- The specific target server to start the [multi-server] job on
  @step_name   sysname          = NULL, -- The name of the job step to start execution with [for use with a local job only]
  @output_flag INT              = 1     -- Set to 0 to suppress the success message
AS
BEGIN
  DECLARE @job_id_as_char VARCHAR(36)
  DECLARE @retval         INT
  DECLARE @step_id        INT
  DECLARE @job_owner_sid  VARBINARY(85)

  SET NOCOUNT ON

  -- Remove any leading/trailing spaces from parameters
  SELECT @job_name    = LTRIM(RTRIM(@job_name))
  SELECT @server_name = UPPER(LTRIM(RTRIM(@server_name)))
  SELECT @step_name   = LTRIM(RTRIM(@step_name))

  -- Turn [nullable] empty string parameters into NULLs
  IF (@job_name = N'')    SELECT @job_name = NULL
  IF (@server_name = N'') SELECT @server_name = NULL
  IF (@step_name = N'')   SELECT @step_name = NULL

  EXECUTE @retval = sp_verify_job_identifiers '@job_name',
                                              '@job_id',
                                               @job_name OUTPUT,
                                               @job_id   OUTPUT,
                                               @owner_sid = @job_owner_sid OUTPUT
  IF (@retval <> 0)
    RETURN(1) -- Failure

  -- Check permissions beyond what's checked by the sysjobs_view
  -- SQLAgentReader role can see all jobs but
  -- cannot start/stop jobs they do not own
  IF (@job_owner_sid <> SUSER_SID()                      -- does not own the job
     AND (ISNULL(IS_SRVROLEMEMBER(N'sysadmin'), 0) = 0)     -- is not sysadmin
     AND (ISNULL(IS_MEMBER(N'SQLAgentOperatorRole'), 0) = 0))  -- is not SQLAgentOperatorRole
  BEGIN
   RAISERROR(14393, -1, -1);  
   RETURN(1) -- Failure
  END

  IF (NOT EXISTS (SELECT *
                  FROM msdb.dbo.sysjobservers
                  WHERE (job_id = @job_id)))
  BEGIN
    SELECT @job_id_as_char = CONVERT(VARCHAR(36), @job_id)
    RAISERROR(14256, -1, -1, @job_name, @job_id_as_char)
    RETURN(1) -- Failure
  END

  IF (EXISTS (SELECT *
              FROM msdb.dbo.sysjobservers
              WHERE (job_id = @job_id)
                AND (server_id = 0)))
  BEGIN
    -- The job is local, so start (run) the job locally

    -- Check the step name (if supplied)
    IF (@step_name IS NOT NULL)
    BEGIN
      SELECT @step_id = step_id
      FROM msdb.dbo.sysjobsteps
      WHERE (step_name = @step_name)
        AND (job_id = @job_id)

      IF (@step_id IS NULL)
      BEGIN
        RAISERROR(14262, -1, -1, '@step_name', @step_name)
        RETURN(1) -- Failure
      END
    END

    EXECUTE @retval = msdb.dbo.sp_sqlagent_notify @op_type     = N'J',
                                                  @job_id      = @job_id,
                                                  @schedule_id = @step_id, -- This is the start step
                                                  @action_type = N'S',
                                                  @error_flag  = @error_flag
    IF ((@retval = 0) AND (@output_flag = 1))
      RAISERROR(14243, 0, 1, @job_name)
  END
  ELSE
  BEGIN
    -- The job is a multi-server job

      -- Only sysadmin can start multi-server job
      IF (ISNULL(IS_SRVROLEMEMBER(N'sysadmin'), 0) <> 1)
      BEGIN
         RAISERROR(14397, -1, -1);
         RETURN(1) -- Failure
      END            

    -- Check target server name (if any)
    IF (@server_name IS NOT NULL)
    BEGIN
      IF (NOT EXISTS (SELECT *
                      FROM msdb.dbo.systargetservers
                      WHERE (UPPER(server_name) = @server_name)))
      BEGIN
        RAISERROR(14262, -1, -1, '@server_name', @server_name)
        RETURN(1) -- Failure
      END
    END

    -- Re-post the job if it's an auto-delete job
    IF ((SELECT delete_level
         FROM msdb.dbo.sysjobs
         WHERE (job_id = @job_id)) <> 0)
      EXECUTE @retval = msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', @job_id, @server_name

    -- Post start instruction(s)
    EXECUTE @retval = msdb.dbo.sp_post_msx_operation 'START', 'JOB', @job_id, @server_name
  END

  RETURN(@retval) -- 0 means success
END

```
---
## **Backup**
> Arquivos para armazenar o banco em caso de perda de dados, o arquivo fica salvo como NOME.bak

- **INIT & NOT INIT**
> Informa se o banco devera adicionar informacoes ou vai criar um novo backup dentro do arquivo ja existente

- **Full**
> Completo, o SQL vai armazenar o conteudo, estrutura e logs 
``` sql
BACKUP DATABASE NOME TO DISK = 'C:\CAMINHO' WITH INIT 
```

- **Transact**
> Copia as alteracoes des do ultimo backup, ou seja precisa ter sido feito um Backup Full 
``` sql
BACKUP LOG NOME TO DISK = 'C:\CAMINHO' WITH NOINIT
```

- **Diferencial**
> Prixomo do full mas mapeia apenas as diferencas e é considerado melhor que o transact
``` sql
BACKUP DATABASE NOME TO DISK = 'C:\CAMINHO' WITH DIFFERENTIAL 
```

- **Importando Banco:**
  - Click com direito em Banco De Dados > Restaurar Banco de dados > Dispositivo > ARQUIVO.BAK > OK
``` sql
-- VERIFICA ESTADO DOS BAK RETORNA 1 PARA OK E 0 PARA ERRO
RESTORE VERIFYONLY FROM DISK = `C:\CAMINHO\NOME.bak` WITH CHECKSUM

-- VERIFICA O BAK E RETORNA UM LOG NA ORDEM DOS BACKUPS CRIADOS NELE
RESTORE HEADERONLY FROM DISK = 'C:\CAMINHO\NOME.bak'

-- AGORA SIM O BACKUP
RESTORE DATABASE NOMEBANCO FROM DISK = 'C:\CAMINHO' WITH FILE = 'NUMERO DO BACKUP' WITH RECOVERY
```

- **Importando e exportando dados do banco:**
  - Click com direito > tasks > IMPORT DATA/EXPORT DATA

- **Exemplo de policita de BKP**
  - Full 1:00
  - 4:00 - 8:00 backup de logs de 2 em 2 horas
  - as 9:00 um backup diferencial
  - 10:00 - 14:00 backup de transacoes
  - 2:00 backup diferencial
  - 3:00 - 9:00 backup de transacoes

``` SQL
-- 1:00 AM -- BACKUP FULL INICIAL QUE SUBSTITUI OS BACKUPS DO DIA ANTERIOR
BACKUP DATABASE NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH INIT

-- 4:00 AM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 6:00 AM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 8:00 AM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 9:00 AM - BACKUP DIFERENCIAL
BACKUP DATABASE NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH DIFFERENTIAL

-- 10:00 AM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 12:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 14:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 14:00 PM - BACKUP DIFERENCIAL
BACKUP DATABASE NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH DIFFERENTIAL

-- 15:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 17:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 19:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT

-- 21:00 PM - BACKUP LOG
BACKUP LOG NOME TO DISK = 'C:\Temp\SQL\NOME_COMPLETO.BAK'
WITH NOINIT
```

---
## **Autenticacao**
> Usuario e permissoes sao necessarios para garantir a seguranca do servidor

- Os processos de acesso de usuario podem ser feitos em:
  - Segurança > Logins

- **Usuario padrao do SQL SERVER**
  - **NT SERVICE\MSSQLSERVER** - Para servicos do DB
  - **NT SERVICE\SQLSERVERAGENT** - Para os servicos do agente do sql server

- Criando grupo\usuario de login para o Windows
``` sql
CREATE LOGIN [SQLSERVER\USUARIO] FROM WINDOWS
-- A senha vem do usuario windows
```

- Criando usuario SQLSERVER
``` sql
CREATE LOGIN [USUARIO] WITH PASSWORD = 'SENHA'
```

- Dando permissoes
  - Documentacao: [Microsoft](https://docs.microsoft.com/pt-br/sql/relational-databases/security/authentication-access/database-level-roles)
```sql
ALTER SERVER ROLE [AUTORIZACAO] ADD MEMBER [USUARIO]
```


---
## **Observacao:**
- **Quantidade de digitos com 2 numeros**
> primeiro numero se trata do numero max de caracters e o segundo o numero de caracters depois da virgula (virgula conta como caracter)

``` sql
create table NOME (
	COLUNA1 int (10,2),
 	COLUNA2 varchar (50),
    primary key (COLUNA1)); 
```
---

## **External Name**
> Exportar a DLL do C# para o SQL, o nome da função especificada deve ser exatamente igual, inclusive maiúsculas e minúsculas, ao nome da função na DLL.

```sql
--Registra a funcao
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--chamando xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
```

---

## **Visual Studio**
> O visual studio tem ferramentas para usar com o banco que fazem toda a diferença.   
- **New Project > SQL Server Database Project** Aqui podemos mapear um banco ja existente ou criar um banco novo e despois criar ele no servidor.

- **Tools >  SqlServer > Data Comparison** Usado para replicar os dados, podemos descer todos os dados inseridos direto na outra tabela.
- **Tools >  SqlServer > Schema Comparison** Usado para replicar a arquitetura da tabela com storage procedures, views, tabela...

- **View > SQL SERVER OBJECT EXPLORER** Ferramenta parecida com o SQL MANAGEMENT STUDIO
---
## **SQL Server Managemente**
  - **Active Monitor**
    - Botao direito no servidor > Monitor de atividades
  - **SQL SERVER PROFILE**
    - Monitor de picos de atividades no Servidor para monitorar a performace do servidor
    - (Menu superior)Ferramentas > SQL Server Profile > 

 - **DATABASE > Tasks > Genarate Scripts** Para gerar scripts como um DUMP da arquitetura do banco

- **sp_who2** Lista processos
``` sql
 create Table #TABLE(
        SPID INT,
        Status VARCHAR(MAX),
        LOGIN VARCHAR(MAX),
        HostName VARCHAR(MAX),
        BlkBy VARCHAR(MAX),
        DBName VARCHAR(MAX),
        Command VARCHAR(MAX),
        CPUTime INT,
        DiskIO INT,
        LastBatch VARCHAR(MAX),
        ProgramName VARCHAR(MAX),
        SPID_1 INT,
        REQUESTID INT
)

INSERT INTO #Table EXEC sp_who2

SELECT  *
FROM #TABLE
WHERE ...

DROP TABLE #TABLE
```
- **kill NUMERO** Mata processo

- Podemos consultar os logins consultando a tabela com
```sql
master.sys.sql_logins

-- informacoes do login
SELECT name, LOGINPROPERTY(nome, 'TIPO_DE_PROPRIEDADE') FROM master.sys.sql_logins
```
---

## **Plano de Consulta**
> Previa do que o SQL vai fazer ao rodar um T-SQL, retorna um custo para essa funcao e retorna uma alternativa para melhorar esse SQL 

- SCAN, VARREDURA: Varre toda a tabela
- SEEK, BUSCA: Vai a partir de um indice

- Incluir no comando SQL o Plano de consulta
  - ctrl + m, e na resposta do servidor podemos ver o plano de cunsulta 
