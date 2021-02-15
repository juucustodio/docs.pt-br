---
description: 'Saiba mais sobre: usando o Instrumentação de Gerenciamento do Windows para diagnóstico'
title: Usando Windows Management Instrumentation para diagnóstico
ms.date: 03/30/2017
ms.assetid: fe48738d-e31b-454d-b5ec-24c85c6bf79a
ms.openlocfilehash: 508422e8e060e608032d7ed22c5736c56c838f10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99653869"
---
# <a name="using-windows-management-instrumentation-for-diagnostics"></a>Usando Windows Management Instrumentation para diagnóstico

Windows Communication Foundation (WCF) expõe os dados de inspeção de um serviço em tempo de execução por meio de um provedor de Instrumentação de Gerenciamento do Windows do WCF (WMI).  
  
## <a name="enabling-wmi"></a>Habilitando o WMI  

 O WMI é a implementação da Microsoft do padrão Web-Based Enterprise Management (WBEM). Para obter mais informações sobre o SDK do WMI, consulte [Instrumentação de gerenciamento do Windows](/windows/desktop/WmiSdk/wmi-start-page). O WBEM é um padrão do setor para a forma como os aplicativos expõem a instrumentação de gerenciamento para ferramentas de gerenciamento externas.  
  
 Um provedor WMI é um componente que expõe a instrumentação em tempo de execução por meio de uma interface compatível com o WBEM. Ele consiste em um conjunto de objetos WMI que têm pares de atributo/valor. Os pares podem ser de vários tipos simples. As ferramentas de gerenciamento podem se conectar aos serviços por meio da interface em tempo de execução. O WCF expõe atributos de serviços como endereços, associações, comportamentos e ouvintes.  
  
 O provedor WMI interno pode ser ativado no arquivo de configuração do aplicativo. Isso é feito por meio do `wmiProviderEnabled` atributo do [\<diagnostics>](../../../configure-apps/file-schema/wcf/diagnostics.md) na [\<system.serviceModel>](../../../configure-apps/file-schema/wcf/system-servicemodel.md) seção, conforme mostrado na seguinte configuração de exemplo.  
  
```xml  
<system.serviceModel>  
    …  
    <diagnostics wmiProviderEnabled="true" />  
    …  
</system.serviceModel>  
```  
  
 Essa entrada de configuração expõe uma interface WMI. Os aplicativos de gerenciamento agora podem se conectar por meio dessa interface e acessar a instrumentação de gerenciamento do aplicativo.  
  
## <a name="accessing-wmi-data"></a>Acessando dados do WMI  

 Os dados do WMI podem ser acessados de várias maneiras diferentes. A Microsoft fornece APIs WMI para scripts, Visual Basic aplicativos, aplicativos C++ e o .NET Framework. Para obter mais informações, consulte [usando o WMI](/windows/win32/wmisdk/using-wmi).  
  
> [!CAUTION]
> Se você usar os métodos .NET Framework fornecidos para acessar os dados do WMI programaticamente, você deve estar ciente de que esses métodos podem gerar exceções quando a conexão é estabelecida. A conexão não é estabelecida durante a construção da <xref:System.Management.ManagementObject> instância, mas na primeira solicitação que envolve a troca de dados real. Portanto, você deve usar um `try..catch` bloco para capturar as possíveis exceções.  
  
 Você pode alterar o rastreamento e o nível de log de mensagens, bem como as opções de log de mensagens para a `System.ServiceModel` origem do rastreamento no WMI. Isso pode ser feito acessando a instância [AppDomainInfo](appdomaininfo.md) , que expõe essas propriedades booleanas: `LogMessagesAtServiceLevel` ,, `LogMessagesAtTransportLevel` `LogMalformedMessages` e `TraceLevel` . Portanto, se você configurar um ouvinte de rastreamento para o log de mensagens, mas definir essas opções como `false` em configuração, você poderá alterá-las posteriormente para `true` quando o aplicativo estiver em execução. Isso habilitará efetivamente o registro em log de mensagens em tempo de execução. Da mesma forma, se você habilitar o log de mensagens em seu arquivo de configuração, poderá desabilitá-lo em tempo de execução usando o WMI.  
  
 Você deve estar ciente de que, se nenhum ouvinte de rastreamento de log de mensagens do log de mensagens ou nenhum `System.ServiceModel` ouvinte de rastreamento para rastreamento for especificado no arquivo de configuração, nenhuma das alterações será levada em vigor, mesmo que as alterações sejam aceitas pelo WMI. Para obter mais informações sobre como configurar corretamente os respectivos ouvintes, consulte [Configurando o log de mensagens](../configuring-message-logging.md) e [Configurando o rastreamento](../tracing/configuring-tracing.md). O nível de rastreamento de todas as outras origens de rastreamento especificadas pela configuração é efetivo quando o aplicativo é iniciado e não pode ser alterado.  
  
 O WCF expõe um `GetOperationCounterInstanceName` método para scripts. Esse método retornará um nome de instância do contador de desempenho se você fornecê-lo com um nome de operação. No entanto, ele não valida sua entrada. Portanto, se você fornecer um nome de operação incorreto, um nome de contador incorreto será retornado.  
  
 A `OutgoingChannel` propriedade da `Service` instância não conta canais abertos por um serviço para se conectar a outro serviço, se o cliente WCF para o serviço de destino não for criado dentro do `Service` método.  
  
 **Cuidado** O WMI só dá suporte a um <xref:System.TimeSpan> valor de até 3 pontos decimais. Por exemplo, se o serviço definir uma de suas propriedades como <xref:System.TimeSpan.MaxValue> , seu valor será truncado após 3 pontos decimais quando exibido por meio do WMI.  
  
## <a name="security"></a>Segurança  

 Como o provedor WMI WCF permite a descoberta de serviços em um ambiente, você deve ter muito cuidado para conceder acesso a ele. Se você relaxar o acesso padrão somente ao administrador, poderá permitir que partes menos confiáveis acessem dados confidenciais em seu ambiente. Especificamente, se você afrouxar permissões no acesso WMI remoto, poderão ocorrer ataques de inundação. Se um processo for inundado por solicitações excessivas do WMI, seu desempenho poderá ser degradado.  
  
 Além disso, se você relaxar as permissões de acesso para o arquivo MOF, partes menos confiáveis poderão manipular o comportamento do WMI e alterar os objetos que são carregados no esquema WMI. Por exemplo, os campos podem ser removidos de modo que os dados críticos sejam ocultados do administrador ou que os campos que não populem ou façam com que exceções sejam adicionadas ao arquivo.  
  
 Por padrão, o provedor WCF WMI concede a permissão "executar método", "gravação do provedor" e "Habilitar conta" para o administrador e a permissão "Habilitar conta" para ASP.NET, serviço local e serviço de rede. Em particular, em plataformas que não são do Windows Vista, a conta ASP.NET tem acesso de leitura ao namespace ServiceModel WMI. Se você não quiser conceder esses privilégios a um grupo de usuários específico, desative o provedor WMI (ele está desabilitado por padrão) ou desabilite o acesso para o grupo de usuários específico.  
  
 Além disso, quando você tenta habilitar o WMI por meio da configuração, o WMI pode não ser habilitado devido a um privilégio de usuário insuficiente. No entanto, nenhum evento é gravado no log de eventos para registrar essa falha.  
  
 Para modificar os níveis de privilégio do usuário, use as etapas a seguir.  
  
1. Clique em Iniciar e em executar e digite **compmgmt. msc**.  
  
2. Clique com o botão direito do mouse em **serviços e aplicativos/controles WMI** para selecionar **Propriedades**.  
  
3. Selecione a guia **segurança** e navegue até o namespace **raiz/ServiceModel** . Clique no botão **segurança** .  
  
4. Selecione o grupo ou usuário específico para o qual você deseja controlar o acesso e use a caixa de seleção **permitir** ou **negar** para configurar permissões.  
  
## <a name="granting-wcf-wmi-registration-permissions-to-additional-users"></a>Concedendo permissões de registro do WCF WMI a usuários adicionais  

 O WCF expõe dados de gerenciamento para o WMI. Ele faz isso hospedando um provedor WMI em processo, às vezes chamado de "provedor desacoplado". Para que os dados de gerenciamento sejam expostos, a conta que registra esse provedor deve ter as permissões apropriadas. No Windows, apenas um pequeno conjunto de contas com privilégios pode registrar provedores dissociados por padrão. Isso é um problema porque os usuários normalmente desejam expor dados WMI de um serviço WCF em execução em uma conta que não está no conjunto padrão.  
  
 Para fornecer esse acesso, um administrador deve conceder as seguintes permissões para a conta adicional na seguinte ordem:  
  
1. Permissão para acessar o namespace WCF WMI.  
  
2. Permissão para registrar o provedor WMI dissociado do WCF.  
  
#### <a name="to-grant-wmi-namespace-access-permission"></a>Para conceder permissão de acesso do namespace WMI  
  
1. Execute o script do PowerShell a seguir.  
  
    ```powershell  
    write-host ""  
    write-host "Granting Access to root/servicemodel WMI namespace to built in users group"  
    write-host ""  
  
    # Create the binary representation of the permissions to grant in SDDL  
    $newPermissions = "O:BAG:BAD:P(A;CI;CCDCLCSWRPWPRCWD;;;BA)(A;CI;CC;;;NS)(A;CI;CC;;;LS)(A;CI;CC;;;BU)"  
    $converter = new-object system.management.ManagementClass Win32_SecurityDescriptorHelper  
    $binarySD = $converter.SDDLToBinarySD($newPermissions)  
    $convertedPermissions = ,$binarySD.BinarySD  
  
    # Get the object used to set the permissions  
    $security = gwmi -namespace root/servicemodel -class __SystemSecurity  
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "Previous ACL: "$outsddl.SDDL  
  
    # Change the Access Control List (ACL) using SDDL  
    $result = $security.PsBase.InvokeMethod("SetSD",$convertedPermissions)
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "New ACL:      "$outsddl.SDDL  
    write-host ""  
    ```  
  
     Esse script do PowerShell usa o SDDL (Security Descriptor Definition Language) para conceder ao grupo de Built-In usuários acesso ao namespace WMI "root/ServiceModel". Ele especifica as seguintes ACLs:  
  
    - Built-In administrador (BA)-já tinha acesso.  
  
    - Serviço de rede (NS)-já tinha acesso.  
  
    - Sistema local (LS)-já tinha acesso.  
  
    - Built-In usuários-o grupo ao qual conceder acesso.  
  
#### <a name="to-grant-provider-registration-access"></a>Para conceder acesso ao registro do provedor  
  
1. Execute o script do PowerShell a seguir.  
  
    ```powershell  
    write-host ""  
    write-host "Granting WCF provider registration access to built in users group"  
    write-host ""  
    # Set security on ServiceModel provider  
    $provider = get-WmiObject -namespace "root\servicemodel" __Win32Provider  
  
    write-host "Previous ACL: "$provider.SecurityDescriptor  
    $result = $provider.SecurityDescriptor = "O:BUG:BUD:(A;;0x1;;;BA)(A;;0x1;;;NS)(A;;0x1;;;LS)(A;;0x1;;;BU)"  
  
    # Commit the changes and display it to the console  
    $result = $provider.Put()  
    write-host "New ACL:      "$provider.SecurityDescriptor  
    write-host ""  
    ```  
  
### <a name="granting-access-to-arbitrary-users-or-groups"></a>Concedendo acesso a usuários ou grupos arbitrários  

 O exemplo nesta seção concede privilégios de registro do provedor WMI a todos os usuários locais. Se você quiser conceder acesso a um usuário ou grupo que não esteja interno, deverá obter o SID (identificador de segurança) do usuário ou do grupo. Não há uma maneira simples de obter o SID para um usuário arbitrário. Um método é fazer logon como o usuário desejado e, em seguida, emitir o comando do Shell a seguir.  
  
```console
Whoami /user  
```  
  
 Isso fornece o SID do usuário atual, mas esse método não pode ser usado para obter o SID em qualquer usuário arbitrário. Outro método para obter o SID é usar a ferramenta [getsid.exe](/windows/win32/wmisdk/using-wmi) das ferramentas do Windows 2000 Resource Kit para tarefas administrativas. Essa ferramenta compara o SID de dois usuários (local ou domínio) e, como um efeito colateral, imprime os dois SIDs na linha de comando. Para obter mais informações, consulte [SIDs bem conhecidos](https://support.microsoft.com/help/243330/well-known-security-identifiers-in-windows-operating-systems).  
  
## <a name="accessing-remote-wmi-object-instances"></a>Acessando instâncias de objeto WMI remoto  

 Se você precisar acessar as instâncias WMI do WCF em um computador remoto, deverá habilitar a privacidade do pacote nas ferramentas que você usa para acesso. A seção a seguir descreve como fazer isso usando o WMI CIM Studio, o Instrumentação de Gerenciamento do Windows Tester, bem como o SDK do .NET 2,0.  
  
### <a name="wmi-cim-studio"></a>WMI CIM Studio

Se você tiver instalado as ferramentas administrativas do WMI, poderá usar o WMI CIM Studio para acessar as instâncias do WMI. As ferramentas estão na seguinte pasta:
  
*Ferramentas do%windir%\Program Files\WMI\\*
  
1. Na janela **conectar ao namespace:** , digite **root\ServiceModel** e clique em **OK.**  
  
2. Na janela de **logon do WMI CIM Studio** , clique no botão **Opções >>** para expandir a janela. Selecione **privacidade de pacote** para **nível de autenticação** e clique em **OK**.  
  
### <a name="windows-management-instrumentation-tester"></a>Instrumentação de Gerenciamento do Windows testador  

 Essa ferramenta é instalada pelo Windows. Para executá-lo, inicie um console de comando digitando **cmd.exe** na caixa de diálogo **Iniciar/Executar** e clique em **OK**. Em seguida, digite **wbemtest.exe** na janela de comando. Em seguida, a ferramenta de testador Instrumentação de Gerenciamento do Windows é iniciada.  
  
1. Clique no botão **conectar** no canto superior direito da janela.  
  
2. Na nova janela, insira **root\ServiceModel** para o campo **namespace** e selecione privacidade de **pacote** para o **nível de autenticação**. Clique em **Conectar**.  
  
### <a name="using-managed-code"></a>Usando código gerenciado  

 Você também pode acessar instâncias WMI remotas programaticamente usando classes fornecidas pelo <xref:System.Management> namespace. O exemplo de código a seguir demonstra como fazer isso.  
  
```csharp
String wcfNamespace = $@"\\{this.serviceMachineName}\Root\ServiceModel");
  
ConnectionOptions connection = new ConnectionOptions();  
connection.Authentication = AuthenticationLevel.PacketPrivacy;  
ManagementScope scope = new ManagementScope(this.wcfNamespace, connection);  
```
