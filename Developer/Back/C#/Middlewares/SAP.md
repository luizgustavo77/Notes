# **SAP**
> Como chamar funções do SAP 

- **Requisitos**
    - SAP Gir Biztalk
    - References > sapnco && sapnco_utils
    - using SAP.Middleware.Connector;

- **Modelo**
``` c#
public class ConexaoSapBase : IDestinationConfiguration
    {
        private struct PARAMETROS
        {
            public const string SystemNumber = "02";
            public const string Client = "200";
            public const string User = "USUARIO";
            public const string Password = "SENHA";
            public const string Language = "PT";
        }

        public bool ChangeEventsSupported() { return false; }
        public event RfcDestinationManager.ConfigurationChangeHandler ConfigurationChanged;

        public RfcConfigParameters GetParameters(string ambiente)
        {
            RfcConfigParameters config = new RfcConfigParameters();
            string hostAddress = string.Empty;

            switch (ambiente)
            {
                case "MeuSAP1":
                    hostAddress = "192.168.1.1";
                    break;
                case "MeuSAP2":
                    hostAddress = "192.168.1.1";
                    break;
                case "MeuSAP3":
                    hostAddress = "192.168.1.1";
                    break;
            }

            config.Add(RfcConfigParameters.AppServerHost, hostAddress);
            config.Add(RfcConfigParameters.SystemNumber, PARAMETROS.SystemNumber);
            config.Add(RfcConfigParameters.Client, PARAMETROS.Client);
            config.Add(RfcConfigParameters.User, PARAMETROS.User);
            config.Add(RfcConfigParameters.Password, PARAMETROS.Password);
            config.Add(RfcConfigParameters.Language, PARAMETROS.Language);

            PingReply oPing = new Ping().Send(hostAddress, 2000);

            return config;
        }        
    }

public FuncaoSAP Executar(TabelaEntrada dtoPesquisa)
{    
    string NomeRFC = "FuncaoSAP";

    FuncaoSAPDto retorno = new FuncaoSAPDto();
    ConexaoSapBase conexaoSAP = new ConexaoSapBase();

    try
    {
        // Abre coneccao
        RfcDestinationManager.RegisterDestinationConfiguration(conexaoSAP);
        RfcDestination destination = RfcDestinationManager.GetDestination("MeuSap1");
        RfcRepository repository = destination.Repository;
        IRfcFunction funcaoRfc = repository.CreateFunction(NomeRFC);

        // Converte nossa entrada para a entrada do SAP
        IRfcTable TabelaEntradaTabelaEntrada = funcaoRfc.GetTable("TabelaEntrada");
        TabelaEntradaTabelaEntrada.Append();
        TabelaEntradaTabelaEntrada.SetValue("VariavelEntrada", dtoPesquisa.Variavel);

        //Faz a consulta
        funcaoRfc.Invoke(destination);

        //Procura o retorno
        IRfcTable entidade = funcaoRfc.GetTable("TabelaSaida");

        //Busca resultados da consulta 
        if (entidade.RowCount > 0)
        {
            retorno.Resultado = false;

            foreach (IRfcStructure item in entidade)
            {
                retorno.LENUM = item.GetString("LENUM");
                retorno.LGNUM = item.GetString("LGNUM");
                retorno.LQNUM = item.GetString("LQNUM");
            }
        }

        //se existir algum item com erro, gero erro geral
        if (retorno.LENUM == null)
        {
            throw new Exception("ERRO, sem retorno");
        }

        retorno.Resultado = true;
    }
    catch (Exception ex)
    {
        retorno.Resultado = false;
        retorno.Mensagem = ex.Message;
    }
    finally
    {
        // Fecha coneccao
        RfcDestinationManager.UnregisterDestinationConfiguration(conexaoSAP);
    }
    return retorno;
}
```
