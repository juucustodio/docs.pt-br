---
title: Ferramenta geradora de serializador de XML (Sgen.exe)
description: O gerador de serializador XML cria um assembly de serialização XML para tipos em um assembly, o que melhora o desempenho de inicialização do XmlSerializer.
ms.date: 03/30/2017
ms.assetid: cc1d1f1c-fb26-4be9-885a-3fe84c81cec6
ms.openlocfilehash: c2f33236e39f61638118f45f0d5ab5385df27ac3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676511"
---
# <a name="xml-serializer-generator-tool-sgenexe"></a>Ferramenta geradora de serializador de XML (Sgen.exe)

O gerador de serializador XML cria um assembly de serialização XML para tipos em um assembly especificado. O assembly de serialização melhora o desempenho de inicialização de um <xref:System.Xml.Serialization.XmlSerializer> quando serializa ou desserializa objetos dos tipos especificados.
  
## <a name="syntax"></a>Sintaxe

Execute a ferramenta na linha de comando.
  
```console  
sgen [options]  
```
  
> [!TIP]
> Para que as ferramentas de .NET Framework funcionem corretamente, você deve definir as `Path` `Include` variáveis de ambiente, e `Lib` corretamente. Defina essas variáveis de ambiente executando SDKVars.bat, que está localizado no \<SDK> \\ \<version> diretório \bin. SDKVars.bat deve ser executado em todo shell de comando.
  
## <a name="parameters"></a>parâmetros  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|**/a \[ me \] :**_nome de arquivo_|Gera o código de serialização para todos os tipos contidos no assembly ou no executável especificado pelo *filename*. Somente um nome de arquivo pode ser fornecido. Se esse argumento for repetido, o último nome de arquivo será usado.|  
|**/c \[ Ackers \] :**_Opções_|Especifica as opções para passar para o compilador C#. Todas as opções csc.exe têm suporte quando são passadas para o compilador. Isso pode ser usado para especificar que o assembly deve ser assinado e para especificar o arquivo de chave.|  
|**/d \[ ebug\]**|Gera uma imagem que pode ser usada com um depurador.|  
|**/f \[ orçar\]**|Força a substituição de um assembly existente de mesmo nome. O padrão é **false**.|  
|**/Help ou/?**|Exibe sintaxe de comando e opções para a ferramenta.|  
|**/k \[ er\]**|Suprime a exclusão dos arquivos de origem gerados e outros arquivos temporários depois que tiverem sido compilados no assembly de serialização. Isso pode ser usado para determinar se a ferramenta está gerando o código de serialização para um tipo específico.|  
|**/n \[ ologo\]**|Suprime a exibição do banner de inicialização da Microsoft.|  
|**/o \[ UT \] :**_caminho_|Especifica o diretório no qual salvar o assembly gerado. **Observação:** o nome do assembly gerado é composto pelo nome do assembly de entrada mais “xmlSerializers.dll”.|  
|**/p \[ roxytypes\]**|Gera o código de serialização somente para os tipos de proxy de serviço Web XML.|  
|**/r \[ eference \] :**_AssemblyFiles_|Especifica os assemblies que são referenciados pelos tipos que exigem a serialização de XML. Aceita vários arquivos de assembly separados por vírgulas.|  
|**/s \[ ilent\]**|Suprime a exibição de mensagens de sucesso.|  
|**/t \[ tipo \] :**_Type_|Gera o código de serialização somente para o tipo especificado.|  
|**/v \[ erbose\]**|Exibe a saída detalhada para depuração. Lista os tipos do assembly de destino que não podem ser serializados com o <xref:System.Xml.Serialization.XmlSerializer>.|  
|**/?**|Exibe sintaxe de comando e opções para a ferramenta.|  
  
## <a name="remarks"></a>Comentários  

 Quando o Gerador do Serializador do XML não é usado, um <xref:System.Xml.Serialization.XmlSerializer> gera o código de serialização e um assembly de serialização para cada tipo toda vez que um aplicativo é executado. Para melhorar o desempenho da inicialização de serialização XML, use a ferramenta Sgen.exe para gerar esses assemblies com antecedência. Esses assemblies podem então ser implantados com o aplicativo.  
  
 O Gerador do Serializador do XML também pode aprimorar o desempenho de clientes que usam proxies de serviço Web XML para se comunicarem com servidores porque o processo de serialização não incorrerá em um acerto de desempenho quando o tipo for carregado pela primeira vez.  
  
 Esses assemblies gerados não podem ser usados no lado do servidor de um serviço Web. Essa ferramenta é somente para clientes de serviço Web e cenários de serialização manual.  
  
 Se o assembly que contém o tipo para serializar é denominado MyType.dll, o assembly de serialização associada será denominado MyType.XmlSerializers.dll.  
  
## <a name="examples"></a>Exemplos  

 O comando a seguir cria um assembly denominado Data.XmlSerializers.dll para serializar todos os tipos contidos no assembly denominado Data.dll.  
  
```console  
sgen Data.dll
```  
  
 O assembly Data.XmlSerializers.dll pode ser referenciado do código que precisa serializar e desserializar os tipos no Data.dll.  
  
## <a name="see-also"></a>Confira também

- [Ferramentas](../../framework/tools/index.md)
- [Prompts de comando](../../framework/tools/developer-command-prompt-for-vs.md)
