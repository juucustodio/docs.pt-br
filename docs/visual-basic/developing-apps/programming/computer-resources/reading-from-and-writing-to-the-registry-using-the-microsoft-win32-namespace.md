---
description: 'Saiba mais sobre: leitura e gravação no registro usando o namespace Microsoft. Win32 (Visual Basic)'
title: Ler e gravar no Registro usando o namespace Microsoft.Win32
ms.date: 07/20/2015
helpviewer_keywords:
- registry [Visual Basic]
ms.assetid: 4a0dcce0-c27b-4199-baa8-ee4528da6a56
ms.openlocfilehash: beb81a6385043011a37eee82f2036aca91382240
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701580"
---
# <a name="reading-from-and-writing-to-the-registry-using-the-microsoftwin32-namespace-visual-basic"></a>Lendo e gravando no Registro usando o namespace Microsoft.Win32 (Visual Basic)

Embora `My.Computer.Registry` o deva abranger suas necessidades básicas ao programar em relação ao registro, você também pode usar as <xref:Microsoft.Win32.Registry> <xref:Microsoft.Win32.RegistryKey> classes e no <xref:Microsoft.Win32> namespace do .net.
  
## <a name="keys-in-the-registry-class"></a>Chaves na classe de Registro  

 A classe <xref:Microsoft.Win32.Registry> fornece as chaves base do Registro que podem ser usadas para acessar subchaves e seus valores. As chaves base em si são somente leitura. A tabela a seguir lista e descreve as sete chaves expostas pela classe <xref:Microsoft.Win32.Registry>.  
  
|**Chave**|**Descrição**|  
|-------------|---------------------|  
|<xref:Microsoft.Win32.Registry.ClassesRoot>|Define os tipos de documentos e as propriedades associadas a esses tipos.|  
|<xref:Microsoft.Win32.Registry.CurrentConfig>|Contém informações de configuração de hardware que não são específicas do usuário.|  
|<xref:Microsoft.Win32.Registry.CurrentUser>|Contém informações sobre as preferências do usuário atual, como variáveis ambientais.|  
|<xref:Microsoft.Win32.Registry.DynData>|Contém dados do registro dinâmico, como aqueles usados por Drivers de dispositivo virtual.|  
|<xref:Microsoft.Win32.Registry.LocalMachine>|Contém cinco subchaves (Hardware, SAM, Segurança, Software e Sistema) que armazenam os dados de configuração do computador local.|  
|<xref:Microsoft.Win32.Registry.PerformanceData>|Contém informações de desempenho de componentes de software.|  
|<xref:Microsoft.Win32.Registry.Users>|Contém informações sobre as preferências do usuário padrão.|  
  
> [!IMPORTANT]
> É mais seguro gravar dados na pasta do usuário atual (<xref:Microsoft.Win32.Registry.CurrentUser>) do que no computador local (<xref:Microsoft.Win32.Registry.LocalMachine>). Uma condição que costuma ser chamada de "squatting" ocorre quando a chave que você está criando foi criada anteriormente por outro processo, possivelmente mal-intencionado. Para evitar que isso ocorra, use um método, como <xref:Microsoft.Win32.RegistryKey.GetValue%2A>, que retornará `Nothing` se a chave ainda não existir.  
  
## <a name="reading-a-value-from-the-registry"></a>Lendo um valor do Registro  

 O código a seguir mostra como ler uma cadeia de caracteres de HKEY_CURRENT_USER.  
  
 [!code-vb[VbResourceTasks#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#20)]  
  
 O código a seguir lê, incrementa e grava uma cadeia de caracteres em HKEY_CURRENT_USER.  
  
 [!code-vb[VbResourceTasks#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.SystemException>
- <xref:System.ApplicationException>
- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [Instrução Try...Catch...Finally](../../../language-reference/statements/try-catch-finally-statement.md)
- [Ler e gravar no Registro](reading-from-and-writing-to-the-registry.md)
- [Segurança e Registro](security-and-the-registry.md)
