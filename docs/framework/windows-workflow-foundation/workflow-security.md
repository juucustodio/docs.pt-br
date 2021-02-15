---
description: 'Saiba mais sobre: segurança de fluxo de trabalho'
title: Segurança de fluxo de trabalho
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], workflow security
ms.assetid: d712a566-f435-44c0-b8c0-49298e84b114
ms.openlocfilehash: afaf5c9f5a8b0bcf707dae0e9e9669d63c5f8176
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754856"
---
# <a name="workflow-security"></a>Segurança de fluxo de trabalho

O Windows Workflow Foundation (WF) é integrado a várias tecnologias diferentes, como Microsoft SQL Server e Windows Communication Foundation (WCF). Interagir com essas tecnologias pode gerar problemas de segurança no fluxo de trabalho se feito de modo inadequado.

## <a name="persistence-security-concerns"></a>Problemas de segurança de persistência

1. Fluxos de trabalho que usam uma necessidade de atividade e de persistência <xref:System.Activities.Statements.Delay> de ser reactivated por um serviço. Windows AppFabric usa o serviço de gerenciamento (WMS) de fluxo de trabalho para reativar fluxos de trabalho com timers expirados. WMS cria <xref:System.ServiceModel.WorkflowServiceHost> para hospedar o fluxo de trabalho reactivated. Se o serviço de WMS é interrompida, os fluxos de trabalho mantidas não reactivated quando seus timers eles expiram.

2. Acesso a métodos de como exemplo de bens deve ser protegido contra as entidades mal-intencionados externos ao domínio do aplicativo. Além disso, os desenvolvedores devem garantir que o código mal-intencionado não pode ser executado no mesmo domínio de aplicativo que o código de instâncias durável.

3. Citar como exemplo de bens não deve ser executado com permissões elevadas (de administrador).

4. Os dados que estão sendo processadas fora do domínio de aplicativo devem ser protegidos.

5. Aplicativos que requerem isolamento de segurança não devem compartilhar a mesma instância de abstração de esquema. Esses aplicativos devem usar diferentes provedores de armazenamento, ou provedores de armazenamento configurados para usar instanciações diferentes de armazenamento.

## <a name="sql-server-security-concerns"></a>Problemas de segurança do SQL Server

- Quando um grande número de atividades filhos, locais, indexadores, hospedam extensões, ou os escopos são usados, ou quando os indicadores com as carrega úteis muito grandes são usados, a memória pode ser esgotada, ou as quantidades inadequadas do espaço de base de dados podem ser atribuídas durante a persistência. Isso pode ser abrandado utilizando em nível de objeto e a segurança de base de dados - nível.

- Ao usar <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, o armazenamento de instância deve ser protegido.

- Dados confidenciais no armazenamento de instância devem ser criptografados. Para obter mais informações, veja [Criptografia do SQL Server](/sql/relational-databases/security/encryption/sql-server-encryption).

- Desde que a cadeia de conexão caracteres de base de dados é incluída com frequência em um arquivo de configuração, a segurança do windows nível (ACL) deve ser usada para garantir que o arquivo de configuração (Web.Config) geralmente é seguro, e que o logon e informações de senha não estão incluídos na cadeia de conexão. A autenticação do Windows deve ser usada entre o base de dados e o servidor web em vez disso.

## <a name="considerations-for-workflowservicehost"></a>Considerações para WorkflowServiceHost

- Os pontos de extremidade do Windows Communication Foundation (WCF) usados em fluxos de trabalho devem ser protegidos. Para obter mais informações, consulte [visão geral da segurança do WCF](../wcf/feature-details/security-overview.md).

- Autorização do nível pode ser implementada usando <xref:System.ServiceModel.ServiceAuthorizationManager>. Consulte [como: criar um Gerenciador de autorização personalizado para um serviço](../wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md) para obter detalhes.

- O ServiceSecurityContext para a mensagem de entrada também está disponível no fluxo de trabalho acessando OperationContext.

## <a name="wf-security-pack-ctp"></a>Bloco CTP de segurança de WF

 O Microsoft WF Security Pack Community Technology Preview (CTP) 1 é um conjunto de atividades e sua implementação com base em [Windows Workflow Foundation](index.md) no [.NET Framework 4](/previous-versions/dotnet/netframework-4.0/w0x726c2(v=vs.100)) (WF 4) e no [Windows Identity Foundation (WIF)](/previous-versions/dotnet/framework/security/index). O bloco CTP 1 de segurança do Microsoft WF contém ambas as atividades e seus designers que ilustram como facilmente ative vários cenários relacionados a segurança usando o fluxo de trabalho, incluindo:

1. Representando uma identidade de cliente no fluxo de trabalho

2. Autorização de Em- fluxo de trabalho, como PrincipalPermission e validação de reivindicações

3. Autenticada mensagem usando ClientCredentials especificado no fluxo de trabalho, como o nome de usuário ou senha/um token recuperado de um serviço (STS) de símbolo de segurança

4. Fluxo um símbolo de segurança de cliente a um serviço back-end (delegação reivindicação- base) usando a ws-trust Ata

Para obter mais informações e baixar o WF Security Pack CTP, consulte: [WF Security Pack CTP](https://archive.codeplex.com/?p=wf)
