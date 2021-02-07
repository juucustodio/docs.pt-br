---
description: 'Saiba mais sobre: <oidEntry> elemento'
title: Elemento <oidEntry>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/oidMap/oidEntry
- http://schemas.microsoft.com/.NetConfiguration/v2.0#oidEntry
helpviewer_keywords:
- <oidEntry> element
- oidEntry element
ms.assetid: 22fb88b0-bf27-489c-9ca0-e65950ac136c
ms.openlocfilehash: d5fe22018377e247ffa0b6addb58cbeee7119e66
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99698746"
---
# <a name="oidentry-element"></a>Elemento \<oidEntry>

Mapeia um OID (identificador de objeto) do ASN.1 para um nome amigável.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<mscorlib>**](mscorlib-element-for-cryptography-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptographySettings>**](cryptographysettings-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<oidMap>**](oidmap-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<oidEntry>**

## <a name="syntax"></a>Syntax  
  
```xml  
<oidEntry OID="object identifier number" name="friendly name" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**OIDs**|Atributo obrigatório.<br /><br /> Especifica a OID ASN. 1 correspondente ao algoritmo implementado pela sua classe.|  
|**name**|Atributo obrigatório.<br /><br /> Especifica o valor para o atributo **Name** na [\<nameEntry>](nameentry-element.md) marca.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`cryptographySettings`|Contém configurações de criptografia.|  
|`mscorlib`|Contém o `cryptographySettings` elemento.|  
|`oidMap`|Contém mapeamentos de OID (identificador de objeto) ASN para classes.|  
  
## <a name="remarks"></a>Comentários  

 Os identificadores de objeto ASN. 1 identificam algoritmos em alguns formatos criptográficos. Mapeie identificadores de objeto para nomes amigáveis para os algoritmos que você deseja identificar.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como usar o **\<oidEntry>** elemento para mapear um identificador de objeto para o algoritmo de hash RIPEMD-160 para uma implementação desse algoritmo de hash.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RIPEMD-160" class="MyCrypto"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Esquema do arquivo de configuração](../index.md)
- [Esquema de configurações de criptografia](index.md)
- [Serviços criptográficos](../../../../standard/security/cryptographic-services.md)
- [Configurando classes de criptografia](../../configure-cryptography-classes.md)
- [Mapeando identificadores de objeto para algoritmos de criptografia](../../map-object-identifiers-to-cryptography-algorithms.md)
