---
title: Creare un proxy di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], creating
ms.assetid: 142e0c55-a8b9-4669-be49-b9dc602d5988
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 92f50fd5d4a192e44238625c97449f23a41d9629
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2018
---
# <a name="create-a-sql-server-agent-proxy"></a>Creazione di un proxy di SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come creare un proxy SQL Server Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
Un account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent definisce un contesto di sicurezza in cui è possibile l'esecuzione di un passaggio di processo. Ogni proxy corrisponde a una credenziale di sicurezza Per impostare le autorizzazioni per un particolare passaggio di processo, creare un proxy dotato delle autorizzazioni necessarie per un sottosistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent e quindi assegnarlo al passaggio di processo.  
  
**Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
    [Limitazioni e restrizioni](#Restrictions)  
  
    [Security](#Security)  
  
-   **Per creare un proxy di SQL Server Agent utilizzando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   Se non disponibili, prima di creare un proxy è necessario creare le credenziali.  
  
-   I proxy di[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent utilizzano le credenziali per archiviare le informazioni sugli account utente di Windows. L'utente specificato nella credenziale deve avere l'autorizzazione "Accedi al computer dalla rete" (SeNetworkLogonRight) nel computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] è in esecuzione.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent verifica l'accesso al sottosistema per un proxy e garantisce l'accesso al proxy ad ogni esecuzione del passaggio di processo. Se il proxy non dispone più di accesso al sottosistema, il passaggio di processo non viene eseguito correttamente. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent rappresenta l'utente specificato nel proxy ed esegue il passaggio di processo.  
  
-   La creazione di un proxy non implica la modifica delle autorizzazioni per l'utente specificato nella credenziale del proxy. È possibile ad esempio creare un proxy per un utente che non dispone dell'autorizzazione per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. In questo caso, i passaggi di processo che utilizzano il proxy non sono in grado di connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Se l'account di accesso per l'utente viene utilizzato per l'accesso al proxy oppure se l'utente appartiene a un qualsiasi ruolo che prevede l'accesso al proxy, l'utente potrà utilizzare il proxy in un passaggio di processo.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
  
-   Solo i membri del ruolo predefinito del server **sysadmin** sono autorizzati a creare, modificare o eliminare gli account proxy. Gli utenti che non sono membri del ruolo predefinito del server **sysadmin** devono essere aggiunti a uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nel database **msdb** per poter utilizzare i proxy: **SQLAgentUserRole**, **SQLAgentReaderRole**o **SQLAgentOperatorRole**.  
  
-   Richiede l'autorizzazione **ALTER ANY CREDENTIAL** se si creano credenziali oltre al proxy.  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>Per creare un proxy di SQL Server Agent  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera creare un proxy SQL Server Agent.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Proxy** e scegliere **Nuovo proxy**.  
  
4.  Nella pagina **Generale** della finestra di dialogo **Nuovo account proxy** immettere il nome del nuovo account proxy nella casella **Nome proxy** .  
  
5.  Nella casella **Nome credenziali** immettere il nome delle credenziali di sicurezza che verranno utilizzate dall'account proxy.  
  
6.  Immettere una descrizione dell'account proxy nella casella **Descrizione** .  
  
7.  In **Attivo nei sottosistemi seguenti**, selezionare il sottosistema o i sottosistemi adatti per questo proxy.  
  
8.  Nella pagina **Entità** aggiungere o rimuovere account di accesso oppure ruoli per concedere o negare l'accesso all'account proxy.  
  
9. Al termine, fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>Per creare un proxy di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- creates credential CatalogApplicationCredential  
    USE msdb ;  
    GO  
    CREATE CREDENTIAL CatalogApplicationCredential WITH IDENTITY = 'REDMOND/TestUser',   
        SECRET = 'G3$1o)lkJ8HNd!';  
    GO  
    -- creates proxy "Catalog application proxy" and assigns
    -- the credential 'CatalogApplicationCredential' to it.  
    EXEC dbo.sp_add_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 1,  
        @description = 'Maintenance tasks on catalog application.',  
        @credential_name = 'CatalogApplicationCredential' ;  
    GO  
    -- grants the proxy "Catalog application proxy" access to 
    -- the ActiveX Scripting subsystem.  
    EXEC dbo.sp_grant_proxy_to_subsystem  
        @proxy_name = N'Catalog application proxy',  
        @subsystem_id = 2 ;  
    GO  
    ```  
  
Per altre informazioni, vedere:  
  
-   [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/en-us/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)  
  
-   [sp_add_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/cb59df37-f103-439b-bec1-2871fb669a8b)  
  
-   [sp_grant_proxy_to_subsystem (Transact-SQL)](http://msdn.microsoft.com/en-us/866aaa27-a1e0-453a-9b1b-af39431ad9c2)  
  
