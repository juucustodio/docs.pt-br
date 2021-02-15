---
description: 'Saiba mais sobre: suporte ao identificador de recurso internacional em System. URI'
title: Suporte ao International Resource Identifier em System.Uri
ms.date: 03/30/2017
ms.assetid: b5e994c3-3535-4aff-8e1b-b69be22e9a22
ms.openlocfilehash: 9aa22a42f45d149b56441e113e3e6cc00512c506
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801872"
---
# <a name="international-resource-identifier-support-in-systemuri"></a>Suporte ao International Resource Identifier em System.Uri

A classe <xref:System.Uri?displayProperty=nameWithType> foi estendida com o suporte a IDNs (nomes de domínio internacionalizados) e ao IRI (International Resource Identifier). Essas melhorias estão disponíveis no .NET Framework 3.5, 3.0 SP1 e 2.0 SP1.  
  
## <a name="iri-and-idn-support"></a>Suporte a IRI e a IDN  

 Os endereços da Web são normalmente expressos por meio de URIs (identificadores de recurso universal), que consistem de um conjunto de caracteres muito restrito:  
  
- Letras maiúsculas e minúsculas ASCII do alfabeto inglês.  
  
- Dígitos de 0 a 9.  
  
- Um pequeno número de outros símbolos ASCII.  
  
 As especificações para URIs estão documentadas em RFC 2396 e RFC 3986, publicados pela IETF (Internet Engineering Task Force).  
  
 Com o crescimento da Internet, há uma necessidade crescente de identificar recursos com idiomas diferentes do inglês. Identificadores que facilitam a essa necessidade e permitem que os caracteres não ASCII (caracteres no conjunto de caracteres Unicode/ISO 10646) são conhecidos como IRIs (International Resource Identifiers). As especificações de IRIs estão documentadas na RFC 3987, publicado pela IETF. O uso de IRIs permite que uma URL contenha caracteres Unicode.  
  
 A classe <xref:System.Uri?displayProperty=nameWithType> existente foi estendida para dar suporte a IRI com base na RFC 3987. Os usuários atuais não verão qualquer mudança do comportamento do .NET Framework 2.0, a menos que habilitem o IRI especificamente. Isso garante a compatibilidade do aplicativo com versões anteriores do .NET Framework.  
  
 Um aplicativo pode especificar se a análise do IDN (nome de domínio internacionalizado) deve ser aplicada aos nomes do domínio e se as regras de análise do IRI devem ser aplicadas. Isso pode ser feito no arquivo machine.config ou em app.config.  
  
 Habilitar o IDN converterá todos os rótulos Unicode de um nome de domínio para seus equivalentes em Punycode. Os nomes Punycode contêm apenas caracteres ASCII e sempre começam com o prefixo xn--. A razão para isso é dar suporte a servidores DNS existentes na Internet, pois a maioria dos servidores DNS dá suporte somente a caracteres ASCII (consulte RFC 3940).  
  
 Habilitar IRI e IDN afeta o valor da propriedade <xref:System.Uri.DnsSafeHost%2A?displayProperty=nameWithType>. Habilitar IRI e IDN também pode alterar o comportamento dos métodos <xref:System.Uri.Equals%2A?displayProperty=nameWithType>, <xref:System.Uri.OriginalString%2A?displayProperty=nameWithType>, <xref:System.Uri.GetComponents%2A?displayProperty=nameWithType> e <xref:System.Uri.IsWellFormedOriginalString%2A>.  
  
 A classe <xref:System.GenericUriParser?displayProperty=nameWithType> também foi estendida para permitir a criação de um analisador personalizável que dá suporte a IRI e IDN. O comportamento de um objeto <xref:System.GenericUriParser?displayProperty=nameWithType> é especificado passando-se uma combinação bit a bit dos valores disponíveis na enumeração <xref:System.GenericUriParserOptions?displayProperty=nameWithType> para o construtor <xref:System.GenericUriParser?displayProperty=nameWithType>. O tipo <xref:System.GenericUriParserOptions.IriParsing?displayProperty=nameWithType> que indica que o analisador dá suporte às regras de análise especificadas na RFC 3987 para IRI (Identificadores de Recurso Internacional). Se o IRI será realmente usado é algo que depende de o IRI estar habilitado.  
  
 O tipo <xref:System.GenericUriParserOptions.Idn?displayProperty=nameWithType> indica que o analisador dá suporte à análise de IDN (Nome de Domínio Internacionalizado) dos nomes de host. Se o IDN será realmente usado é algo que depende de o IDN estar habilitado.  
  
 Habilitar a análise de IRI executará a normalização e a verificação de caracteres de acordo com as regras recentes de IRI na RFC 3987. O valor padrão é que a análise de IRI esteja desabilitada para que normalização e a verificação de caractere sejam feitas de acordo com RFC 2396 e RFC 3986.  
  
 O processamento de IRI e IDN na classe <xref:System.Uri?displayProperty=nameWithType> também pode ser controlado usando as classes de configuração <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> e <xref:System.Configuration.IdnElement?displayProperty=nameWithType>. A configuração <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> habilita ou desabilita o processamento de IRI na classe <xref:System.Uri?displayProperty=nameWithType>. A configuração <xref:System.Configuration.IdnElement?displayProperty=nameWithType> habilita ou desabilita o processamento de IDN na classe <xref:System.Uri>. A configuração <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> também controla indiretamente o IDN. O processamento de IRI deve estar habilitado para que o processamento de IDN seja possível. Se o processamento de IRI estiver desabilitado, o processamento de IDN será definido para a configuração padrão, na qual o comportamento do .NET Framework 2.0 será usado para fins de compatibilidade e nomes IDN não serão usados.  
  
 O parâmetro de configuração para as classes de configuração <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> e <xref:System.Configuration.IdnElement?displayProperty=nameWithType> serão lidos uma vez quando a primeira classe <xref:System.Uri?displayProperty=nameWithType> for criada. Alterações nas configurações depois desse tempo serão ignoradas.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Configuration.IdnElement?displayProperty=nameWithType>
- <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- <xref:System.Uri.DnsSafeHost%2A?displayProperty=nameWithType>
