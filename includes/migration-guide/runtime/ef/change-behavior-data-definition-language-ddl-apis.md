---
ms.openlocfilehash: 4416a7c09f2d163961fe2fe3d6dfaa8bd5e66f93
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496633"
---
### <a name="change-in-behavior-in-data-definition-language-ddl-apis"></a>Mudança de comportamento nas APIs DDL (Linguagem de Definição de Dados)

#### <a name="details"></a>Detalhes

O comportamento dos APIs DDL quando AttachDBFilename é especificado foi alterado da seguinte forma:<ul><li>As cadeias de conexão não precisam especificar um valor de Catálogo Inicial. Anteriormente, AttachDBFilename e Catálogo Inicial eram obrigatórios.</li><li>Se AttachDBFilename e Catálogo Inicial forem especificados e o arquivo MDF especificado existir, o método <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> retornará <code>true</code>. Anteriormente, o valor retornado era <code>false</code>.</li><li>Se AttachDBFilename e Catálogo Inicial forem especificados e o arquivo MDF especificado existir, chamar o método <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> excluirá o arquivo.</li><li>Se <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> for chamado quando a cadeia de conexão especificar um valor de AttachDBFilename com um MDF e um Catálogo Inicial que não existam, o método gerará uma exceção <xref:System.InvalidOperationException>. Anteriormente, ele gerava uma exceção <xref:System.Data.SqlClient.SqlException>.</li></ul>

#### <a name="suggestion"></a>Sugestão

Essas alterações facilitam a criação de ferramentas e aplicativos que usam APIs de DDL. Essas alterações podem afetar a compatibilidade do aplicativo nas seguintes situações:<ul><li>O usuário escreve um código que executará um comando <code>DROP DATABASE</code> diretamente em vez de chamar <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> se <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> retornar <code>true</code>. Isso quebrará o código existente se o banco de dados não estiver anexado, mas um arquivo MDF existir.</li><li>O usuário escreve um código que espera o método <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> para gerar uma <xref:System.Data.SqlClient.SqlException> em vez de uma <xref:System.InvalidOperationException> quando os arquivos de Catálogo Inicial e de MDF não existes.</li></ul>

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
