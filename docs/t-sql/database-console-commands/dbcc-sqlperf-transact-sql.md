---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/07/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: cd615cd56860138d2e9afa7e2d7090ed27ba8e3a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Fornisce statistiche relative all'utilizzo dello spazio nel log delle transazioni per tutti i database. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può anche essere usata per reimpostare le statistiche relative a latch e attese.
  
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([anteprima in alcune aree](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
LOGSPACE  
Restituisce la dimensione corrente del log delle transazioni e la percentuale di spazio del log utilizzata per ogni database. Usare queste informazioni per monitorare la quantità di spazio usato in un log delle transazioni.

> [!IMPORTANT]
> Per altre informazioni sui dati di uso dello spazio per il log delle transazioni a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vedere la sezione [Osservazioni](#Remarks) in questo argomento.
  
**"sys.dm_os_latch_stats"**, CLEAR  
Reimposta le statistiche relative ai latch. Per altre informazioni, vedere [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Questa opzione non è disponibile in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**"sys.dm_os_wait_stats"**, CLEAR  
Reimposta le statistiche relative alle attese. Per altre informazioni, vedere [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Questa opzione non è disponibile in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
WITH NO_INFOMSGS  
Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
## <a name="result-sets"></a>Set di risultati  
 Nella tabella seguente vengono descritte le colonne del set di risultati.  
  
|Nome colonna|Definizione|  
|---|---|
|**Database Name**|Nome del database a cui si riferiscono le statistiche del log visualizzate.|  
|**Log Size (MB)**|Dimensione corrente allocata al log. Questo valore è sempre inferiore rispetto alla quantità di spazio allocata inizialmente per il log in quanto [!INCLUDE[ssDE](../../includes/ssde-md.md)] riserva una piccola quantità di spazio su disco per informazioni di intestazione interne.|  
|**Log Space Used (%)**|Percentuale del file di log attualmente usata per archiviare informazioni del log delle transazioni.|  
|**Stato**|Stato del file di log. Sempre 0.|  
  
## <a name="Remarks"></a> Osservazioni  
A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usare la DMV [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) anziché `DBCC SQLPERF(LOGSPACE)` per restituire informazioni sull'uso dello spazio per il log transazioni di ogni database.    
 
Nel log delle transazioni viene registrata ogni transazione eseguita in un database. Per altre informazioni, vedere [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) e [Guida sull'architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).
  
## <a name="permissions"></a>Autorizzazioni  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire `DBCC SQLPERF(LOGSPACE)` è richiesta l'autorizzazione `VIEW SERVER STATE` nel server. Per reimpostare le statistiche relative a latch e attese è richiesta l'autorizzazione `ALTER SERVER STATE` per il server.
  
Nei livelli Premium di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesta l'autorizzazione `VIEW DATABASE STATE` nel database. Nei livelli Basic e Standard di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesto l'account amministratore di [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Le statistiche di reimpostazione di latch e attese non sono supportate.
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Visualizzazione delle informazioni relative allo spazio del log per tutti i database  
Nell'esempio seguente vengono visualizzate le informazioni relative a `LOGSPACE` per tutti i database inclusi nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. Reimpostazione delle statistiche relative alle attese  
Nell'esempio seguente vengono reimpostate le statistiche relative alle attese per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

