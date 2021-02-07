---
description: 'Saiba mais sobre: token personalizado'
title: Token personalizado
ms.date: 03/30/2017
ms.assetid: e7fd8b38-c370-454f-ba3e-19759019f03d
ms.openlocfilehash: 500cc187db0280e508ef079ca370483c716ea2c5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752425"
---
# <a name="custom-token"></a>Token personalizado

Este exemplo demonstra como adicionar uma implementação de token personalizada a um aplicativo Windows Communication Foundation (WCF). O exemplo usa um `CreditCardToken` para transmitir informações com segurança sobre cartões de crédito do cliente para o serviço. O token é passado no cabeçalho da mensagem de WS-Security e é assinado e criptografado usando o elemento de ligação de segurança simétrica junto com o corpo da mensagem e outros cabeçalhos de mensagem. Isso é útil em casos em que os tokens internos não são suficientes. Este exemplo demonstra como fornecer um token de segurança personalizado para um serviço em vez de usar um dos tokens internos. O serviço implementa um contrato que define um padrão de comunicação de solicitação-resposta.

> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.

 Para resumir, este exemplo demonstra o seguinte:

- Como um cliente pode passar um token de segurança personalizado para um serviço.

- Como o serviço pode consumir e validar um token de segurança personalizado.

- Como o código do serviço WCF pode obter as informações sobre tokens de segurança recebidos, incluindo o token de segurança personalizado.

- Como o certificado X. 509 do servidor é usado para proteger a chave simétrica usada para criptografia e assinatura de mensagens.

## <a name="client-authentication-using-a-custom-security-token"></a>Autenticação de cliente usando um token de segurança personalizado

 O serviço expõe um único ponto de extremidade que é criado programaticamente usando `BindingHelper` `EchoServiceHost` classes e. O ponto de extremidade consiste em um endereço, uma associação e um contrato. A associação é configurada com uma associação personalizada usando `SymmetricSecurityBindingElement` e `HttpTransportBindingElement` . Este exemplo define o `SymmetricSecurityBindingElement` para usar o certificado X. 509 de um serviço para proteger a chave simétrica durante a transmissão e passar um personalizado `CreditCardToken` em um cabeçalho de mensagem de WS-Security como um token de segurança assinado e criptografado. O comportamento especifica as credenciais de serviço que devem ser usadas para autenticação de cliente e também informações sobre o certificado X. 509 do serviço.

```csharp
public static class BindingHelper
{
    public static Binding CreateCreditCardBinding()
    {
        var httpTransport = new HttpTransportBindingElement();

        // The message security binding element will be configured to require a credit card.
        // The token that is encrypted with the service's certificate.
        var messageSecurity = new SymmetricSecurityBindingElement();
        messageSecurity.EndpointSupportingTokenParameters.SignedEncrypted.Add(new CreditCardTokenParameters());
        X509SecurityTokenParameters x509ProtectionParameters = new X509SecurityTokenParameters();
        x509ProtectionParameters.InclusionMode = SecurityTokenInclusionMode.Never;
        messageSecurity.ProtectionTokenParameters = x509ProtectionParameters;
        return new CustomBinding(messageSecurity, httpTransport);
    }
}
```

 Para consumir um token de cartão de crédito na mensagem, o exemplo usa credenciais de serviço personalizadas para fornecer essa funcionalidade. A classe de credenciais de serviço está localizada na `CreditCardServiceCredentials` classe e é adicionada às coleções de comportamentos do host de serviço no `EchoServiceHost.InitializeRuntime` método.

```csharp
class EchoServiceHost : ServiceHost
{
    string creditCardFile;

    public EchoServiceHost(parameters Uri[] addresses)
        : base(typeof(EchoService), addresses)
    {
        creditCardFile = ConfigurationManager.AppSettings["creditCardFile"];
        if (string.IsNullOrEmpty(creditCardFile))
        {
            throw new ConfigurationErrorsException("creditCardFile not specified in service config");
        }

        creditCardFile = String.Format("{0}\\{1}", System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath, creditCardFile);
    }

    override protected void InitializeRuntime()
    {
        // Create a credit card service credentials and add it to the behaviors.
        CreditCardServiceCredentials serviceCredentials = new CreditCardServiceCredentials(this.creditCardFile);
        serviceCredentials.ServiceCertificate.SetCertificate("CN=localhost", StoreLocation.LocalMachine, StoreName.My);
        this.Description.Behaviors.Remove((typeof(ServiceCredentials)));
        this.Description.Behaviors.Add(serviceCredentials);

        // Register a credit card binding for the endpoint.
        Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();
        this.AddServiceEndpoint(typeof(IEchoService), creditCardBinding, string.Empty);

        base.InitializeRuntime();
    }
}
```

 O ponto de extremidade do cliente é configurado de maneira semelhante ao ponto de extremidade de serviço. O cliente usa a mesma `BindingHelper` classe para criar uma associação. O restante da instalação está localizado na `Client` classe. O cliente também define as informações a serem contidas no `CreditCardToken` e no certificado X. 509 no código de instalação, adicionando uma `CreditCardClientCredentials` instância com os dados apropriados à coleção de comportamentos de ponto de extremidade do cliente. O exemplo usa o certificado X. 509 com o nome da entidade definido como `CN=localhost` o certificado de serviço.

```csharp
Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();
var serviceAddress = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");

// Create a client with given client endpoint configuration.
channelFactory = new ChannelFactory<IEchoService>(creditCardBinding, serviceAddress);

// Configure the credit card credentials on the channel factory.
var credentials =
      new CreditCardClientCredentials(
      new CreditCardInfo(creditCardNumber, issuer, expirationTime));
// Configure the service certificate on the credentials.
credentials.ServiceCertificate.SetDefaultCertificate(
      "CN=localhost", StoreLocation.LocalMachine, StoreName.My);

// Replace ClientCredentials with CreditCardClientCredentials.
channelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));
channelFactory.Endpoint.Behaviors.Add(credentials);

client = channelFactory.CreateChannel();

Console.WriteLine($"Echo service returned: {client.Echo()}");

((IChannel)client).Close();
channelFactory.Close();
```

## <a name="custom-security-token-implementation"></a>Implementação do token de segurança personalizado

 Para habilitar um token de segurança personalizado no WCF, crie uma representação de objeto do token de segurança personalizado. O exemplo tem essa representação na `CreditCardToken` classe. A representação do objeto é responsável por manter todas as informações de token de segurança relevantes e fornecer uma lista de chaves de segurança contidas no token de segurança. Nesse caso, o token de segurança do cartão de crédito não contém nenhuma chave de segurança.

 A próxima seção descreve o que deve ser feito para permitir que um token personalizado seja transmitido pela rede e consumido por um ponto de extremidade do WCF.

```csharp
class CreditCardToken : SecurityToken
{
    CreditCardInfo cardInfo;
    DateTime effectiveTime = DateTime.UtcNow;
    string id;
    ReadOnlyCollection<SecurityKey> securityKeys;

    public CreditCardToken(CreditCardInfo cardInfo) : this(cardInfo, Guid.NewGuid().ToString()) { }

    public CreditCardToken(CreditCardInfo cardInfo, string id)
    {
        if (cardInfo == null)
            throw new ArgumentNullException(nameof(cardInfo));

        if (id == null)
            throw new ArgumentNullException(nameof(id));

        this.cardInfo = cardInfo;
        this.id = id;

        // The credit card token is not capable of any cryptography.
        this.securityKeys = new ReadOnlyCollection<SecurityKey>(new List<SecurityKey>());
    }

    public CreditCardInfo CardInfo { get { return this.cardInfo; } }

    public override ReadOnlyCollection<SecurityKey> SecurityKeys { get { return this.securityKeys; } }

    public override DateTime ValidFrom { get { return this.effectiveTime; } }
    public override DateTime ValidTo { get { return this.cardInfo.ExpirationDate; } }
    public override string Id { get { return this.id; } }
}
```

## <a name="getting-the-custom-credit-card-token-to-and-from-the-message"></a>Obtendo o token do cartão de crédito personalizado de e para a mensagem

 Os serializadores de token de segurança no WCF são responsáveis por criar uma representação de objeto de tokens de segurança do XML na mensagem e criar um formulário XML dos tokens de segurança. Eles também são responsáveis por outras funcionalidades, como leitura e gravação de identificadores de chave que apontam para tokens de segurança, mas este exemplo usa apenas a funcionalidade relacionada ao token de segurança. Para habilitar um token personalizado, você deve implementar seu próprio serializador de token de segurança. Este exemplo usa a `CreditCardSecurityTokenSerializer` classe para essa finalidade.

 No serviço, o serializador personalizado lê o formulário XML do token personalizado e cria a representação de objeto de token personalizado a partir dele.

 No cliente, a `CreditCardSecurityTokenSerializer` classe grava as informações contidas na representação do objeto de token de segurança no gravador de XML.

```csharp
public class CreditCardSecurityTokenSerializer : WSSecurityTokenSerializer
{
    public CreditCardSecurityTokenSerializer(SecurityTokenVersion version) : base() { }

    protected override bool CanReadTokenCore(XmlReader reader)
    {
        XmlDictionaryReader localReader = XmlDictionaryReader.CreateDictionaryReader(reader);

        if (reader == null)
            throw new ArgumentNullException(nameof(reader));

        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))
            return true;

        return base.CanReadTokenCore(reader);
    }

    protected override SecurityToken ReadTokenCore(XmlReader reader, SecurityTokenResolver tokenResolver)
    {
        if (reader == null)
            throw new ArgumentNullException(nameof(reader));

        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))
        {
            string id = reader.GetAttribute(Constants.Id, Constants.WsUtilityNamespace);

            reader.ReadStartElement();

            // Read the credit card number.
            string creditCardNumber = reader.ReadElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace);

            // Read the expiration date.
            string expirationTimeString = reader.ReadElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace);
            DateTime expirationTime = XmlConvert.ToDateTime(expirationTimeString, XmlDateTimeSerializationMode.Utc);

            // Read the issuer of the credit card.
            string creditCardIssuer = reader.ReadElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace);
            reader.ReadEndElement();

            var cardInfo = new CreditCardInfo(creditCardNumber, creditCardIssuer, expirationTime);

            return new CreditCardToken(cardInfo, id);
        }
        else
        {
            return WSSecurityTokenSerializer.DefaultInstance.ReadToken(reader, tokenResolver);
        }
    }

    protected override bool CanWriteTokenCore(SecurityToken token)
    {
        if (token is CreditCardToken)
            return true;
        return base.CanWriteTokenCore(token);
    }

    protected override void WriteTokenCore(XmlWriter writer, SecurityToken token)
    {
        if (writer == null)
            throw new ArgumentNullException(nameof(writer));
        if (token == null)
            throw new ArgumentNullException(nameof(token));

        CreditCardToken c = token as CreditCardToken;
        if (c != null)
        {
            writer.WriteStartElement(Constants.CreditCardTokenPrefix, Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace);
            writer.WriteAttributeString(Constants.WsUtilityPrefix, Constants.Id, Constants.WsUtilityNamespace, token.Id);
            writer.WriteElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardNumber);
            writer.WriteElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace, XmlConvert.ToString(c.CardInfo.ExpirationDate, XmlDateTimeSerializationMode.Utc));
            writer.WriteElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardIssuer);
            writer.WriteEndElement();
            writer.Flush();
        }
        else
        {
            base.WriteTokenCore(writer, token);
        }
    }
}
```

## <a name="how-token-provider-and-token-authenticator-classes-are-created"></a>Como as classes do provedor de token e do autenticador de token são criadas

 As credenciais de cliente e serviço são responsáveis por fornecer a instância do Gerenciador de token de segurança. A instância do Gerenciador de token de segurança é usada para obter provedores de token, autenticadores de token e serializadores de token.

 O provedor de token cria uma representação de objeto do token com base nas informações contidas nas credenciais do cliente ou do serviço. A representação do objeto token é gravada na mensagem usando o serializador de token (abordado na seção anterior).

 O autenticador de token valida os tokens que chegam na mensagem. A representação de objeto de token de entrada é criada pelo serializador de token. Essa representação de objeto é passada para o autenticador de token para validação. Depois que o token é validado com êxito, o autenticador de token retorna uma coleção de `IAuthorizationPolicy` objetos que representam as informações contidas no token. Essas informações são usadas posteriormente durante o processamento de mensagens para executar decisões de autorização e para fornecer declarações para o aplicativo. Neste exemplo, o autenticador de token de cartão de crédito usa `CreditCardTokenAuthorizationPolicy` para essa finalidade.

 O serializador de token é responsável por obter a representação do objeto do token de e para a conexão. Isso é abordado na seção anterior.

 Neste exemplo, usamos um provedor de token somente no cliente e um autenticador de token somente no serviço, pois queremos transmitir um token de cartão de crédito somente na direção do cliente para o serviço.

 A funcionalidade no cliente está localizada nas `CreditCardClientCredentials` `CreditCardClientCredentialsSecurityTokenManager` `CreditCardTokenProvider` classes e.

 No serviço, a funcionalidade reside nas `CreditCardServiceCredentials` `CreditCardServiceCredentialsSecurityTokenManager` `CreditCardTokenAuthenticator` classes, e `CreditCardTokenAuthorizationPolicy` .

```csharp
    public class CreditCardClientCredentials : ClientCredentials
    {
        CreditCardInfo creditCardInfo;

        public CreditCardClientCredentials(CreditCardInfo creditCardInfo)
            : base()
        {
            if (creditCardInfo == null)
                throw new ArgumentNullException(nameof(creditCardInfo));

            this.creditCardInfo = creditCardInfo;
        }

        public CreditCardInfo CreditCardInfo
        {
            get { return this.creditCardInfo; }
        }

        protected override ClientCredentials CloneCore()
        {
            return new CreditCardClientCredentials(this.creditCardInfo);
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            return new CreditCardClientCredentialsSecurityTokenManager(this);
        }
    }

    public class CreditCardClientCredentialsSecurityTokenManager : ClientCredentialsSecurityTokenManager
    {
        CreditCardClientCredentials creditCardClientCredentials;

        public CreditCardClientCredentialsSecurityTokenManager(CreditCardClientCredentials creditCardClientCredentials)
            : base (creditCardClientCredentials)
        {
            this.creditCardClientCredentials = creditCardClientCredentials;
        }

        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)
        {
            // Handle this token for Custom.
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)
                return new CreditCardTokenProvider(this.creditCardClientCredentials.CreditCardInfo);
            // Return server cert.
            else if (tokenRequirement is InitiatorServiceModelSecurityTokenRequirement)
            {
                if (tokenRequirement.TokenType == SecurityTokenTypes.X509Certificate)
                {
                    return new X509SecurityTokenProvider(creditCardClientCredentials.ServiceCertificate.DefaultCertificate);
                }
            }

            return base.CreateSecurityTokenProvider(tokenRequirement);
        }

        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)
        {

            return new CreditCardSecurityTokenSerializer(version);
        }

    }

    class CreditCardTokenProvider : SecurityTokenProvider
    {
        CreditCardInfo creditCardInfo;

        public CreditCardTokenProvider(CreditCardInfo creditCardInfo) : base()
        {
            if (creditCardInfo == null)
                throw new ArgumentNullException(nameof(creditCardInfo));

            this.creditCardInfo = creditCardInfo;
        }

        protected override SecurityToken GetTokenCore(TimeSpan timeout)
        {
            SecurityToken result = new CreditCardToken(this.creditCardInfo);
            return result;
        }
    }

    public class CreditCardServiceCredentials : ServiceCredentials
    {
        string creditCardFile;

        public CreditCardServiceCredentials(string creditCardFile)
            : base()
        {
            if (creditCardFile == null)
                throw new ArgumentNullException(nameof(creditCardFile));

            this.creditCardFile = creditCardFile;
        }

        public string CreditCardDataFile
        {
            get { return this.creditCardFile; }
        }

        protected override ServiceCredentials CloneCore()
        {
            return new CreditCardServiceCredentials(this.creditCardFile);
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            return new CreditCardServiceCredentialsSecurityTokenManager(this);
        }
    }

    public class CreditCardServiceCredentialsSecurityTokenManager : ServiceCredentialsSecurityTokenManager
    {
        CreditCardServiceCredentials creditCardServiceCredentials;

        public CreditCardServiceCredentialsSecurityTokenManager(CreditCardServiceCredentials creditCardServiceCredentials)
            : base(creditCardServiceCredentials)
        {
            this.creditCardServiceCredentials = creditCardServiceCredentials;
        }

        public override SecurityTokenAuthenticator CreateSecurityTokenAuthenticator(SecurityTokenRequirement tokenRequirement, out SecurityTokenResolver outOfBandTokenResolver)
        {
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)
            {
                outOfBandTokenResolver = null;
                return new CreditCardTokenAuthenticator(creditCardServiceCredentials.CreditCardDataFile);
            }

            return base.CreateSecurityTokenAuthenticator(tokenRequirement, out outOfBandTokenResolver);
        }

        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)
        {
            return new CreditCardSecurityTokenSerializer(version);
        }
    }

    class CreditCardTokenAuthenticator : SecurityTokenAuthenticator
    {
        string creditCardsFile;
        public CreditCardTokenAuthenticator(string creditCardsFile)
        {
            this.creditCardsFile = creditCardsFile;
        }

        protected override bool CanValidateTokenCore(SecurityToken token)
        {
            return (token is CreditCardToken);
        }

        protected override ReadOnlyCollection<IAuthorizationPolicy> ValidateTokenCore(SecurityToken token)
        {
            CreditCardToken creditCardToken = token as CreditCardToken;

            if (creditCardToken.CardInfo.ExpirationDate < DateTime.UtcNow)
                throw new SecurityTokenValidationException("The credit card has expired.");
            if (!IsCardNumberAndExpirationValid(creditCardToken.CardInfo))
                throw new SecurityTokenValidationException("Unknown or invalid credit card.");

            // the credit card token has only 1 claim - the card number. The issuer for the claim is the
            // credit card issuer

            var cardIssuerClaimSet = new DefaultClaimSet(new Claim(ClaimTypes.Name, creditCardToken.CardInfo.CardIssuer, Rights.PossessProperty));
            var cardClaimSet = new DefaultClaimSet(cardIssuerClaimSet, new Claim(Constants.CreditCardNumberClaim, creditCardToken.CardInfo.CardNumber, Rights.PossessProperty));
            var policies = new List<IAuthorizationPolicy>(1);
            policies.Add(new CreditCardTokenAuthorizationPolicy(cardClaimSet));
            return policies.AsReadOnly();
        }

        /// <summary>
        /// Helper method to check if a given credit card entry is present in the User DB
        /// </summary>
        private bool IsCardNumberAndExpirationValid(CreditCardInfo cardInfo)
        {
            try
            {
                using (var myStreamReader = new StreamReader(this.creditCardsFile))
                {
                    string line = "";
                    while ((line = myStreamReader.ReadLine()) != null)
                    {
                        string[] splitEntry = line.Split('#');
                        if (splitEntry[0] == cardInfo.CardNumber)
                        {
                            string expirationDateString = splitEntry[1].Trim();
                            DateTime expirationDateOnFile = DateTime.Parse(expirationDateString, System.Globalization.DateTimeFormatInfo.InvariantInfo, System.Globalization.DateTimeStyles.AdjustToUniversal);
                            if (cardInfo.ExpirationDate == expirationDateOnFile)
                            {
                                string issuer = splitEntry[2];
                                return issuer.Equals(cardInfo.CardIssuer, StringComparison.InvariantCultureIgnoreCase);
                            }
                            else
                            {
                                return false;
                            }
                        }
                    }
                    return false;
                }
            }
            catch (Exception e)
            {
                throw new Exception("BookStoreService: Error while retrieving credit card information from User DB " + e.ToString());
            }
        }
    }

    public class CreditCardTokenAuthorizationPolicy : IAuthorizationPolicy
    {
        string id;
        ClaimSet issuer;
        IEnumerable<ClaimSet> issuedClaimSets;

        public CreditCardTokenAuthorizationPolicy(ClaimSet issuedClaims)
        {
            if (issuedClaims == null)
                throw new ArgumentNullException(nameof(issuedClaims));
            this.issuer = issuedClaims.Issuer;
            this.issuedClaimSets = new ClaimSet[] { issuedClaims };
            this.id = Guid.NewGuid().ToString();
        }

        public ClaimSet Issuer { get { return this.issuer; } }

        public string Id { get { return this.id; } }

        public bool Evaluate(EvaluationContext context, ref object state)
        {
            foreach (ClaimSet issuance in this.issuedClaimSets)
            {
                context.AddClaimSet(this, issuance);
            }

            return true;
        }
    }
```

## <a name="displaying-the-callers-information"></a>Exibindo as informações dos chamadores

 Para exibir as informações do chamador, use o `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` conforme mostrado no código de exemplo a seguir. O `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` contém declarações de autorização associadas ao chamador atual. As declarações são fornecidas pela `CreditCardToken` classe em sua `AuthorizationPolicies` coleção.

```csharp
bool TryGetStringClaimValue(ClaimSet claimSet, string claimType, out string claimValue)
{
    claimValue = null;
    IEnumerable<Claim> matchingClaims = claimSet.FindClaims(claimType, Rights.PossessProperty);
    if (matchingClaims == null)
        return false;
    IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();
    enumerator.MoveNext();
    claimValue = (enumerator.Current.Resource == null) ? null :
        enumerator.Current.Resource.ToString();
    return true;
}

string GetCallerCreditCardNumber()
{
     foreach (ClaimSet claimSet in
         ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)
     {
         string creditCardNumber = null;
         if (TryGetStringClaimValue(claimSet,
             Constants.CreditCardNumberClaim, out creditCardNumber))
             {
                 string issuer;
                 if (!TryGetStringClaimValue(claimSet.Issuer,
                        ClaimTypes.Name, out issuer))
                 {
                     issuer = "Unknown";
                 }
                 return $"Credit card '{creditCardNumber}' issued by '{issuer}'";
        }
    }
    return "Credit card is not known";
}
```

 Quando você executa o exemplo, as solicitações de operação e as respostas são exibidas na janela do console do cliente. Pressione ENTER na janela do cliente para desligar o cliente.

## <a name="setup-batch-file"></a>Arquivo em lotes de instalação

 O arquivo em lotes Setup.bat incluído com este exemplo permite que você configure o servidor com certificados relevantes para executar o aplicativo hospedado pelo IIS que requer segurança baseada em certificado do servidor. Esse arquivo em lotes deve ser modificado para funcionar em computadores ou para funcionar em um caso não hospedado.

 Veja a seguir uma breve visão geral das diferentes seções dos arquivos em lotes para que eles possam ser modificados para serem executados na configuração apropriada.

- Criando o certificado do servidor:

     As linhas a seguir do `Setup.bat` arquivo em lotes criam o certificado do servidor a ser usado. A `%SERVER_NAME%` variável especifica o nome do servidor. Altere essa variável para especificar seu próprio nome de servidor. O padrão neste arquivo em lotes é localhost. Se você alterar a `%SERVER_NAME%` variável, deverá percorrer os arquivos Client.cs e Service.cs e substituir todas as instâncias do localhost pelo nome do servidor que você usa no script Setup.bat.

     O certificado é armazenado no meu repositório (pessoal) no `LocalMachine` local do repositório. O certificado é armazenado no armazenamento LocalMachine para os serviços hospedados pelo IIS. Para serviços hospedados internamente, você deve modificar o arquivo em lotes para armazenar o certificado do cliente no local do repositório CurrentUser, substituindo a cadeia de caracteres LocalMachine por CurrentUser.

    ```bat
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- Instalando o certificado do servidor no repositório de certificados confiáveis do cliente:

     As linhas a seguir no arquivo de Setup.bat lote copiam o certificado do servidor no repositório de pessoas confiáveis do cliente. Essa etapa é necessária porque os certificados gerados por Makecert.exe não são implicitamente confiáveis pelo sistema cliente. Se você já tiver um certificado com raiz em um certificado raiz confiável do cliente — por exemplo, um certificado emitido pela Microsoft — esta etapa de popular o repositório de certificados do cliente com o certificado do servidor não será necessária.

    ```bat
    echo ************
    echo copying server cert to client's TrustedPeople store
    echo ************
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- Para habilitar o acesso à chave privada do certificado do serviço hospedado pelo IIS, a conta de usuário sob a qual o processo hospedado pelo IIS está em execução deve receber as permissões apropriadas para a chave privada. Isso é feito pelas últimas etapas do script de Setup.bat.

    ```bat
    echo ************
    echo setting privileges on server certificates
    echo ************
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R
    iisreset
    ```

> [!NOTE]
> O arquivo em lotes Setup.bat foi projetado para ser executado em um prompt de comando do Visual Studio 2012. A variável de ambiente PATH definida no prompt de comando do Visual Studio 2012 aponta para o diretório que contém os executáveis exigidos pelo script Setup.bat.

#### <a name="to-set-up-and-build-the-sample"></a>Para configurar e compilar o exemplo

1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Para compilar a solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).

#### <a name="to-run-the-sample-on-the-same-computer"></a>Para executar o exemplo no mesmo computador

1. Abra uma janela do prompt de comando do Visual Studio 2012 com privilégios de administrador e execute Setup.bat na pasta de instalação de exemplo. Isso instala todos os certificados necessários para executar o exemplo. Certifique-se de que o caminho inclui a pasta onde Makecert.exe está localizado.

> [!NOTE]
> Certifique-se de remover os certificados executando Cleanup.bat quando terminar com o exemplo. Outros exemplos de segurança usam os mesmos certificados.  
  
1. Inicie o Client.exe do diretório client\bin. A atividade do cliente é exibida no aplicativo de console do cliente.  
  
2. Se o cliente e o serviço não puderem se comunicar, consulte [dicas de solução de problemas para exemplos do WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-run-the-sample-across-computer"></a>Para executar o exemplo no computador  
  
1. Crie um diretório no computador de serviço para os binários de serviço.  
  
2. Copie os arquivos de programa do serviço para o diretório de serviço no computador do serviço. Não se esqueça de copiar CreditCardFile.txt; caso contrário, o autenticador de cartão de crédito não poderá validar as informações de cartão de crédito enviadas do cliente. Copie também os arquivos de Setup.bat e Cleanup.bat para o computador de serviço.  
  
3. Você deve ter um certificado de servidor com o nome da entidade que contém o nome de domínio totalmente qualificado do computador. Você pode criar um usando a Setup.bat se alterar a `%SERVER_NAME%` variável para o nome totalmente qualificado do computador em que o serviço está hospedado. Observe que o arquivo de Setup.bat deve ser executado em um Prompt de Comando do Desenvolvedor para o Visual Studio aberto com privilégios de administrador.  
  
4. Copie o certificado do servidor no repositório de CurrentUser-TrustedPeople no cliente. Você deve fazer isso somente se o certificado do servidor não for emitido por um emissor confiável.  
  
5. No arquivo EchoServiceHost.cs, altere o valor do nome da entidade do certificado para especificar um nome de computador totalmente qualificado em vez de localhost.  
  
6. Copie os arquivos de programas do cliente da pasta \client\bin\, na pasta específica do idioma, para o computador cliente.  
  
7. No arquivo Client.cs, altere o valor de endereço do ponto de extremidade para corresponder ao novo endereço do serviço.  
  
8. No arquivo Client.cs, altere o nome da entidade do certificado X. 509 para corresponder ao nome do computador totalmente qualificado do host remoto, em vez de localhost.  
  
9. No computador cliente, inicie o Client.exe em uma janela de prompt de comando.  
  
10. Se o cliente e o serviço não puderem se comunicar, consulte [dicas de solução de problemas para exemplos do WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-clean-up-after-the-sample"></a>Para limpar após o exemplo  
  
1. Execute Cleanup.bat na pasta Samples depois de concluir a execução do exemplo.
