---
title: "Clustering di failover e gruppi di disponibilità Always On (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
caps.latest.revision: "48"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd664120017d7e498fd2930281380c718e98aaa9
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>Clustering di failover e gruppi di disponibilità Always On (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], la soluzione di ripristino di emergenza a disponibilità elevata introdotta in [!INCLUDE[sssql11](../../../includes/sssql11_md.md)], richiede WSFC (Windows Server Failover Clustering). Sebbene inoltre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] non dipenda dal clustering di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è possibile utilizzare un'istanza di clustering di failover per ospitare una replica di disponibilità per un gruppo di disponibilità. È importante conoscere la funzione di ogni tecnologia di clustering e sapere quali sono le considerazioni necessarie per la progettazione di un ambiente di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
> [!NOTE]  
>  Per informazioni sui concetti di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , vedere [Panoramica di Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 **Contenuto dell'argomento:**  
  
-   [Windows Server Failover Clustering](#WSFC)  
  
-   [Clustering di failover di SQL Server](#SQLServerFC)  
  
-   [Le restrizioni sull'utilizzo di Gestione cluster di failover WSFC con i gruppi di disponibilità](#FCMrestrictions)  
  
##  <a name="WSFC"></a> Clustering di failover di Windows Server e gruppi di disponibilità  
 La distribuzione dei [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] richiede un cluster WSCF (Windows Server Failover Clustering). Per essere abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve trovarsi in un nodo WSFC e il nodo e il cluster WSFC devono essere online. Inoltre, ogni replica di disponibilità di un gruppo di disponibilità deve risiedere in un nodo diverso dello stesso cluster WSFC. L'unica eccezione è che quando viene eseguita la migrazione a un altro cluster WSFC, un gruppo di disponibilità può risiedere temporaneamente in due cluster.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] si basa sul cluster WSFC (Windows Server Failover Clustering) per monitorare e gestire i ruoli correnti delle repliche di disponibilità che appartengono a un determinato gruppo di disponibilità e per determinare in che modo un evento di failover influisca sulle repliche di disponibilità. Il gruppo di risorse WSFC viene creato per ogni gruppo di disponibilità che viene creato. Con il cluster WSFC è possibile eseguire il monitoraggio del gruppo di risorse per valutare lo stato di integrità della replica primaria.  
  
 Il quorum di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] si basa su tutti i nodi del cluster WSFC, indipendentemente dal fatto che un nodo del cluster ospiti una replica di disponibilità. A differenza del mirroring del database, non esiste alcun ruolo del server di controllo in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 L'integrità complessiva di un cluster WSFC è determinata dai voti di un quorum di nodi nel cluster. Se il cluster WSFC viene portato offline a causa di un'emergenza non pianificata o di un errore persistente dell'hardware o di comunicazione, è necessario un intervento amministrativo manuale. Un amministratore di cluster Windows Server or WSFC dovrà forzare un quorum e, successivamente, riportare online i nodi del cluster ancora esistenti in una configurazione non a tolleranza d'errore.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sono sottochiavi del cluster WSFC. Se si elimina e si ricrea un cluster WSFC, è necessario disabilitare e riabilitare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è ospitata una replica di disponibilità nel cluster WSFC originale.  
  
 Per informazioni sull'esecuzione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nei nodi WSFC (Windows Server Failover Clustering) e sul quorum WSFC, vedere [WSFC &#40;Windows Server Failover Clustering&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
### <a name="cross-cluster-migration-of-always-on-availability-groups-for-os-upgrade"></a>Migrazione tra cluster di gruppi di disponibilità Always On per l'aggiornamento del sistema operativo  
 A partire da [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)], in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è supportata migrazione tra cluster di gruppi di disponibilità per distribuzioni in un nuovo cluster WSFC (Windows Server Failover Clustering). In una migrazione tra cluster un gruppo o un batch di gruppi di disponibilità viene spostato nel nuovo cluster WSFC di destinazione con tempi di inattività minimi. Il processo di migrazione tra cluster consente di gestire i contratti di servizio (SLA, Service Level Agreement) durante l'aggiornamento a un cluster [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] . [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] (o versioni successive) deve essere installato e abilitato per Always On nel cluster WSFC di destinazione. L'esito positivo della migrazione tra cluster dipende da una pianificazione e una preparazione dettagliate del cluster WSFC di destinazione.  
  
 Per altre informazioni, vedere [Migrazione tra cluster di gruppi di disponibilità Always On per l'aggiornamento del sistema operativo](http://msdn.microsoft.com/library/jj873730.aspx).  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] - Istanze del cluster di failover e gruppi di disponibilità  
 È possibile configurare un secondo livello di failover a livello di istanza del server implementando il clustering di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] insieme al cluster WSFC. Una replica di disponibilità può essere ospitata da un'istanza autonoma di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o da un'istanza FCI. Solo un partner di un'istanza del cluster di failover può ospitare una replica per un gruppo di disponibilità. Quando una replica di disponibilità viene eseguita in un'istanza del cluster di failover, l'elenco dei possibili proprietari per il gruppo di disponibilità conterrà solo il nodo FCI attivo.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] non dipende da alcun mezzo di archiviazione condivisa. Tuttavia, se si utilizza un'istanza del cluster di failover (FCI) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per ospitare una o più repliche di disponibilità, per ognuna di queste FCI sarà richiesta l'archiviazione condivisa in base all'installazione dell'istanza del cluster di failover di SQL Server standard.  
  
 Per altre informazioni sui prerequisiti aggiuntivi, vedere la sezione "Prerequisiti e restrizioni per l'uso di un'istanza del cluster di failover di SQL Server per ospitare una replica di disponibilità" di [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>Confronto tra le istanze del cluster di failover e i gruppi di disponibilità  
 Indipendentemente dal numero di nodi nell'istanza FCI, in un'intera FCI viene ospitata una sola replica all'interno di un gruppo di disponibilità. Nella tabella seguente sono descritte le differenze dei concetti tra i nodi di un'istanza FCI e le repliche all'interno di un gruppo di disponibilità.  
  
||Nodi all'interno di un'istanza FCI|Repliche all'interno di un gruppo di disponibilità|  
|-|-------------------------|-------------------------------------------|  
|**Utilizzo di cluster WSFC**|Sì|Sì|  
|**Livello di protezione**|Istanza|Database|  
|**Tipo di archiviazione**|Condivisa|Non condivisi<br /><br /> Mentre le repliche di un gruppo di disponibilità non condividono le risorse di archiviazione, una replica ospitata da un'istanza del cluster di failover usa una soluzione di archiviazione condivisa come richiesto da tale istanza. La soluzione di archiviazione è condivisa solo dai nodi all'interno dell'istanza FCI e non tra le repliche del gruppo di disponibilità.|  
|**Soluzioni di archiviazione**|Collegamento diretto, rete SAN, punti di montaggio, SMB|Dipende dal tipo di nodo|  
|**Secondarie leggibili**|No*|Sì|  
|**Impostazioni dei criteri di failover applicabili**|Quorum WSFC<br /><br /> Specifiche per FCI<br /><br /> Impostazioni dei gruppi di disponibilità*|Quorum WSFC<br /><br /> Impostazioni dei gruppi di disponibilità|  
|**Risorse di cui è stato eseguito il failover**|Server, istanza e database|Solo database|  
  
 * Mentre le repliche secondarie sincrone di un gruppo di disponibilità sono sempre in esecuzione nelle rispettive istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , i nodi secondari in un'istanza del cluster di failover non hanno avviato le rispettive istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e quindi non sono leggibili. In un'istanza FCI, un nodo secondario consente di avviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo quando la proprietà del gruppo di risorse viene trasferita a questo nodo durante un failover dell'istanza FCI. Tuttavia, nel nodo FCI attivo, se un database ospitato da FCI appartiene a un gruppo di disponibilità e la replica di disponibilità locale è in esecuzione come replica secondaria leggibile, il database è leggibile.  
  
 ** Le impostazioni dei criteri di failover per il gruppo di disponibilità si applicano a tutte le repliche, indipendentemente dal fatto che siano ospitate in un'istanza autonoma o in un'istanza del cluster di failover.  
  
> [!NOTE]  
>  Per altre informazioni sul **numero di nodi** all'interno di clustering di failover e **Gruppi di disponibilità Always On** per edizioni diverse di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>Considerazioni sull'hosting di una replica di disponibilità in un'istanza FCI  
  
> [!IMPORTANT]  
>  Se si intende ospitare una replica di disponibilità in un'istanza del cluster di failover di SQL Server (FCI), assicurarsi che i nodi host di Windows Server 2008 soddisfino i prerequisiti e le restrizioni di Always On per le istanze del cluster di failover (FCI). Per altre informazioni, vedere [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha istanze del cluster di failover che non supportano il failover automatico da gruppi di disponibilità, quindi le repliche di disponibilità ospitate da un'istanza del cluster di failover possono essere configurate solo per il failover manuale.  
  
 Potrebbe essere necessario configurare un cluster WSCF (Windows Server Failover Clustering) per includere i dischi condivisi che non sono disponibili in tutti i nodi. Ad esempio, si consideri un cluster WSFC in due data center con tre nodi. A due dei nodi è consentito ospitare un'istanza del clustering di failover di SQL Server (FCI) nel data center principale, nonché accedere agli stessi dischi condivisi. Al terzo nodo è permesso ospitare un'istanza autonoma di SQL Server in un data center diverso, ma non è consentito accedere ai dischi condivisi dal data center principale. Questa configurazione del cluster WSFC supporta la distribuzione di un gruppo di disponibilità se nell'istanza FCI è ospitata la replica primaria e in quella autonoma la replica secondaria.  
  
 Se si decide che in un'istanza FCI venga ospitata una replica di disponibilità per un determinato gruppo di disponibilità, assicurarsi che un failover dell'istanza FCI non possa comportare il tentativo da parte di un unico nodo WSFC di ospitare due repliche di disponibilità per lo stesso gruppo di disponibilità.  
  
 Nello scenario di esempio seguente si descrivono i potenziali problemi causati da questa configurazione:  
  
 Marcel configura un cluster WSFC con due nodi, `NODE01` e `NODE02`. Installa un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , `fciInstance1`, sia in `NODE01` sia in `NODE02` dove `NODE01` è il proprietario corrente di `fciInstance1`.  
 In `NODE02`Marcel installa un'altra istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], `Instance3`, che è un'istanza autonoma.  
 In `NODE01`Marcel abilita fciInstance1 per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. In `NODE02`abilita `Instance3` per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Successivamente configura un gruppo di disponibilità per il quale in `fciInstance1` è ospitata la replica primaria e in `Instance3` quella secondaria.  
 A un certo punto `fciInstance1` non è più disponibile in `NODE01`e il cluster WSFC comporta il failover di `fciInstance1` in `NODE02`. Dopo il failover, `fciInstance1` è un'istanza abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]in esecuzione nel ruolo primario di `NODE02`. Tuttavia, `Instance3` si trova ora nello stesso nodo WSFC di `fciInstance1`. Viene pertanto violato il vincolo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
 Per risolvere il problema presentato in questo scenario, l'istanza autonoma, `Instance3`, deve trovarsi in un altro nodo dello stesso cluster WSFC come per `NODE01` e `NODE02`.  
  
 Per altre informazioni sul [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , vedere [Istanze del cluster di failover Always On &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
##  <a name="FCMrestrictions"></a> Le restrizioni sull'utilizzo di Gestione cluster di failover WSFC con i gruppi di disponibilità  
 Non utilizzare Gestione cluster di failover per modificare i gruppi di disponibilità, ad esempio:  
  
-   Non aggiungere o rimuovere risorse nel servizio del cluster (gruppo di risorse) per il gruppo di disponibilità.  
  
-   Non modificare le proprietà del gruppo di disponibilità, ad esempio i possibili proprietari e i proprietari preferiti. Queste proprietà vengono impostate automaticamente dal gruppo di disponibilità.  
  
-   Non utilizzare Gestione cluster di failover per spostare i gruppi di disponibilità in altri nodi o per effettuarne il failover. Gestione cluster di failover non è in grado di rilevare lo stato di sincronizzazione delle repliche di disponibilità, pertanto possono verificarsi tempi di inattività prolungati. È necessario utilizzare [!INCLUDE[tsql](../../../includes/tsql-md.md)] o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Pagina relativa alla configurazione del clustering di failover di Windows per SQL Server (gruppo di disponibilità o FCI) con sicurezza limitata](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (Blog del team di SQL Server Always On: blog ufficiale del team di SQL Server Always On)](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **White paper:**  
  
     [Always On Architecture Guide: Building a High Availability and Disaster Recovery Solution by Using Failover Cluster Instances and Availability Groups (Guida all'architettura di Always On: compilazione di una soluzione a disponibilità elevata e di ripristino di emergenza usando istanze del cluster di failover e gruppi di disponibilità)](http://msdn.microsoft.com/library/jj215886.aspx)  
  
     [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza)](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Abilitare e disabilitare gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Istanze del cluster di failover Always On &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
