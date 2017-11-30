---
title: exec_trigger_stats (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce dati statistici aggregati sulle prestazioni dei trigger memorizzati nella cache. La vista contiene una riga per ogni trigger e la durata della riga è uguale al periodo in cui il trigger rimane memorizzato nella cache. Quando un trigger viene rimosso dalla cache, le righe corrispondenti vengono eliminate dalla vista. In quel momento, viene generato un evento di traccia di SQL di Performance Statistics simile a **Sys.dm exec_query_stats**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database in cui è contenuto il trigger.|  
|**object_id**|**int**|Numero di identificazione del trigger.|  
|**tipo**|**Char(2)**|Tipo dell'oggetto:<br /><br /> TA = Trigger di assembly (CLR)<br /><br /> TR = trigger SQL|  
|**Type_desc**|**nvarchar(60)**|Descrizione del tipo di oggetto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**valore di sql_handle**|**varbinary(64)**|Può essere utilizzato per correlare le query in **Sys.dm exec_query_stats** eseguite dall'interno del trigger.|  
|**plan_handle**|**varbinary(64)**|Identificatore del piano in memoria. Si tratta di un identificatore temporaneo, che rimane costante solo se il piano rimane nella cache. Questo valore può essere utilizzato con il **Sys.dm exec_cached_plans** vista a gestione dinamica.|  
|**cached_time**|**datetime**|Ora in cui il trigger è stato aggiunto alla cache.|  
|**last_execution_time**|**datetime**|Ora dell'ultima esecuzione del trigger.|  
|**execution_count**|**bigint**|Numero di esecuzioni del trigger a partire dall'ultima compilazione.|  
|**total_worker_time**|**bigint**|Quantità totale di tempo CPU, in microsecondi, utilizzato dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_worker_time**|**bigint**|Tempo di CPU, in microsecondi, utilizzato durante l'ultima esecuzione del trigger.|  
|**min_worker_time**|**bigint**|Tempo massimo di CPU, in microsecondi, utilizzato dal trigger durante una singola esecuzione.|  
|**max_worker_time**|**bigint**|Tempo massimo di CPU, in microsecondi, utilizzato dal trigger durante una singola esecuzione.|  
|**total_physical_reads**|**bigint**|Numero totale di letture fisiche effettuate dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_physical_reads**|**bigint**|Numero di letture fisiche eseguite durante l'ultima esecuzione del trigger.|  
|**min_physical_reads**|**bigint**|Numero minimo di letture fisiche effettuate dal trigger durante una singola esecuzione.|  
|**max_physical_reads**|**bigint**|Numero massimo di letture fisiche effettuate dal trigger durante una singola esecuzione.|  
|**total_logical_writes**|**bigint**|Numero totale di letture logiche effettuate dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_logical_writes**|**bigint**|**total_physical_reads**numero di scritture logiche eseguite durante l'ultima esecuzione del trigger.|  
|**min_logical_writes**|**bigint**|Numero minimo di scritture logiche effettuate dal trigger durante una singola esecuzione.|  
|**max_logical_writes**|**bigint**|Numero massimo di scritture logiche effettuate dal trigger durante una singola esecuzione.|  
|**total_logical_reads**|**bigint**|Numero totale di scritture logiche effettuate dalle esecuzioni del trigger a partire dalla relativa compilazione.|  
|**last_logical_reads**|**bigint**|Numero di letture logiche eseguite durante l'ultima esecuzione del trigger.|  
|**min_logical_reads**|**bigint**|Numero minimo di letture logiche effettuate dal trigger durante una singola esecuzione.|  
|**max_logical_reads**|**bigint**|Numero massimo di letture logiche effettuate dal trigger durante una singola esecuzione.|  
|**total_elapsed_time**|**bigint**|Tempo totale trascorso, in microsecondi, per le esecuzioni complete del trigger.|  
|**last_elapsed_time**|**bigint**|Tempo trascorso, in microsecondi, per l'ultima esecuzione completata del trigger.|  
|**min_elapsed_time**|**bigint**|Tempo minimo trascorso, in microsecondi, per qualsiasi esecuzione completata del trigger.|  
|**max_elapsed_time**|**bigint**|Tempo massimo trascorso, in microsecondi, per qualsiasi esecuzione completata del trigger.|  
  
## <a name="remarks"></a>Osservazioni  
 Nel database SQL di Windows Azure, le viste a gestione dinamica non possono esporre le informazioni che influenzerebbero l'indipendenza del database o le informazioni sugli altri database a cui l'utente dispone di accesso. Per evitare di esporre queste informazioni, ogni riga che contiene dati che non appartengono al tenant connesso viene esclusa tramite filtro.  

Le statistiche nella vista vengono aggiornate quando viene completata una query.  
  
## <a name="permissions"></a>Permissions  
In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione per il database. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Standard e Basic, è necessario il **amministratore del Server** o **amministratore di Azure Active Directory** account.
  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sui primi cinque trigger identificati in base al tempo medio trascorso.  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40; relative all'esecuzione Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys.dm exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [Sys.dm exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [Sys.dm exec_procedure_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [Sys.dm exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  