---
title: Creare un passaggio di processo di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c3cff59c5192f94fe7a3d56116934b78df89be2
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2018
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come creare e definire passaggi del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] che consentono di eseguire comandi e query di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Analysis Services utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] o SQL Server Management Objects.  
  
-   **Prima di iniziare:**  
  
    [Limitazioni e restrizioni](#Restrictions)  
  
    [Security](#Security)  
  
-   **Per creare i passaggi di un processo di SQL Server utilizzando i comandi e/o le query di Analysis Services con:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   Se il passaggio del processo utilizza un comando di Analysis Services, l'istruzione del comando deve essere un metodo **Execute** di Servizi di XML for Analysis Services. L'istruzione non può includere un elemento Envelope SOAP (Simple Object Access Protocol) completo o un metodo **Discover** di XML for Analysis. A differenza di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] , i passaggi di processo di **Agent non supportano le buste SOAP complete e il metodo** Discover [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Per altre informazioni su XML for Analysis Services, vedere [Panoramica di XML for Analysis (XMLA)](http://msdn.microsoft.com/library/ms187190.aspx).  
  
-   Se il passaggio del processo utilizza una query di Analysis Services, l'istruzione della query deve essere una query di espressioni MDX. Per altre informazioni su MDX, vedere [Elementi fondamentali dell'istruzione MDX (MDX)](http://msdn.microsoft.com/en-us/a560383b-bb58-472e-95f5-65d03d8ea08b).  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
  
-   Per eseguire un passaggio di processo in cui viene utilizzato il sottosistema Analysis Services, è necessario che l'utente sia membro del ruolo predefinito del server **sysadmin** o che sia autorizzato ad accedere a un account proxy valido definito per l'utilizzo di questo sottosistema. L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent o l'account proxy deve inoltre essere amministratore di Analysis Services, nonché un account di dominio Windows valido.  
  
-   Solo i membri del ruolo predefinito del server **sysadmin** sono autorizzati a scrivere l'output di un passaggio del processo in un file. Se il passaggio del processo viene eseguito da utenti appartenenti al ruolo di database **SQLAgentUserRole** nel database **msdb** , sarà possibile scrivere l'output solo in una tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent viene scritto l'output del passaggio di processo nella tabella **sysjobstepslog** del database **msdb** .  
  
-   Per informazioni dettagliate, vedere [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Per creare un passaggio di processo di un comando di Analysis Services  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per altre informazioni sulla creazione di un processo, vedere [Creazione di processi](../../ssms/agent/create-jobs.md).  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Comando di SQL Server Analysis Services**.  
  
6.  Nell'elenco **Esegui come** selezionare un proxy definito per l'utilizzo del sottosistema Comando di Analysis Services. Un utente membro del ruolo predefinito del server **sysadmin** è inoltre autorizzato a selezionare **Account del servizio SQL Server Agent** per l'esecuzione di questo passaggio del processo.  
  
7.  Selezionare il **Server** in cui verrà eseguito il passaggio del processo oppure digitare il nome del server desiderato.  
  
8.  Nella casella **Comando** immettere l'istruzione da eseguire oppure fare clic su **Apri** per selezionare l'istruzione desiderata.  
  
9. Fare clic sulla pagina **Avanzate** per definire le opzioni relative al passaggio del processo, ad esempio l'azione che dovrà essere eseguita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in caso di esito positivo o negativo del passaggio del processo, il numero di tentativi di esecuzione del passaggio del processo e il percorso in cui scrivere l'output del passaggio del processo.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Per creare un passaggio del processo di una query di Analysis Services  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per altre informazioni sulla creazione di un processo, vedere [Creazione di processi](../../ssms/agent/create-jobs.md).  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Query di SQL Server Analysis Services**.  
  
6.  Nell'elenco **Esegui come** selezionare un proxy definito per l'utilizzo del sottosistema Query di Analysis Services. Un utente membro del ruolo predefinito del server **sysadmin** è inoltre autorizzato a selezionare **Account del servizio SQL Server Agent** per l'esecuzione di questo passaggio del processo.  
  
7.  Selezionare il **Server** e il **Database** in cui verrà eseguito il passaggio del processo oppure digitare il nome del server o del database desiderato.  
  
8.  Nella casella **Comando** immettere l'istruzione da eseguire oppure fare clic su **Apri** per selezionare l'istruzione desiderata.  
  
9. Fare clic sulla pagina **Avanzate** per definire le opzioni relative al passaggio del processo, ad esempio l'azione che dovrà essere eseguita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in caso di esito positivo o negativo del passaggio del processo, il numero di tentativi di esecuzione del passaggio del processo e il percorso in cui scrivere l'output del passaggio del processo.  
  
## <a name="TSQL"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Per creare un passaggio di processo di un comando di Analysis Services  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Per creare un passaggio del processo di una query di Analysis Services  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Utilizzo di SQL Server Management Objects  
**Per creare un passaggio di processo di uno script di PowerShell**  
  
Usare la classe **JobStep** con un linguaggio di programmazione, come XMLA o MDX. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
