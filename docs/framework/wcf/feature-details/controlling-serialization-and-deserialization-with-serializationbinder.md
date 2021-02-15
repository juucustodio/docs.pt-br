---
description: 'Saiba mais sobre: controlando a serialização e a desserialização com o SerializationBinder'
title: Controlando a serialização e a desserialização sem SerializationBinder
ms.date: 07/14/2020
ms.assetid: ba8dcecf-acc7-467c-939d-021bbac797d4
ms.openlocfilehash: e1a437fa2f627fd3d5989d053a21540f139c9797
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780421"
---
# <a name="controlling-serialization-and-deserialization-with-serializationbinder"></a>Controlando a serialização e a desserialização sem SerializationBinder

> [!WARNING]
> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> Não é seguro e ***não*** pode se tornar seguro. Para obter mais informações, consulte o [Guia de segurança do BinaryFormatter](../../../standard/serialization/binaryformatter-security-guide.md).

Durante a serialização, um formatador transmite as informações necessárias para criar uma instância de um objeto do tipo e da versão corretos. Essas informações geralmente incluem o nome completo do tipo e o nome do assembly do objeto. Por padrão, a desserialização usa essas informações para criar uma instância de um objeto idêntico. Alguns usuários podem precisar controlar qual classe serializar e desserializar, porque a classe original pode não existir no computador que executa a desserialização, a classe original foi movida entre assemblies ou uma versão diferente da classe é necessária no servidor e no cliente. Para obter mais informações, consulte [uso do associador de serialização](../samples/usage-of-serialization-binder.md).  
  
> [!WARNING]
> Essa funcionalidade só está disponível ao usar o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> ou o <xref:System.Runtime.Serialization.NetDataContractSerializer> .  
  
## <a name="using-serializationbinder"></a>Usando SerializationBinder  

 O <xref:System.Runtime.Serialization.SerializationBinder> é uma classe abstrata usada para controlar os tipos reais usados durante a serialização e a desserialização. Para controlar os tipos usados durante a serialização e desserialização, derive uma classe de <xref:System.Runtime.Serialization.SerializationBinder> e substitua os <xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)> <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)> métodos e. O <xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)> método usa um <xref:System.Type> e retorna um assembly e um nome de tipo. O <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)> método usa um assembly e um nome de tipo e retorna um <xref:System.Type> .  
  
## <a name="see-also"></a>Consulte também

- [Serialização e desserialização](serialization-and-deserialization.md)
- [Utilização do associador de serialização](../samples/usage-of-serialization-binder.md)
