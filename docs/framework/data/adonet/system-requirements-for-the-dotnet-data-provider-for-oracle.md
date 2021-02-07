---
description: 'Saiba mais sobre: requisitos de sistema para o .NET Framework Provedor de Dados para Oracle'
title: Requisitos do sistema para o provedor de dados do .NET Framework para Oracle
ms.date: 03/30/2017
ms.assetid: 054f76b9-1737-43f0-8160-84a00a387217
ms.openlocfilehash: 6b48ab695fdb87b2f51f4fe29589305325329098
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766823"
---
# <a name="system-requirements-for-the-net-framework-data-provider-for-oracle"></a>Requisitos do sistema para o provedor de dados do .NET Framework para Oracle

O .NET Framework Provedor de Dados para Oracle requer o MDAC (Microsoft Data Access Components) versão 2,6 ou posterior. O MDAC 2,8 SP1 é recomendado.  
  
 Você também deve ter o cliente Oracle 8i versão 3 (8.1.7) ou posterior instalado.  
  
 O software cliente Oracle anterior à versão do Oracle 9i não pode acessar bancos de dados UTF16 porque o UTF16 é um novo recurso no Oracle 9i. Para usar esse recurso, você deve atualizar o software cliente para Oracle 9i ou posterior.  
  
## <a name="working-with-the-data-provider-for-oracle-and-unicode-data"></a>Trabalhando com os Provedor de Dados para dados do Oracle e Unicode  

Veja a seguir uma lista de problemas relacionados a Unicode que você deve considerar ao trabalhar com o .NET Framework Provedor de Dados para bibliotecas de cliente Oracle e Oracle. Para obter mais informações, consulte a documentação do Oracle.  
  
### <a name="setting-the-unicode-value-in-a-connection-string-attribute"></a>Definindo o valor Unicode em um atributo de cadeia de conexão  

Ao trabalhar com a Oracle, você pode usar o atributo de cadeia de conexão  
  
`Unicode=True`
  
para inicializar as bibliotecas de cliente Oracle no modo UTF-16. Isso faz com que as bibliotecas de cliente Oracle aceitem UTF-16 (que é muito semelhante ao UCS-2) em vez de cadeias de caracteres de byte múltiplo. Isso permite que o Provedor de Dados para Oracle trabalhe sempre com qualquer página de código Oracle sem trabalho de tradução adicional. Essa configuração só funcionará se você estiver usando clientes do Oracle 9i para se comunicar com um banco de dados Oracle 9i com o conjunto de caracteres alternativo de AL16UTF16. Quando um cliente Oracle 9i se comunica com um servidor Oracle 9i, recursos adicionais são necessários para converter os valores de **CommandText** de Unicode no conjunto de caracteres de vários bytes apropriado que o servidor Oracle9i usa. Isso pode ser evitado quando você sabe que tem a configuração segura adicionando `Unicode=True` à sua cadeia de conexão.  
  
### <a name="mixing-versions-of-oracle-client-and-oracle-server"></a>Combinação de versões do Oracle Client e do Oracle Server  

Os clientes Oracle 8i não podem acessar dados **nchar**, **NVARCHAR2** ou **NClob** em bancos de dado Oracle 9i quando o conjunto de caracteres nacionais do servidor é especificado como AL16UTF16 (a configuração padrão para Oracle 9i). Como o suporte para o conjunto de caracteres UTF-16 não foi introduzido até o Oracle 9i, os clientes Oracle 8i não podem lê-lo.  
  
### <a name="working-with-utf-8-data"></a>Trabalhando com dados UTF-8  

Para definir o conjunto de caracteres alternativo, defina a chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE\HOMEID\NLS_LANG como UTF8. Consulte as notas de instalação do Oracle em sua plataforma para obter mais informações. A configuração padrão é o conjunto de caracteres primário do idioma do qual você está instalando o software cliente Oracle. Não definir o idioma para corresponder ao conjunto de caracteres do idioma nacional do banco de dados ao qual você está se conectando fará com que as associações de parâmetro e coluna enviem ou recebam dados em seu conjunto de caracteres de banco de dado primário, não no conjunto de caracteres nacionais.  
  
### <a name="oraclelob-can-only-update-full-characters"></a>OracleLob só pode atualizar caracteres completos.  

Por motivos de usabilidade, o <xref:System.Data.OracleClient.OracleLob> objeto herda da classe .NET Framework Stream e fornece os métodos **ReadByte** e **WriteByte** . Ele também implementa métodos, como **CopyTo** e **Erase**, que funcionam em seções de objetos **LOB** da Oracle. Por outro lado, o software cliente Oracle fornece várias APIs para trabalhar com caracteres **LOB** s (**CLOB** e **NClob**). No entanto, essas APIs funcionam somente em caracteres completos. Devido a essa diferença, o Provedor de Dados para Oracle implementa o suporte para **leitura** e **ReadByte** para trabalhar com dados UTF-16 de maneira inteligente. No entanto, os outros métodos do objeto **OracleLob** permitem apenas operações de caractere completo.  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
