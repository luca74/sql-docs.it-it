---
title: sys.dm_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ebecbd762d9c689d5564772c377001d69a1941b2
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosthreads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce un elenco di tutti i thread del sistema operativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Per chiamare questo metodo dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_os_threads**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|Indirizzo di memoria (chiave primaria) del thread.|  
|started_by_sqlservr|**bit**|Indica l'initiator del thread.<br /><br /> 1 = Il thread è stato avviato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Il thread è stato avviato da un altro componente, ad esempio una stored procedure estesa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**int**|ID del thread assegnato dal sistema operativo.|  
|status|**int**|Flag di stato interno.|  
|instruction_address|**varbinary(8)**|Indirizzo dell'istruzione attualmente in esecuzione.|  
|creation_time|**datetime**|Ora di creazione del thread.|  
|kernel_time|**bigint**|Quantità di tempo del kernel utilizzato dal thread.|  
|usermode_time|**bigint**|Quantità di tempo utente utilizzato dal thread.|  
|stack_base_address|**varbinary(8)**|Indirizzo di memoria dell'indirizzo dello stack più alto per il thread.|  
|stack_end_address|**varbinary(8)**|Indirizzo di memoria dell'indirizzo dello stack più basso per il thread.|  
|stack_bytes_committed|**int**|Numero di byte di cui è stato eseguito il commit nello stack.|  
|stack_bytes_used|**int**|Numero di byte attivamente utilizzati nel thread.|  
|affinity|**bigint**|Maschera della CPU nella quale il thread è in esecuzione. Questo dipende dal valore configurato per il **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY** istruzione. Potrebbe essere diverso dall'utilità di pianificazione in caso di affinità soft.|  
|Priorità|**int**|Valore di priorità del thread.|  
|Impostazioni locali|**int**|Identificatore delle impostazioni locali (LCID) nella cache per il thread.|  
|Token|**varbinary(8)**|Handle del token di rappresentazione nella cache per il thread.|  
|is_impersonating|**int**|Indica se il thread utilizza la rappresentazione Win32.<br /><br /> 1 = Il thread utilizza credenziali di sicurezza diverse da quelle predefinite del processo. Ciò indica che il thread rappresenta un'entità diversa da quella che ha creato il processo.|  
|is_waiting_on_loader_lock|**int**|Stato del sistema operativo indicante se il thread è in attesa di un blocco del caricatore.|  
|fiber_data|**varbinary(8)**|Fiber Win32 corrente in esecuzione nel thread. È applicabile solo in caso di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il lightweight pooling.|  
|thread_handle|**varbinary(8)**|Solo per uso interno.|  
|event_handle|**varbinary(8)**|Solo per uso interno.|  
|scheduler_address|**varbinary(8)**|Indirizzo di memoria dell'utilità di pianificazione associata al thread. Per altre informazioni, vedere [DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary(8)**|Indirizzo di memoria del thread di lavoro associato al thread. Per altre informazioni, vedere [DM os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary(8)**|Indirizzo del contesto interno del fiber. È applicabile solo in caso di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il lightweight pooling.|  
|self_address|**varbinary(8)**|Puntatore di consistenza interno.|  
|processor_group|**smallint**|**Si applica a**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID del gruppo di processori.|  
|pdw_node_id|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo che utilizza questo tipo di distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], richiede il `VIEW DATABASE STATE` autorizzazione per il database.   

## <a name="examples"></a>Esempi  
 All'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono avviati dei thread a cui vengono associati thread di lavoro. Componenti esterni, ad esempio una stored procedure estesa, possono tuttavia avviare thread nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di controllo su questi thread. Sys.dm os_threads può offrire informazioni sui thread non autorizzati che utilizzano risorse nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo.  
  
 La query seguente consente di individuare i thread di lavoro che eseguono thread non avviati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], con il tempo utilizzato per l'esecuzione.  
  
> [!NOTE]  
>  A scopo di brevità, nell'istruzione `*` della query seguente viene utilizzato un asterisco (`SELECT`). È consigliabile evitare di utilizzare l'asterisco (*), in particolare per viste del catalogo, viste a gestione dinamica e funzioni di sistema con valori di tabella. Gli aggiornamenti futuri e le versioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe aggiungere colonne e modificare l'ordine delle colonne in queste viste e funzioni. Queste modifiche potrebbero causare malfunzionamenti nelle applicazioni che prevedono un ordine e un numero di colonne specifici.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Vedere anche  
  [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


