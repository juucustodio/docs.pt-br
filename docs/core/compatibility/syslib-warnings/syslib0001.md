---
title: Aviso de SYSLIB0001
description: Saiba mais sobre o obsoletions que gera SYSLIB0001 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 6c4b6a2f41e9dc044ef76bb5a53a4a54a44bca5a
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596447"
---
# <a name="syslib0001-the-utf-7-encoding-is-insecure"></a>SYSLIB0001: a codificação UTF-7 é insegura

A codificação UTF-7 não está mais em uso amplo entre aplicativos, e muitas especificações agora [proíbem seu uso](https://security.stackexchange.com/a/68609/3573) no intercâmbio. Ele também é [usado ocasionalmente como um vetor de ataque](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=utf-7) em aplicativos que não antecipam a ocorrência de dados codificados em UTF-7. A Microsoft avisa sobre o uso do <xref:System.Text.UTF7Encoding?displayProperty=nameWithType> porque não fornece detecção de erros.

Consequentemente, as seguintes APIs são marcadas como obsoletas, a partir do .NET 5,0. O uso dessas APIs gera aviso `SYSLIB0001` no momento da compilação.

- Propriedade <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType>
- <xref:System.Text.UTF7Encoding.%23ctor%2A> construtores

## <a name="workarounds"></a>Soluções Alternativas

- Se você estiver usando <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> ou <xref:System.Text.UTF7Encoding> dentro de seu próprio protocolo ou formato de arquivo:

  Alterne para o usando o <xref:System.Text.Encoding.UTF8?displayProperty=nameWithType> ou o <xref:System.Text.UTF8Encoding> . O UTF-8 é um padrão da indústria e tem amplo suporte em linguagens, sistemas operacionais e tempos de execução. O uso de UTF-8 facilita a manutenção futura de seu código e o torna mais interoperável com o restante do ecossistema.

- Se você estiver comparando uma <xref:System.Text.Encoding> instância do <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> :

  Em vez disso, considere executar uma verificação na página de código UTF-7 conhecida, que é `65000` . Ao comparar com a página de código, você evita o aviso e também lida com alguns casos de borda, como se alguém chamou `new UTF7Encoding()` ou subclasse o tipo.

  ```csharp
  void DoSomething(Encoding enc)
  {
      // Don't perform the check this way.
      // It produces a warning and misses some edge cases.
      if (enc == Encoding.UTF7)
      {
          // Encoding is UTF-7.
      }

      // Instead, perform the check this way.
      if (enc != null && enc.CodePage == 65000)
      {
          // Encoding is UTF-7.
      }
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Confira também

- [Os caminhos do código UTF-7 estão obsoletos](../core-libraries/5.0/utf-7-code-paths-obsolete.md)
