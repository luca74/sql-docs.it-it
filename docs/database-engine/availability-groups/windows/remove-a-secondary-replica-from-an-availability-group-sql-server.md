---
title: Rimuovere una replica secondaria da un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.removesecondaryar.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e92e9180de7f3a0e5d845a702f3851fef2542ad4
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="remove-a-secondary-replica-from-an-availability-group-sql-server"></a>Rimuovere una replica secondaria da un gruppo di disponibilità (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento illustra come rimuovere una replica secondaria da un gruppo di disponibilità AlwaysOn usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Security](#Security)  
  
-   **Per rimuovere una replica secondaria utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Completamento:**  [Dopo la rimozione di una replica secondaria](#PostBestPractices)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Questa attività è supportata solo nella replica primaria.  
  
-   È possibile rimuove solo una replica secondaria da un gruppo di disponibilità.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria del gruppo di disponibilità.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per rimuovere una replica secondaria**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità**.  
  
3.  Selezionare il gruppo di disponibilità ed espandere il nodo **Repliche di disponibilità** .  
  
4.  Questo passaggio dipende dalla scelta di rimuovere più repliche o una sola replica, come indicato di seguito:  
  
    -   Per rimuovere più repliche, utilizzare il riquadro **Dettagli Esplora oggetti** per visualizzare e selezionare tutte le repliche che si desidera rimuovere. Per altre informazioni, vedere [Utilizzare Dettagli Esplora oggetti per monitorare Gruppi di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Per rimuovere una singola replica, selezionarla nel riquadro **Esplora oggetti** o **Dettagli Esplora oggetti** .  
  
5.  Fare clic con il pulsante destro del mouse sulla replica o sulle repliche secondarie selezionate e scegliere **Rimuovi da gruppo di disponibilità** nel menu dei comandi.  
  
6.  Nella finestra di dialogo **Rimozione delle repliche secondarie dal gruppo di disponibilità** scegliere **OK**per rimuovere tutte le repliche secondarie elencate. Se non si desidera rimuovere tutte le repliche elencate, fare clic su **Annulla**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per rimuovere una replica secondaria**  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* REMOVE REPLICA ON '*nome_istanza*' [,...*n*]  
  
     dove *nome_gruppo* è il nome del gruppo di disponibilità e *nome_istanza* è l'istanza del server in cui si trova la replica secondaria.  
  
     Nell'esempio seguente viene rimossa una replica secondaria dal gruppo di disponibilità *MyAG* . La replica secondaria di destinazione si trova in un'istanza del server denominata *HADR_INSTANCE* in un computer denominato *COMPUTER02*.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per rimuovere una replica secondaria**  
  
1.  Cambiare la directory (**cd**) impostandola sull'istanza del server che ospita la replica primaria.  
  
2.  Usare il cmdlet **Remove-SqlAvailabilityReplica** .  
  
     Ad esempio, il seguente comando rimuove la replica di disponibilità nel server `MyReplica` dal gruppo di disponibilità denominato `MyAg`.  Il comando deve essere eseguito nell'istanza del server che ospita la replica primaria del gruppo di disponibilità.  
  
    ```  
    Remove-SqlAvailabilityReplica `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, usare il cmdlet **Get-Help** nell'ambiente PowerShell di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="PostBestPractices"></a> Completamento: Dopo la rimozione di una replica secondaria  
 Se si specifica una replica che non è attualmente disponibile, quando viene portata online viene rilevato che è stata rimossa.  
  
 La rimozione di una replica ne arresta la ricezione di dati. Dopo la conferma della rimozione dall'archivio globale di una replica secondaria, la replica rimuove le impostazioni del gruppo di disponibilità dai relativi database che rimangono nell'istanza del server locale nello stato RECOVERING.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [Rimuovere un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
