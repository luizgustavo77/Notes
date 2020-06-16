# **XML && JSON**
> Formato de arquivos para criar objetos que podem ser recuperados

## **XML**
- **Serializar:** Transforma o Objeto em um XML
``` c#
//Objeto
[Serializable]
[XmlRoot("result"), XmlType("result")]
public class Result
{
    [XmlElement("resourceName")]
    public string resourceName { get; set; }
    [XmlElement("size")]
    public string size { get; set; }
    [XmlArray("entries")]
    public List<entry> entries { get; set; }

    [XmlType("entry")]
    public class entry
    {
        [XmlAttribute("id")]
        public string id { get; set; }
        [XmlAttribute("link")]
        public string link { get; set; }
    }
}

//Codigo
CLASSE obj = new CLASSE();
DataContractSerializer serializer = new DataContractSerializer(typeof(CLASSE));
XmlDictionaryWriter xdw = XmlDictionaryWriter.CreateTextWriter(someStream,Encoding.UTF8 );
serializer.WriteObject(xdw, obj);
//OU
XmlSerializer serializador = new XmlSerializer(typeof(CLASSE));
string xml = writer.ToString();
TextReader reader = new StringReader(xml);
CLASSE c = serializador.Deserialize(reader) as CLASSE;
```

- **Deserializador:** Transforma um arquivo XML em um objeto 
``` c#
XmlSerializer serializer = new XmlSerializer(typeof(CLASSE));
FileStream arquivo = new FileStream("ARQUIVO.xml", FileMode.Open);
CLASSE obj = (CLASSE)serializer.Deserialize(arquivo)
```

- **Enviar Objetos**
``` c#
[DataContract]
public class CLASSE
{
    [DataMember]
    public string Name;
}
```


- Exemplo de **XML**
``` xml
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<Root>
  <EmployeeInfo>
    <Name>Jane Winston</Name>
    <Date>2001-01-01</Date>
    <Code>0001</Code>
  </EmployeeInfo>
  <ExpenseItem>
    <Date>2001-01-01</Date>
    <Description>Airfare</Description>
    <Amount>500.34</Amount>
  </ExpenseItem>
</Root>
```
---

## **JSON**

- **Serializar:** Transforma o objeto em um JSON
```c#
//Objeto

[JsonObject("CLASSE")]
public class CLASSE
{
    [JsonProperty("id")]
    public int id { get; set; }

    [JsonProperty("nome")]
    public string Nome { get; set; }
}

//Codigo
CLASSE obj = new CLASSE();
JavaScriptSerializer serializer = new JavaScriptSerializer();
var serializedResult = serializer.Serialize(CLASSE);

```

- **Deserializador:** Transforma JSON em objeto
``` c#
// Com NewtonSoft
private static List<CLASS> GetCLASSs()
{
    var json = File.ReadAllText("NOME.json");
    var retorno = JsonConvert.DeserializeObject<List<CLASS>>(json);
    return retorno;
}

// OU

public static CLASS GetCLASS(string json)
{
    var ser = new JavaScriptSerializer();
    return ser.Deserialize<Cliente>(json);
}
```

- Exemplo de **JSON**
```json
{
  "Name": "Jane Winston",
  "Date": "2001-01-01",
  "Code": 001,
  "genero": ["masculoni", "feminino", "outros"] 
}
```
