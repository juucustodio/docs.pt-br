---
description: 'Saiba mais sobre: segurança de acesso ao código e ADO.NET'
title: Segurança de Acesso do Código
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
ms.openlocfilehash: e7a6054cd7c222c700f5a83e46f5b44bfee23248
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663996"
---
# <a name="code-access-security-and-adonet"></a>Segurança de acesso do código e o ADO.NET

O .NET Framework oferece segurança baseada em função e segurança de acesso de código (CAS), ambas são implementadas por meio de uma infraestrutura comum fornecida pelo CLR (Common Language Runtime). No mundo do código não gerenciado, a maioria dos aplicativos é executada com as permissões do usuário ou da entidade de segurança. Como resultado, é possível que os sistemas de computador sejam danificados e os dados particulares sejam comprometidos quando um software mal-intencionado ou com erro for executado por um usuário com privilégios elevados.  
  
 Por sua vez, o código gerenciado em execução no .NET Framework inclui a segurança de acesso de código, que se aplica apenas ao código. O fato de o código ter a execução permitida ou não depende da origem do código ou de outros aspectos da identidade do código, não apenas da identidade da entidade de segurança. Isso reduz a probabilidade de que o código gerenciado seja mal-utilizado.  
  
## <a name="code-access-permissions"></a>Permissões de acesso de código  

 Quando o código é executado, ele apresenta evidências que são avaliadas pelo sistema de segurança CLR. Normalmente, essas evidências englobam a origem de código, incluindo a URL, o site e a zona, e as assinaturas digitais que garantem a identidade do assembly.  
  
 O CLR permite que o código realize apenas as operações que ele tem permissão para executar. O código pode solicitar permissões, e essas solicitações são respeitadas com base na política de segurança definida por um administrador.  
  
> [!NOTE]
> O código executado no CLR não pode conceder permissões a ele mesmo. Por exemplo, o código pode solicitar e receber menos permissões do que uma política de segurança permite, mas nunca receberá mais permissões. Ao conceder as permissões, comece com nenhuma permissão e depois adicione as permissões mais restritas para a tarefa específica que está sendo executada. Começar com todas as permissões e depois negar permissões individuais resulta em aplicativos inseguros que podem conter brechas de segurança não intencionais para a concessão de mais permissões do que as necessárias. Para obter mais informações, consulte [Configurando política de segurança](/previous-versions/dotnet/netframework-4.0/7c9c2y1w(v=vs.100)) e [Gerenciamento de política de segurança](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)).  
  
 Existem três tipos de permissões de acesso de código:  
  
- As `Code access permissions` são derivadas da classe <xref:System.Security.CodeAccessPermission>. São necessárias permissões para acessar recursos protegidos, como arquivos e variáveis de ambiente, e executar operações protegidas, como acessar código não gerenciado.  
  
- As `Identity permissions` representam características que identificam um assembly. As permissões são concedidas a um assembly com base em evidências, o que pode incluir itens como uma assinatura digital ou a origem do código. As permissões de identidade também são derivadas da classe base <xref:System.Security.CodeAccessPermission>.  
  
- As `Role-based security permissions` são baseadas no fato de uma entidade de segurança ter uma identidade especificada ou ser membro de uma função especificada. A classe <xref:System.Security.Permissions.PrincipalPermission> permite verificações de permissões declarativas e imperativas na entidade de segurança ativa.  
  
 Para determinar se o código está autorizado a acessar um recurso ou executar uma operação, o sistema de segurança do runtime atravessa a pilha de chamadas, comparando as permissões concedidas de cada chamador com a permissão que está sendo exigida. Se algum chamador na pilha de chamadas não tiver a permissão exigida, uma <xref:System.Security.SecurityException> será gerada e o acesso será recusado.  
  
### <a name="requesting-permissions"></a>Solicitando permissões  

 A finalidade de solicitar permissões é informar ao runtime quais permissões seu aplicativo requer para ser executado, e garantir que ele receberá apenas as permissões de que realmente precisa. Por exemplo, se seu aplicativo precisa gravar dados no disco local, ele requer a <xref:System.Security.Permissions.FileIOPermission>. Se essa permissão não for concedida, o aplicativo falhará quando tentar gravar no disco. Entretanto, se o aplicativo solicitar a `FileIOPermission` e essa permissão não for concedida, ele gerará a exceção no início e não será carregado.  
  
 Em um cenário onde o aplicativo precisa apenas ler dados do disco, você pode solicitar que ele nunca receba permissões de gravação. No caso de um bug ou um ataque mal-intencionado, seu código não pode danificar os dados em que opera. Para obter mais informações, consulte [solicitando permissões](/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100)).  
  
## <a name="role-based-security-and-cas"></a>Segurança baseada em função e CAS  

 Implementar a segurança baseada em função e a segurança de acesso de código (CAS) melhora a segurança geral de seu aplicativo. A segurança baseada em função pode ser baseada em uma conta do Windows ou uma identidade personalizada, tornando as informações sobre a entidade de segurança disponíveis ao thread atual. Além disso, os aplicativos são geralmente necessários para fornecer acesso a dados ou recursos com base nas credenciais fornecidas pelo usuário. Em geral, esses aplicativos verificam a função de um usuário e fornecem acesso aos recursos com base nas funções.  
  
 A segurança baseada em função permite que um componente identifique os usuários atuais e suas funções associadas em tempo de execução. Essas informações são então mapeadas por meio de uma política de CAS para determinar o conjunto de permissões concedidas em tempo de execução. Para um domínio de aplicativo especificado, o host pode alterar a política de segurança baseada em função padrão e definir uma entidade de segurança padrão que represente um usuário e as funções associadas a esse usuário.  
  
 O CLR usa permissões para implementar seu mecanismo de imposição de restrições em código gerenciado. As permissões de segurança baseada em função fornecem um mecanismo para descobrir se um usuário (ou o agente que atua em nome do usuário) tem uma identidade em particular ou é membro de uma função especificada. Para obter mais informações, consulte [permissões de segurança](/previous-versions/dotnet/netframework-4.0/5ba4k1c5(v=vs.100)).  
  
 Dependendo do tipo de aplicativo que você está criando, você também deve considerar implementar as permissões baseadas em função no banco de dados. Para obter mais informações sobre a segurança baseada em funções no SQL Server, consulte [segurança do SQL Server](./sql/sql-server-security.md).  
  
## <a name="assemblies"></a>Assemblies  

 Os assemblies formam a unidade fundamental de implantação, controle de versão, reutilização, escopo de ativação e permissões de segurança para um aplicativo .NET Framework. Um assembly fornece uma coleção de tipos e recursos que são criados para trabalhar em conjunto e formar uma unidade lógica de funcionalidade. Para o CLR, um tipo não existe fora do contexto de um assembly. Para obter mais informações sobre como criar e implantar assemblies, consulte [programação com assemblies](../../../standard/assembly/index.md).  
  
### <a name="strong-naming-assemblies"></a>Assemblies de nomes fortes  

 Um nome forte, ou assinatura digital, consiste na identidade do assembly, que inclui seu nome de texto simples, número de versão e informações de cultura (se fornecidas), além de uma chave pública e uma assinatura digital. A assinatura digital é gerada a partir de um arquivo de assembly usando a chave privada correspondente. O arquivo do assembly inclui o manifesto do assembly, o qual contém os nomes e os hashes de todos os arquivos que compõem o assembly.  
  
 Um assembly de nome forte oferece a um aplicativo ou componente uma identidade exclusiva que outro software pode usar para se referir a ele explicitamente. O nome forte impede que os assemblies sejam enganados por um assembly que contém código hostil. O nome forte também garante a consistência entre versões diferentes de um componente. Você deve dar nomes fortes aos assemblies que serão implantados no GAC (cache de assembly global). Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](../../../standard/assembly/create-use-strong-named.md).  
  
## <a name="partial-trust-in-adonet-20"></a>Confiança parcial no ADO.NET 2.0  

 No ADO.NET 2.0, o Provedor de Dados .NET Framework para SQL Server, o Provedor de Dados .NET Framework para OLE DB, o Provedor de Dados .NET Framework para ODBC e o Provedor de Dados .NET Framework para Oracle podem agora ser todos executados em ambientes parcialmente confiáveis. Em versões anteriores do .NET Framework, somente <xref:System.Data.SqlClient> tinha suporte em aplicativos com confiança parcial.  
  
 Pelo menos um aplicativo parcialmente confiável que usa o provedor SQL Server deve ter permissões de execução e <xref:System.Data.SqlClient.SqlClientPermission>.  
  
### <a name="permission-attribute-properties-for-partial-trust"></a>Propriedades de atributo de permissão para confiança parcial  

 Para os cenários de confiança parcial, você pode usar membros <xref:System.Data.SqlClient.SqlClientPermissionAttribute> para restringir ainda mais os recursos disponíveis para o Provedor de Dados .NET Framework para SQL Server.  
  
 A tabela a seguir lista as propriedades <xref:System.Data.SqlClient.SqlClientPermissionAttribute> disponíveis e suas descrições:  
  
|Propriedade de atributo de permissão|Descrição|  
|-----------------------------------|-----------------|  
|`Action`|Obtém ou define uma ação de segurança. Herdado de <xref:System.Security.Permissions.SecurityAttribute>.|  
|`AllowBlankPassword`|Habilita ou desabilita o uso de uma senha em branco em uma cadeia de conexão. Os valores válidos são `true` (para habilitar o uso de senhas em branco) e `false` (para desabilitar o uso de senhas em branco). Herdado de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`ConnectionString`|Identifica uma cadeia de conexão permitida. Várias cadeias de conexão podem ser identificadas. **Observação:**  Não inclua uma ID de usuário ou senha em sua cadeia de conexão. Nesta versão, você não pode modificar restrições de cadeia de conexão usando a Ferramenta de Configuração do .NET Framework. <br /><br /> Herdado de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictions`|Identifica os parâmetros de cadeia de conexão que são permitidos ou não. Os parâmetros da cadeia de conexão são identificados no formulário *\<parameter name>=* . Vários parâmetros podem ser especificados, sendo delimitados por um ponto e vírgula (;). **Observação:**  Se você não especificar `KeyRestrictions` , mas definir `KeyRestrictionBehavior` a propriedade como `AllowOnly` ou `PreventUsage` , nenhum parâmetro de cadeia de conexão adicional será permitido. Herdado de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictionBehavior`|Identifica os parâmetros de cadeia de conexão como os únicos parâmetros adicionais permitidos (`AllowOnly`), ou identifica os parâmetros adicionais que não são permitidos (`PreventUsage`). `AllowOnly` é o padrão. Herdado de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`TypeID`|Obtém um identificador exclusivo para este atributo quando implementado em uma classe derivada. Herdado de <xref:System.Attribute>.|  
|`Unrestricted`|Indica se a permissão irrestrita ao recurso é declarada. Herdado de <xref:System.Security.Permissions.SecurityAttribute>.|  
  
#### <a name="connectionstring-syntax"></a>Sintaxe de ConnectionString  

 O exemplo a seguir demonstra como usar o elemento `connectionStrings` de um arquivo de configuração para permitir que somente uma cadeia de conexão específica seja usada. Consulte [cadeias de conexão](connection-strings.md) para obter mais informações sobre como armazenar e recuperar cadeias de conexão de arquivos de configuração.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictions-syntax"></a>Sintaxe de KeyRestrictions  

 O exemplo a seguir habilita a mesma cadeia de conexão, habilita o uso `Encrypt` das `Packet Size` Opções de cadeia de conexão e, mas restringe o uso de qualquer outra opção de cadeia de conexão.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-preventusage-syntax"></a>Sintaxe de KeyRestrictionBehavior com PreventUsage  

 O exemplo a seguir permite a mesma cadeia de conexão e todos os outros parâmetros de conexão, com exceção de `User Id`, `Password` e `Persist Security Info`.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-allowonly-syntax"></a>Sintaxe de KeyRestrictionBehavior com AllowOnly  

 O exemplo a seguir permite duas cadeias de conexão que também contêm os parâmetros `Initial Catalog`, `Connection Timeout`, `Encrypt` e `Packet Size`. Todos os outros parâmetros de cadeia de conexão são restritos.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"
    connectionString="Data Source=SqlServer2;Initial
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### <a name="enabling-partial-trust-with-a-custom-permission-set"></a>Habilitando a confiança parcial com um conjunto de permissões personalizado  

 Para habilitar o uso de permissões <xref:System.Data.SqlClient> para uma zona específica, um administrador de sistema deve criar um conjunto de permissões personalizado e configurá-lo como o conjunto de permissões para uma zona específica. Os conjuntos de permissões padrão, como `LocalIntranet`, não podem ser modificados. Por exemplo, para incluir <xref:System.Data.SqlClient> permissões para o código que tem um <xref:System.Security.Policy.Zone> do `LocalIntranet` , um administrador do sistema pode copiar o conjunto de permissões para `LocalIntranet` , renomeá-lo como "CustomLocalIntranet", adicionar as <xref:System.Data.SqlClient> permissões, importar o conjunto de permissões CustomLocalIntranet usando o [Caspol.exe (ferramenta de política de segurança de acesso do código)](../../tools/caspol-exe-code-access-security-policy-tool.md)e definir o conjunto de permissões de `LocalIntranet_Zone` como CustomLocalIntranet.  
  
### <a name="sample-permission-set"></a>Conjunto de permissões de exemplo  

 A seguir está um conjunto de permissões de exemplo para o Provedor de Dados .NET Framework para SQL Server em um cenário parcialmente confiável. Para obter informações sobre como criar conjuntos de permissões personalizados, consulte [Configurando conjuntos de permissões usando Caspol.exe](/previous-versions/dotnet/netframework-4.0/4ybs46y6(v=vs.100)).  
  
```xml  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## <a name="verifying-adonet-code-access-using-security-permissions"></a>Verificando o acesso de código ADO.NET usando permissões de segurança  

 Para cenários de confiança parcial, você pode exigir privilégios CAS para determinados métodos em seu código especificando um <xref:System.Data.SqlClient.SqlClientPermissionAttribute>. Se o privilégio não for permitido pela política de segurança restrita em vigor, uma exceção será gerada antes que seu código seja executado. Para obter mais informações sobre a política de segurança, consulte [Gerenciamento de políticas de segurança](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)) e [práticas recomendadas de política](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))de segurança.  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir demonstra como escrever um código que requer um cadeia de conexão específica. Ele simula a negação de permissões irrestritas a <xref:System.Data.SqlClient>, que um administrador de sistema implementaria usando uma política CAS no mundo real.  
  
> [!IMPORTANT]
> Ao criar permissões CAS para ADO.NET, o padrão correto é começar com o caso mais restritivo (nenhuma permissão) e depois adicionar as permissões específicas que são necessárias para a tarefa em particular que o código precisa executar. O padrão oposto, começando com todas as permissões e, em seguida, negar uma permissão específica, não é seguro porque há várias maneiras de expressar a mesma cadeia de conexão. Por exemplo, se você iniciar com todas as permissões e depois tentar negar o uso da cadeia de conexão “server=someserver”, a cadeia de caracteres “server=someserver.mycompany.com” ainda será permitida. Ao iniciar sempre sem conceder absolutamente nenhuma permissão, você reduz as chances de haver brechas no conjunto de permissões.  
  
 O código a seguir demonstra como `SqlClient` realiza a exigência de segurança, que gera uma <xref:System.Security.SecurityException> caso as permissões CAS apropriadas não estejam estabelecidas. A saída <xref:System.Security.SecurityException> é exibida na janela do console.  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 Você deverá ver esta saída na janela do console:  
  
```output  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## <a name="interoperability-with-unmanaged-code"></a>Interoperabilidade com código não gerenciado  

 O código executado fora do CLR é chamado de código não gerenciado. Portanto, mecanismos de segurança, como o CAS, não podem ser aplicados a código não gerenciado. Componentes COM, interfaces ActiveX e funções da API do Windows são exemplos de código não gerenciado. Aplicam-se considerações de segurança especiais ao executar o código não gerenciado, para que você não coloque em risco a segurança geral do aplicativo. Para obter mais informações, consulte [interoperação com código não gerenciado](../../interop/index.md).  
  
 O .NET Framework também oferece suporte à compatibilidade com versões anteriores a componentes COM existentes fornecendo acesso por meio da interoperabilidade COM. Você pode incorporar componentes COM em um aplicativo .NET Framework usando ferramentas de interoperabilidade COM para importar os tipos COM relevantes. Uma vez importados, os tipos COM estão prontos para uso. A interoperabilidade COM também permite que clientes COM acessem o código gerenciado exportando metadados do assembly para uma biblioteca de tipos e registrando o componente gerenciado como um componente COM. Para obter mais informações, consulte [interoperabilidade com avançada](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100)).  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](securing-ado-net-applications.md)
- [Segurança no código nativo e do .NET Framework](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))
- [Segurança baseada em função](../../../standard/security/role-based-security.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
