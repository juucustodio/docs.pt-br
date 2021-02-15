---
description: 'Saiba mais sobre: elementos de diretiva de tempo de execução'
title: Elementos da diretiva de runtime
ms.date: 03/30/2017
ms.assetid: 3fe5848c-ecd7-4136-970b-8e48d250bde6
ms.openlocfilehash: 74ff6c7d782f48106e37b99187770d8e82926be4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738423"
---
# <a name="runtime-directive-elements"></a>Elementos da diretiva de runtime

O formato do arquivo de diretivas (rd.xml) do runtime suporta os seguintes elementos de diretiva de runtime. Consulte a [Referência do arquivo de configuração (rd.xml) de diretivas de runtime](runtime-directives-rd-xml-configuration-file-reference.md) para uma representação hierárquica.  
  
 [\<Application>](application-element-net-native.md)  
 Aplica a política de reflexão de runtime a todos os tipos usados pelo aplicativo e serve como um contêiner para tipos amplos de aplicativos e membros de tipo cujos metadados estão disponíveis para reflexão no runtime. Este é um filho do [\<Directives>](directives-element-net-native.md) elemento.  
  
 [\<Assembly>](assembly-element-net-native.md)  
 Aplica a política de runtime a todos os tipos em um assembly. Esse é um filho dos [\<Application>](application-element-net-native.md) elementos e [\<Library>](library-element-net-native.md) .  
  
 [\<AttributeImplies>](attributeimplies-element-net-native.md)  
 Se a diretiva que o contém [\<Type>](type-element-net-native.md) for um atributo, o aplicará a política de tempo de execução a elementos de código aos quais esse atributo será aplicado.  
  
 [\<Directives>](directives-element-net-native.md)  
 O elemento raiz em cada arquivo de diretivas de tempo de execução para .NET Native. Seus elementos filho são [\<Application>](application-element-net-native.md) e [\<Library>](library-element-net-native.md) .  
  
 [\<Event>](event-element-net-native.md)  
 Aplica a política de runtime a um evento. Esse é um filho dos [\<Type>](type-element-net-native.md) elementos e [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .  
  
 [\<Field>](field-element-net-native.md)  
 Aplica a política de runtime a um campo. Esse é um filho dos [\<Type>](type-element-net-native.md) elementos e [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .  
  
 [\<GenericParameter>](genericparameter-element-net-native.md)  
 Aplica a política de runtime ao tipo de parâmetro de um tipo ou método genérico.  
  
 [\<ImpliesType>](impliestype-element-net-native.md)  
 Aplica a política de runtime a um tipo, se ela tiver sido aplicada ao tipo ou método recipiente.  
  
 [\<Library>](library-element-net-native.md)  
 Aplica a política de runtime a todos os tipos em um assembly. Esse é um filho dos [\<Application>](application-element-net-native.md) elementos e [\<Library>](library-element-net-native.md) .  
  
 [\<Method>](method-element-net-native.md)  
 Aplica a política de runtime a um método. Esse é um filho dos [\<Type>](type-element-net-native.md) elementos e [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .  
  
 [\<MethodInstantiation>](methodinstantiation-element-net-native.md)  
 Aplica a diretiva de runtime para um método genérico construído. Esse é um filho dos [\<Type>](type-element-net-native.md) elementos e [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .  
  
 [\<Namespace>](namespace-element-net-native.md)  
 Aplica a política de runtime a todos os tipos em um namespace.  
  
 [\<Parameter>](parameter-element-net-native.md)  
 Aplica a política de runtime ao tipo do argumento passado para um método.  
  
 [\<Property>](property-element-net-native.md)  
 Aplica a política de runtime a uma propriedade. Esse é um filho dos [\<Type>](type-element-net-native.md) elementos e [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .  
  
 [\<Subtypes>](subtypes-element-net-native.md)  
 Aplica a política de runtime a todas as classes herdadas do tipo recipiente.  
  
 [\<Type>](type-element-net-native.md)  
 Aplica a política de runtime a um tipo.  
  
 [\<TypeInstantiation>](typeinstantiation-element-net-native.md)  
 Aplica a política de runtime a um tipo genérico construído.  
  
 [\<TypeParameter>](typeparameter-element-net-native.md)  
 Aplica a política de runtime ao tipo representado por um argumento <xref:System.Type> passado para um método.  
  
## <a name="see-also"></a>Consulte também

- [Referência do arquivo de configuração rd.xml](runtime-directives-rd-xml-configuration-file-reference.md)
