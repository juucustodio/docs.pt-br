---
description: 'Saiba mais sobre: WS-AtomicTransaction snap-in do MMC de configuração'
title: Snap-in do MMC de configuração de WS-AtomicTransaction
ms.date: 03/30/2017
ms.assetid: 23592973-1d51-44cc-b887-bf8b0d801e9e
ms.openlocfilehash: 5f1ac32a98b93a3ec3edb9cfa31ae0ebf424aba8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676294"
---
# <a name="ws-atomictransaction-configuration-mmc-snap-in"></a>Snap-in do MMC de configuração do WS-AtomicTransaction

O snap-in do MMC de configuração do WS-AtomicTransaction é usado para configurar uma parte das configurações de WS-AtomicTransaction em máquinas locais e remotas.

## <a name="remarks"></a>Comentários

Se você estiver executando o Windows XP ou o Windows Server 2003, o snap-in do MMC poderá ser encontrado navegando até **painel de controle/ferramentas administrativas/serviços de componentes/**, clicando com o botão direito do mouse em **meu computador** e selecionando **Propriedades**. Esse é o mesmo local em que você pode configurar o MSDTC. As opções disponíveis para configuração são agrupadas na guia **WS-AT** .

 Se você estiver executando o Windows Vista ou o Windows Server 2008, o snap-in do MMC poderá ser encontrado clicando no botão **Iniciar** e digitando na `dcomcnfg.exe` caixa de **pesquisa** . Quando o MMC for aberto, navegue até o nó **minhas Computer\Distributed Transaction COORDINATOR\LOCAL DTC** , clique com o botão direito e selecione **Propriedades**. As opções disponíveis para configuração são agrupadas na guia **WS-AT** .

 As etapas anteriores são usadas para iniciar o snap-in para configurar um computador local. Se você quiser configurar um computador remoto, deverá localizar o nome do computador remoto em painel de **controle/ferramentas administrativas/serviços de componentes/** e executar etapas semelhantes se você estiver executando o Windows XP ou o windows Server 2003. Se você estiver executando o Windows Vista ou o Windows Server 2008, siga as etapas anteriores para o Vista e o Windows Server 2008, mas use o nó **Distributed Transaction COORDINATOR\LOCAL DTC** no nó do computador remoto.

 Para usar a interface do usuário fornecida pela ferramenta, você precisa registrar o arquivo de WsatUI.dll, que está localizado no caminho a seguir,

 **%PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin\WsatUI.dll**

 O registro pode ser feito pelo comando a seguir.

```console
regasm.exe /codebase WsatUI.dll
```

 Você pode usar essa ferramenta para modificar as configurações básicas de WS-AtomicTransaction. Por exemplo, você pode habilitar e desabilitar o suporte do protocolo WS-AtomicTransaction, configurar as portas HTTP para WS-AT, associar um certificado SSL à porta HTTP, configurar certificados especificando os nomes de entidades do certificado, selecionar o modo de rastreamento e definir o padrão e o máximo de tempos limite.

 Se você precisar configurar o suporte a WS-AtomicTransaction somente no computador local, poderá usar a versão de linha de comando dessa ferramenta. Para obter mais informações sobre a ferramenta de linha de comando, consulte o tópico [wsatConfig.exe (utilitário de configuração do WS-AtomicTransaction)](ws-atomictransaction-configuration-utility-wsatconfig-exe.md) .

 Você deve estar ciente de que o snap-in do MMC e a ferramenta de linha de comando não dão suporte à configuração de todas as configurações WS-AT. Essas configurações podem ser editadas apenas modificando o registro diretamente. Para obter mais informações sobre essas configurações do registro, consulte [configuring WS-Atomic Transaction support](./feature-details/configuring-ws-atomic-transaction-support.md).

### <a name="user-interface-description"></a>Descrição da interface do usuário

**Habilitar WS-Atomic suporte à rede de transações**:

 Alternar essa caixa de seleção habilita ou desabilita todos os componentes de GUI deste snap-in.

 Antes de marcar essa caixa, você deve verificar se o acesso ao DTC de rede está habilitado com a comunicação de entrada ou de saída, ou ambos. Esse valor pode ser verificado na guia **segurança** do snap-in do MSDTC.

#### <a name="network-group-box"></a>Caixa de grupo de rede

Você pode especificar a porta HTTPS e as configurações de segurança adicionais, como a criptografia SSL no grupo de rede. Esse grupo será desabilitado (esmaecido) se as transações de rede do DTC não estiverem habilitadas.

 **Porta HTTPS**

 Esse é o valor da porta HTTPS usada para WS-AT. O valor deve ser um número no intervalo de 1-65535 (como para representar uma porta válida). A alteração da porta HTTP modifica a configuração do serviço HTTP, o que significa que o endereço do serviço WS-AT usado anteriormente foi liberado e um novo endereço de serviço WS-AT é registrado com base na nova porta. Além disso, a porta recentemente selecionada é criptografada com o certificado selecionado no momento para criptografia SSL.

> [!NOTE]
> Se você já tiver habilitado o firewall antes de executar essa ferramenta, a porta será automaticamente registrada na lista de exceções. Se o firewall estiver desabilitado antes da execução dessa ferramenta, nada adicional será configurado com relação ao firewall.

 Se você habilitar o firewall depois de configurar o WS-AT, deverá executar essa ferramenta novamente e fornecer o número da porta usando esse parâmetro. Se você desabilitar o firewall após a configuração, o WS-AT continuará funcionando sem entrada adicional.

 **Certificado de ponto de extremidade**

 Clicar no botão **selecionar** exibe uma lista com os certificados disponíveis no momento no computador local, permitindo que o usuário selecione o certificado que pode ser usado para a criptografia SSL. Os certificados devem ter uma chave privada. Caso contrário, você receberá uma mensagem de erro.

> [!NOTE]
> Ao definir um certificado SSL para uma porta selecionada, você substitui o certificado SSL original associado a essa porta, se houver.

 **Contas autorizadas**

 Clicar no botão **selecionar** invoca o editor de lista de controle de acesso do Windows, onde você pode especificar o usuário ou grupo que pode participar de WS-Atomic transações marcando a caixa **permitir** ou **negar** no grupo de permissões **participar** .

 **Certificados autorizados**

 Clicar no botão **selecionar** exibe uma lista de certificados disponíveis no momento na LocalMachine. Em seguida, você pode selecionar quais identidades de certificado têm permissão para participar de WS-Atomic transações.

#### <a name="timeout-group-box"></a>Caixa de grupo de tempo limite

A caixa de grupo **tempo limite** permite que você especifique o tempo limite máximo e padrão para uma transação WS-Atomic. Um valor válido para o tempo limite de saída é entre 1 e 3600. Um valor válido para o tempo limite de entrada é entre 0 e 3600.

#### <a name="tracing-and-logging-group-box"></a>Caixa de grupo de rastreamento e log

A caixa de grupo **rastreamento e registro em log** permite que você configure o rastreamento desejado e o nível de log.

 Clicar no botão **Opções** invoca uma página na qual você pode especificar configurações adicionais.

 A caixa de combinação de **nível de rastreamento** permite que você escolha entre qualquer valor válido da <xref:System.Diagnostics.TraceLevel> enumeração. Você também pode usar as caixas de seleção para especificar se deseja executar o rastreamento de atividade, a propagação de atividade ou coletar informações de identificação pessoal.

 Você também pode especificar sessões de log na caixa Grupo de **sessão de registro em log** .

> [!NOTE]
> Quando outro consumidor de rastreamento estiver usando o provedor de rastreamento WS-AT, você não poderá criar uma nova sessão de log para eventos de rastreamento. Qualquer tentativa de configurar o log durante esse tempo resulta na mensagem de erro "falha ao habilitar o provedor. Código de erro: 1 ".

 Para obter mais informações sobre rastreamento e registro em log, consulte [Administração e diagnóstico](./diagnostics/index.md).

## <a name="see-also"></a>Consulte também

- [Configurando suporte de transações de WS-Atomic](./feature-details/configuring-ws-atomic-transaction-support.md)
- [Utilitário de configuração de transações WS-Atomic (wsatConfig.exe)](ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [Administração e diagnósticos](./diagnostics/index.md)
