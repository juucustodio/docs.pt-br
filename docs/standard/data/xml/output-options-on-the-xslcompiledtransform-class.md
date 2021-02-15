---
description: 'Saiba mais sobre: opções de saída na classe XslCompiledTransform'
title: Opções de saída na classe de XslCompiledTransform
ms.date: 03/30/2017
ms.assetid: 91ce8cba-386c-411e-bb38-0891a0393c0a
ms.openlocfilehash: 8f16de929ba196eddb6ebb4b8b251668820b4d91
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783294"
---
# <a name="output-options-on-the-xslcompiledtransform-class"></a>Opções de saída na classe de XslCompiledTransform

Este tópico discute opções de saída disponíveis XSLT. Você pode especificar opções de saída na folha de estilos, ou o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> .  
  
## <a name="xsloutput-element"></a>Elemento xsl:output  

 O elemento de `xsl:output` especificar opções para a saída. O tipo de saída especificado pelo método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> determina o comportamento das opções de `xsl:output` .  
  
 A tabela a seguir descreve o comportamento para cada um dos atributos disponíveis no elemento de `xsl:output` quando o tipo de saída é um fluxo ou um <xref:System.IO.TextWriter>.  
  
|Nome do atributo|Comportamento|  
|--------------------|--------------|  
|method|Com suporte.|  
|version|Ignorado. A versão é sempre 1,0 para XML e 4,0 para HTML.|  
|codificando|Ignorado para gerar a <xref:System.IO.TextWriter>. A propriedade de <xref:System.IO.TextWriter.Encoding%2A?displayProperty=nameWithType> é usada em vez.|  
|omit-xml-declaration|Com suporte.|  
|autônomos|Com suporte.|  
|doctype-public|Com suporte.|  
|doctype-system|Com suporte.|  
|cdata-section-elements|Com suporte.|  
|indent|Com suporte.|  
|media-type|Com suporte.|  
  
#### <a name="sending-output-to-an-xmlwriter"></a>Enviando saída para um XmlWriter  

 Se a folha de estilos usa o elemento de `xsl:output` e o tipo de saída é um objeto de <xref:System.Xml.XmlWriter> , você deve usar a propriedade de <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A?displayProperty=nameWithType> quando você cria o objeto de <xref:System.Xml.XmlWriter> . A propriedade de <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A?displayProperty=nameWithType> retorna um objeto de <xref:System.Xml.XmlWriterSettings> que contém informações derivada de elemento de `xsl:output` de uma folha de estilos compilado. Este objeto de <xref:System.Xml.XmlWriterSettings> pode ser passado para o método de <xref:System.Xml.XmlWriter.Create%2A?displayProperty=nameWithType> para criar um objeto de <xref:System.Xml.XmlWriter> com as configurações corretas.  
  
## <a name="output-types"></a>Tipos de saída  

 A lista a seguir descreve os tipos de saída disponível no comando de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> .  
  
#### <a name="xmlwriter"></a>XmlWriter  

 A classe de <xref:System.Xml.XmlWriter> gravará fluxos XML ou arquivos. Você pode especificar os recursos para oferecer suporte no objeto de <xref:System.Xml.XmlWriter> , incluindo opções de saída, usando a classe de <xref:System.Xml.XmlWriterSettings> . A classe de <xref:System.Xml.XmlWriter> é uma parte integral de estrutura de <xref:System.Xml> . Use esse tipo de saída para canalizar os resultados de saída em outro processo XML.  
  
#### <a name="string"></a>String  

 Use esse tipo de saída para especificar a URL do arquivo de saída.  
  
#### <a name="stream"></a>Fluxo  

 Um fluxo é uma abstração de uma sequência de bytes, como um arquivo, um dispositivo de arquivos entrada/saída, um pipe de comunicação de inter- processo, ou um soquete TCP/IP. A classe de <xref:System.IO.Stream> e suas classes derivadas fornecem uma visão genérica desses tipos diferentes de entrada e saída, isolando o programador de detalhes específicos do sistema operacional e dispositivos subjacentes.  
  
 Use esse tipo de saída para enviar dados a <xref:System.IO.FileStream>, a <xref:System.IO.MemoryStream>, ou um fluxo de saída (`Response.OutputStream`).  
  
#### <a name="textwriter"></a>TextWriter  

 Os caracteres sequenciais de grava de <xref:System.IO.TextWriter> . É implementado nas classes de <xref:System.IO.StringWriter> e de <xref:System.IO.StreamWriter> , que gravam caracteres para cadeias de caracteres ou para fluxos, respectivamente. Use esse tipo de saída quando você deseja para a saída para uma cadeia de caracteres.  
  
## <a name="notes"></a>Observações  
  
- Para gravar marcas vazios, um espaço é escrito entre o último caractere do nome de elemento e a barra invertida, `<myElement />` por exemplo. Isso permite que um navegadores mais antigos exibir as páginas corretamente gerados HTML.  
  
## <a name="see-also"></a>Consulte também

- [Transformações XSLT](xslt-transformations.md)
