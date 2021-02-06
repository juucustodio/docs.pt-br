---
description: 'Saiba mais sobre: como bloquear pontos de extremidade na empresa'
title: 'Como: bloquear pontos de extremidade na empresa'
ms.date: 03/30/2017
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
ms.openlocfilehash: 8e54c3d1cadcfdb6f0102281813eb3758320a143
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644223"
---
# <a name="how-to-lock-down-endpoints-in-the-enterprise"></a>Como: bloquear pontos de extremidade na empresa

Grandes empresas geralmente exigem que os aplicativos sejam desenvolvidos em conformidade com as políticas de segurança corporativa. O tópico a seguir discute como desenvolver e instalar um validador de ponto de extremidade do cliente que pode ser usado para validar todos os aplicativos cliente do Windows Communication Foundation (WCF) instalados nos computadores.

Nesse caso, o validador é um validador de cliente, pois esse comportamento de ponto de extremidade é adicionado à [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) seção cliente no arquivo machine.config. O WCF carrega comportamentos comuns de ponto de extremidade apenas para aplicativos cliente e carrega comportamentos de serviço comuns somente para aplicativos de serviço. Para instalar esse mesmo validador para aplicativos de serviço, o validador deve ser um comportamento de serviço. Para obter mais informações, consulte a [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) seção.

> [!IMPORTANT]
> Os comportamentos de serviço ou ponto de extremidade não marcados com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) que são adicionados à [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) seção de um arquivo de configuração não são executados quando o aplicativo é executado em um ambiente de confiança parcial e nenhuma exceção é lançada quando isso ocorre. Para impor a execução de comportamentos comuns, como validadores, você deve:
>
> - Marque seu comportamento comum com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo para que ele possa ser executado quando implantado como um aplicativo de confiança parcial. Observe que uma entrada de registro pode ser definida no computador para impedir que assemblies marcados com APTCA sejam executados.
>
> - Certifique-se de que, se o aplicativo for implantado como um aplicativo totalmente confiável, que os usuários não possam modificar as configurações de segurança de acesso ao código para executar o aplicativo em um ambiente de confiança parcial. Se puderem fazer isso, o validador personalizado não é executado e nenhuma exceção é gerada. Para obter uma maneira de garantir isso, consulte a `levelfinal` opção usando a [ferramenta de política de segurança de acesso ao código (Caspol.exe)](../../tools/caspol-exe-code-access-security-policy-tool.md).
>
> Para obter mais informações, consulte [práticas recomendadas de confiança parcial](../feature-details/partial-trust-best-practices.md) e [cenários de implantação com suporte](../feature-details/supported-deployment-scenarios.md).

### <a name="to-create-the-endpoint-validator"></a>Para criar o validador de ponto de extremidade

1. Crie um <xref:System.ServiceModel.Description.IEndpointBehavior> com as etapas de validação desejadas no <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A> método. O código a seguir fornece um exemplo. (O `InternetClientValidatorBehavior` é tirado do exemplo de [validação de segurança](../samples/security-validation.md) .)

    [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]

2. Crie <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> um novo que registre o validador de ponto de extremidade criado na etapa 1. O exemplo de código a seguir mostra isso. (O código original para este exemplo está no exemplo de [validação de segurança](../samples/security-validation.md) .)

    [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]

3. Verifique se o assembly compilado está assinado com um nome forte. Para obter detalhes, consulte a [ferramenta de nome forte (SN.EXE)](../../tools/sn-exe-strong-name-tool.md) e os comandos do compilador para seu idioma.

### <a name="to-install-the-validator-into-the-target-computer"></a>Para instalar o validador no computador de destino

1. Instale o validador de ponto de extremidade usando o mecanismo apropriado. Em uma empresa, isso pode ser usando Política de Grupo e o SMS (Systems Management Server).

2. Instale o assembly de nome forte no cache de assembly global usando o [Gacutil.exe (ferramenta de cache de assembly global)](../../tools/gacutil-exe-gac-tool.md).

3. Use os <xref:System.Configuration?displayProperty=nameWithType> tipos de namespace para:

    1. Adicione a extensão à [\<behaviorExtensions>](../../configure-apps/file-schema/wcf/behaviorextensions.md) seção usando um nome de tipo totalmente qualificado e bloqueie o elemento.

         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]

    2. Adicione o elemento Behavior à `EndpointBehaviors` propriedade da [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) seção e bloqueie o elemento. (Para instalar o validador no serviço, o validador deve ser um <xref:System.ServiceModel.Description.IServiceBehavior> e adicionado à `ServiceBehaviors` propriedade.) O exemplo de código a seguir mostra a configuração apropriada após as etapas a. e b., com a única exceção de que não há um nome forte.

        [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]

    3. Salve o arquivo machine.config. O exemplo de código a seguir executa todas as tarefas na etapa 3, mas salva uma cópia do arquivo de machine.config modificado localmente.

        [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]

## <a name="example"></a>Exemplo

O exemplo de código a seguir mostra como adicionar um comportamento comum ao arquivo de machine.config e salvar uma cópia no disco. O `InternetClientValidatorBehavior` é tirado do exemplo de [validação de segurança](../samples/security-validation.md) .

[!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]

## <a name="net-framework-security"></a>Segurança do .NET Framework

Você também pode querer criptografar os elementos do arquivo de configuração. Para obter mais informações, consulte a seção Consulte também.

## <a name="see-also"></a>Consulte também

- [Criptografando elementos do arquivo de configuração usando DPAPI](/previous-versions/msp-n-p/ff647398(v=pandp.10))
- [Criptografando elementos do arquivo de configuração usando RSA](/previous-versions/msp-n-p/ff650304(v=pandp.10))
