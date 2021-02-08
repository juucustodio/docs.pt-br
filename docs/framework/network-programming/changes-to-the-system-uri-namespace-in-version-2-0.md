---
description: 'Saiba mais sobre: alterações no namespace System. URI na versão 2,0'
title: Alterações no namespace System.Uri na versão 2.0
ms.date: 03/30/2017
ms.assetid: 35883fe9-2d09-4d8b-80ca-cf23a941e459
ms.openlocfilehash: 8b5e2f2b3b59fba96e20e40a4df18273a2f6034f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791615"
---
# <a name="changes-to-the-systemuri-namespace-in-version-20"></a>Alterações no namespace System.Uri na versão 2.0

Várias alterações foram feitas na classe <xref:System.Uri?displayProperty=nameWithType>. Essas alterações corrigiram comportamentos incorretos, além de melhorarem a usabilidade e a segurança.

## <a name="obsolete-and-deprecated-members"></a>Membros obsoletos e preteridos

 Construtores:

- Todos os construtores que têm um parâmetro `dontEscape`.

 Métodos:

- <xref:System.Uri.CheckSecurity%2A>

- <xref:System.Uri.Escape%2A>

- <xref:System.Uri.Canonicalize%2A>

- <xref:System.Uri.Parse%2A>

- <xref:System.Uri.IsReservedCharacter%2A>

- <xref:System.Uri.IsBadFileSystemCharacter%2A>

- <xref:System.Uri.IsExcludedCharacter%2A>

- <xref:System.Uri.EscapeString%2A>

## <a name="changes"></a>Alterações

- Para esquemas de URI (Uniform Resource Identifier) conhecidos por não terem uma parte da consulta (arquivo, ftp e outros), o caractere “?” é sempre ignorado e não é considerado o início de uma parte <xref:System.Uri.Query%2A>.

- Para URIs de arquivo implícitos (no formato `c:\directory\file@name.txt`), o caractere de fragmento (“#”) é sempre seguido por caracteres de escape, a menos que seja solicitado que o escape seja totalmente desfeito ou se <xref:System.Uri.LocalPath%2A> for `true`.

- O suporte ao nome do host UNC foi removido; a especificação de IDN para representar nomes de host internacionais foi adotada.

- <xref:System.Uri.LocalPath%2A> sempre retorna uma cadeia de caracteres totalmente sem escape.

- <xref:System.Uri.ToString%2A> não desfaz o escape de um caractere “%”, “?” ou “#” seguido por um caractere de escape.

- <xref:System.Uri.Equals%2A> agora inclui a parte <xref:System.Uri.Query%2A> na verificação de igualdade.

- Os operadores “==” e “!=” foram substituídos e vinculados ao método <xref:System.Uri.Equals%2A>.

- <xref:System.Uri.IsLoopback%2A> agora produz resultados consistentes.

- O URI “`file:///path`” não é mais convertido em `file://path`.

- “#” agora é reconhecido como um terminador de nome do host. Ou seja, `http://contoso.com#fragment` agora é convertido em `http://contoso.com/#fragment`.

- Foi corrigido um bug que ocorria durante a combinação de um URI de base com um fragmento.

- Foi corrigido um bug no <xref:System.Uri.HostNameType%2A>.

- Foi corrigido um bug na análise NNTP.

- Um URI no formato HTTP:contoso.com agora gera uma exceção de análise.

- O Framework manipula corretamente userinfo em um URI.

- A compactação de caminho do URI foi corrigida, de modo que um URI desfeito não possa percorrer o sistema de arquivos acima da raiz.

## <a name="see-also"></a>Confira também

- <xref:System.Uri?displayProperty=nameWithType>
