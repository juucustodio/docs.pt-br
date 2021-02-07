---
description: 'Saiba mais sobre: como criar uma política de autorização personalizada'
title: 'Como: criar uma política de autorização personalizada'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 05b0549b-882d-4660-b6f0-5678543e5475
ms.openlocfilehash: 41158944aec9b0a5b8cb28c51922b8a1b103317c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743701"
---
# <a name="how-to-create-a-custom-authorization-policy"></a>Como: criar uma política de autorização personalizada

A infraestrutura do modelo de identidade no Windows Communication Foundation (WCF) dá suporte a um modelo de autorização baseado em declaração. As declarações são extraídas de tokens, opcionalmente processadas pela política de autorização personalizada e, em seguida, colocadas em um <xref:System.IdentityModel.Policy.AuthorizationContext> que pode ser examinado para tomar decisões de autorização. Uma política personalizada pode ser usada para transformar declarações de tokens de entrada em declarações esperadas pelo aplicativo. Dessa forma, a camada de aplicativo pode ser isolado dos detalhes sobre as diferentes declarações servidas pelos diferentes tipos de token aos quais o WCF dá suporte. Este tópico mostra como implementar uma política de autorização personalizada e como adicionar essa política à coleção de políticas usadas por um serviço.  
  
### <a name="to-implement-a-custom-authorization-policy"></a>Para implementar uma política de autorização personalizada  
  
1. Defina uma nova classe derivada de <xref:System.IdentityModel.Policy.IAuthorizationPolicy> .  
  
2. Implemente a propriedade somente leitura <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> gerando uma cadeia de caracteres exclusiva no construtor para a classe e retornando essa cadeia de caracteres sempre que a propriedade for acessada.  
  
3. Implemente a propriedade somente leitura <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> retornando um <xref:System.IdentityModel.Claims.ClaimSet> que representa o emissor da política. Isso pode ser um `ClaimSet` que representa o aplicativo ou um interno `ClaimSet` (por exemplo, o `ClaimSet` retornado pela <xref:System.IdentityModel.Claims.ClaimSet.System%2A> propriedade estática.  
  
4. Implemente o <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> método conforme descrito no procedimento a seguir.  
  
### <a name="to-implement-the-evaluate-method"></a>Para implementar o método Evaluate  
  
1. Dois parâmetros são passados para este método: uma instância da <xref:System.IdentityModel.Policy.EvaluationContext> classe e uma referência de objeto.  
  
2. Se a política de autorização personalizada adicionar <xref:System.IdentityModel.Claims.ClaimSet> instâncias sem considerar o conteúdo atual do <xref:System.IdentityModel.Policy.EvaluationContext> , adicione cada uma `ClaimSet` chamando o <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> método e retornar `true` do <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> método. `true`O retorno indica à infraestrutura de autorização que a diretiva de autorização realizou seu trabalho e não precisa ser chamada novamente.  
  
3. Se a política de autorização personalizada Adicionar conjuntos de declarações somente se determinadas declarações já estiverem presentes no `EvaluationContext` , procure essas declarações examinando as `ClaimSet` instâncias retornadas pela <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A> propriedade. Se as declarações estiverem presentes, adicione os novos conjuntos de declarações chamando o <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> método e, se nenhum outro conjunto de declarações for ser adicionado, retorne `true` , indicando à infraestrutura de autorização que a diretiva de autorização concluiu seu trabalho. Se as declarações não estiverem presentes, retorne `false` , indicando que a política de autorização deve ser chamada novamente se outras políticas de autorização adicionarem mais conjuntos de declarações ao `EvaluationContext` .  
  
4. Em cenários de processamento mais complexos, o segundo parâmetro do <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> método é usado para armazenar uma variável de estado que a infraestrutura de autorização passará durante cada chamada subsequente para o <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> método de uma avaliação específica.  
  
### <a name="to-specify-a-custom-authorization-policy-through-configuration"></a>Para especificar uma política de autorização personalizada por meio da configuração  
  
1. Especifique o tipo da política de autorização personalizada no atributo no elemento no elemento `policyType` `add` `authorizationPolicies` no `serviceAuthorization` elemento.  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
        <serviceAuthorization serviceAuthorizationManagerType=  
                  "Samples.MyServiceAuthorizationManager" >  
          <authorizationPolicies>  
            <add policyType="Samples.MyAuthorizationPolicy" />  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
### <a name="to-specify-a-custom-authorization-policy-through-code"></a>Para especificar uma política de autorização personalizada por meio de código  
  
1. Crie um <xref:System.Collections.Generic.List%601> de <xref:System.IdentityModel.Policy.IAuthorizationPolicy> .  
  
2. Crie uma instância da política de autorização personalizada.  
  
3. Adicione a instância da política de autorização à lista.  
  
4. Repita as etapas 2 e 3 para cada política de autorização personalizada.  
  
5. Atribua uma versão somente leitura da lista à <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A> propriedade.  
  
     [!code-csharp[c_CustomAuthPol#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#8)]
     [!code-vb[c_CustomAuthPol#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#8)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma <xref:System.IdentityModel.Policy.IAuthorizationPolicy> implementação completa.  
  
 [!code-csharp[c_CustomAuthPol#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#5)]
 [!code-vb[c_CustomAuthPol#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#5)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [Como: comparar declarações](how-to-compare-claims.md)
- [Como: criar gerenciador de autorização personalizado para um serviço](how-to-create-a-custom-authorization-manager-for-a-service.md)
- [Política de autorização](../samples/authorization-policy.md)
