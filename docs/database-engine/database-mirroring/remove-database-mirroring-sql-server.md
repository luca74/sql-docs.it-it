---
title: Rimuovere il mirroring del database (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 601932c4894f4253df9ff95e2e8f280b2850fd38
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="remove-database-mirroring-sql-server"></a>Rimuovere il mirroring del database (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento illustra come rimuovere il mirroring del database da un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  Il proprietario del database può arrestare manualmente una sessione di mirroring del database in qualsiasi momento, rimuovendo il mirroring dal database.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per rimuovere il mirroring del database mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la rimozione del mirroring del database](#FollowUp)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>Per rimuovere il mirroring del database  
  
1.  Durante una sessione di mirroring del database, connettersi all'istanza del server principale e in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e selezionare il database.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Server mirror**. Viene visualizzata la pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
4.  Nel riquadro **Selezione pagina** fare clic su **Mirroring**.  
  
5.  Per rimuovere il mirroring, scegliere **Rimuovi mirroring**. Verrà richiesta una conferma. Se si fa clic su **Sì**, la sessione verrà arrestata e il mirroring verrà rimosso dal database.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Per rimuovere il mirroring del database, utilizzare **Proprietà database**. Utilizzare la pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
#### <a name="to-remove-database-mirroring"></a>Per rimuovere il mirroring del database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] di qualsiasi partner di mirroring.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Eseguire l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] riportata di seguito.  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     dove *database_name* è il database con mirroring di cui si vuole rimuovere la sessione.  
  
     Nell'esempio seguente viene rimosso il mirroring del database dal database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="FollowUp"></a> Completamento: Dopo la rimozione del mirroring del database  
  
> [!NOTE]  
>  Per informazioni sull'impatto della rimozione del mirroring del database, vedere [Rimozione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   **In caso di riavvio del mirroring nel database**  
  
     Prima di poter riavviare il mirroring è necessario che tutti i backup di log eseguiti nel database principale dopo la rimozione del mirroring vengano applicati al database mirror.  
  
-   **In caso di non riavvio del mirroring**  
  
     Facoltativamente, è possibile recuperare il database mirror precedente. Nell'istanza del server mirror è possibile utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  Se questo database viene recuperato, online saranno disponibili due database divergenti con lo stesso nome. Di conseguenza, è necessario assicurarsi che i client possano accedere soltanto a uno di essi, generalmente al database principale più recente.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Sospendere o riprendere una sessione di mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [Rimuovere il server di controllo del mirroring da una sessione di mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [Esempio: Impostazione del mirroring del database tramite certificati &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Impostazione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
