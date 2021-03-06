---
title: Ripristino da backup archiviati in Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 48c5dccb0f90048123c15b637374b358097a16de
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="restoring-from-backups-stored-in-microsoft-azure"></a>Ripristino da backup archiviati in Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento illustra le considerazioni relative al ripristino di un database tramite un backup archiviato nel servizio di archiviazione BLOB di Microsoft Azure. Ciò si applica ai backup creati tramite il backup di SQL Server nell'URL o tramite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Si consiglia di esaminare questo argomento se si dispone di backup archiviati nel servizio di archiviazione BLOB di Windows Azure che si intende ripristinare, nonché di rivedere gli argomenti in cui vengono descritti i passaggi per ripristinare un database che sono uguali sia per i backup in locale sia per quelli di Azure.  
  
## <a name="overview"></a>Panoramica  
 Gli strumenti e i metodi utilizzati per ripristinare un database da un backup in locale si applicano al ripristino di un database da un backup nel cloud.  Nelle sezioni seguenti vengono descritte queste considerazioni e tutte le differenze di cui essere a conoscenza relativamente ai casi in cui si utilizzano backup archiviati nel servizio di archiviazione BLOB di Windows Azure.  
  
### <a name="using-transact-sql"></a>Utilizzo di Transact-SQL  
  
-   Poiché SQL Server deve essere connesso a un'origine esterna per il recupero dei file di backup, vengono utilizzate le credenziali SQL per autenticare l'account di archiviazione. Di conseguenza, per l'istruzione RESTORE è richiesta l'opzione WITH CREDENTIAL. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
-   Se si usa [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] per gestire i backup nel cloud, è possibile verificare tutti i backup disponibili nell'archiviazione usando la funzione di sistema **smart_admin.fn_available_backups** . Tramite questa funzione di sistema vengono restituiti tutti i backup disponibili per un database in una tabella. Poiché i risultati vengono restituiti in una tabella, è possibile filtrarli oppure ordinarli. Per altre informazioni, vedere [managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md).  
  
### <a name="using-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio  
  
-   L'attività di ripristino viene utilizzata per ripristinare un database tramite SQL Server Management Studio. Nella pagina dei supporti di backup è ora disponibile l'opzione **URL** per visualizzare i file di backup archiviati nel servizio di archiviazione BLOB di Windows Azure. Inoltre, è necessario fornire le credenziali SQL utilizzate per autenticare l'account di archiviazione. La griglia **Set di backup da ripristinare** viene popolata successivamente con i backup disponibili nell'archiviazione BLOB di Windows Azure. Per altre informazioni, vedere [Restoring from Windows Azure storage Using SQL Server Management Studio](../../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
### <a name="optimizing-restores"></a>Ottimizzazione dei ripristini  
 Per ridurre il tempo di scrittura di un'operazione di ripristino, aggiungere il diritto utente **Esecuzione attività di manutenzione volume** all'account utente di SQL Server. Per ulteriori informazioni, vedere [Inizializzazione di file di database](http://go.microsoft.com/fwlink/?LinkId=271622). Se l'operazione di ripristino è ancora lenta con l'inizializzazione immediata dei file abilitata, esaminare le dimensioni del file di log nell'istanza in cui è stato eseguito il backup del database. Se le dimensioni del log sono molto grandi (più GB), si prevede un ripristino lento. Durante l'operazione di ripristino il file di log deve essere azzerato; questa operazione richiede una quantità di tempo significativa.  
  
 Per ridurre i tempi di ripristino è consigliabile usare backup compressi.  Per i backup con dimensioni superiori ai 25 GB, usare l' [utilità AzCopy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) per eseguire il download nell'unità locale e quindi eseguire il ripristino. Per altri suggerimenti e procedure consigliate sui backup, vedere [SQL Server Backup to URL Best Practices and Troubleshooting](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md).  
  
 È inoltre possibile abilitare il flag di traccia 3051 quando si esegue il ripristino per generare un log dettagliato. Questo file di log viene inserito nella directory del log e viene denominato con il formato: BackupToUrl-\<nomeistanza>-\<nomedb>-azione-\<PID>.log. Nel file di log sono incluse informazioni su ogni round trip al Servizio di archiviazione Windows Azure, incluso l'intervallo che può essere utile per individuare il problema.  
  
### <a name="topics-on-performing-restore-operations"></a>Argomenti sull'esecuzione delle operazioni di ripristino  
  
-   [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
-   [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
-   [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
-   [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
