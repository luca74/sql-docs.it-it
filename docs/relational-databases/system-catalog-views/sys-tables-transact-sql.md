---
title: Sys. Tables (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- tables_TSQL
- sys.tables_TSQL
- sys.tables
- tables
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tables catalog view
ms.assetid: 8c42eba1-c19f-4045-ac82-b97a5e994090
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6b5b2c25c3391c23102e837437cf77c69c445e3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="systables-transact-sql"></a>sys.tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni tabella utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|\<colonne ereditate >||Per un elenco di colonne ereditate da questa vista, vedere [Sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|lob_data_space_id|**int**|Un valore diverso da zero corrisponde all'ID dello spazio dati (filegroup o schema di partizione) in cui sono inclusi dati LOB (large object binary) per la tabella. Esempi di tipi di dati LOB **varbinary (max)**, **varchar (max)**, **geography**, o **xml**.<br /><br /> 0 = nella tabella non sono presenti dati LOB.|  
|filestream_data_space_id|**int**|ID dello spazio dati per un filegroup FILESTREAM o schema di partizione costituito da filegroup FILESTREAM.<br /><br /> Per segnalare il nome di un filegroup FILESTREAM, eseguire la query `SELECT FILEGROUP_NAME (filestream_data_space_id) FROM sys.tables`.<br /><br /> È possibile aggiungere sys.tables alle viste seguenti in filestream_data_space_id = data_space_id.<br /><br /> -Sys. FileGroups<br /><br /> -Sys. partition_schemes<br /><br /> -Sys. Indexes<br /><br /> -Sys. allocation_units<br /><br /> -Sys. fulltext_catalogs<br /><br /> -data_spaces<br /><br /> -sys.destination_data_spaces<br /><br /> -Sys. master_files<br /><br /> -Sys. database_files<br /><br /> -backupfilegroup (join su filegroup_id)|  
|max_column_id_used|**int**|ID di colonna massimo utilizzato dalla tabella.|  
|lock_on_bulk_load|**bit**|La tabella è bloccata durante il caricamento bulk. Per altre informazioni, vedere [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|uses_ansi_nulls|**bit**|La tabella è stata creata con l'opzione di database SET ANSI_NULLS impostata su ON.|  
|is_replicated|**bit**|1 = La tabella è stata pubblicata tramite una replica snapshot o una replica transazionale.|  
|has_replication_filter|**bit**|1 = La tabella è associata a un filtro di replica.|  
|is_merge_published|**bit**|1 = La tabella è stata pubblicata tramite una replica di tipo merge.|  
|is_sync_tran_subscribed|**bit**|1 = La tabella è stata sottoscritta tramite una sottoscrizione ad aggiornamento immediato.|  
|has_unchecked_assembly_data|**bit**|1 = La tabella contiene dati persistenti che dipendono da un assembly la cui definizione è stata modificata durante l'ultima esecuzione di ALTER ASSEMBLY. Verrà reimpostato su 0 dopo la successiva esecuzione di DBCC CHECKDB o DBCC CHECKTABLE con esito positivo.|  
|text_in_row_limit|**int**|Numero minimo di byte consentito per il testo nella riga.<br /><br /> 0 = L'opzione Text in row non è impostata. Per altre informazioni, vedere [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|large_value_types_out_of_row|**bit**|1 = I tipi per valori di grandi dimensioni vengono archiviati esternamente alla riga. Per altre informazioni, vedere [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|  
|is_tracked_by_cdc|**bit**|1 = Per la tabella è abilitata l'acquisizione dei dati delle modifiche. Per ulteriori informazioni, vedere [sp_cdc_enable_table &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).|  
|lock_escalation|**tinyint**|Valore dell'opzione LOCK_ESCALATION per la tabella:<br /><br /> 0 = TABLE<br /><br /> 1 = DISABLE<br /><br /> 2 = AUTO|  
|lock_escalation_desc|**nvarchar(60)**|Descrizione di testo dell'opzione lock_escalation per la tabella. I valori possibili sono TABLE, AUTO e DISABLE.|  
|is_filetable|**bit**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> 1 = la tabella è una tabella FileTable.<br /><br /> Per ulteriori informazioni su tabelle Filetable, vedere [FileTables &#40; SQL Server &#41; ](../../relational-databases/blob/filetables-sql-server.md).|  
|durability|**tinyint**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Di seguito sono indicati i valori possibili:<br /><br /> 0 = SCHEMA_AND_DATA<br /><br /> 1 = SCHEMA_ONLY<br /><br /> Il valore predefinito è 0.|  
|durability_desc|**nvarchar(60)**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Di seguito sono indicati i valori possibili:<br /><br /> SCHEMA_ONLY<br /><br /> SCHEMA_AND_DATA<br /><br /> Il valore di SCHEMA_AND_DATA indica che la tabella è durevole e in memoria. SCHEMA_AND_DATA è il valore predefinito per le tabelle con ottimizzazione per la memoria. Il valore di SCHEMA_ONLY indica che i dati della tabella non verranno resi persistenti al riavvio del database con gli oggetti con ottimizzazione per la memoria.|  
|is_memory_optimized|**bit**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Di seguito sono indicati i valori possibili:<br /><br /> 0 = senza ottimizzazione per la memoria.<br /><br /> 1 = con ottimizzazione per la memoria.<br /><br /> Il valore predefinito è 0.<br /><br /> Le tabelle con ottimizzazione per la memoria sono tabelle utente in memoria, il cui schema è persistente su disco in modo analogo ad altre tabelle utente. È possibile accedere alle tabelle con ottimizzazione per la memoria da stored procedure compilate in modo nativo.|  
|temporal_type|**tinyint**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Il valore numerico che rappresenta il tipo di tabella:<br /><br /> 0 = NON_TEMPORAL_TABLE<br /><br /> 1 = HISTORY_TABLE<br /><br /> 2 = SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|temporal_type_desc|**nvarchar(60)**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> La descrizione del tipo di tabella:<br /><br /> NON_TEMPORAL_TABLE<br /><br /> HISTORY_TABLE<br /><br /> SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|history_table_id|**int**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].<br /><br /> Quando IN temporal_type (2, 4) restituisce object_id della tabella che conserva i dati cronologici, in caso contrario restituisce NULL.|  
|is_remote_data_archive_enabled|**bit**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e[!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]<br /><br /> Indica se la tabella è abilitata per l'estensione.<br /><br /> 0 = la tabella non è abilitata per l'estensione.<br /><br /> 1 = la tabella è abilitata per l'estensione.<br /><br /> Per ulteriori informazioni, vedere [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|is_external|**bit**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)], e [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)].<br /><br /> Indica la tabella è una tabella esterna.<br /><br /> 0 = la tabella non è una tabella esterna.<br /><br /> 1 = la tabella è una tabella esterna.| 
|history_retention_period|**int**|**Si applica a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>Il valore numerico che rappresenta la durata del periodo di memorizzazione cronologia temporale nelle unità specificate con history_retention_period_unit. |  
|history_retention_period_unit|**int**|**Si applica a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>Il valore numerico che rappresenta tipo di unità del periodo di memorizzazione cronologia temporale. <br /><br />-1: INFINITA <br /><br />3: GIORNO <br /><br />4: SETTIMANA <br /><br />5: MESE <br /><br />6: ANNO |  
|history_retention_period_unit_desc|**nvarchar (10)**|**Si applica a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>La descrizione del tipo di unità del periodo di memorizzazione cronologia temporale. <br /><br />INFINITE <br /><br />DAY <br /><br />WEEK <br /><br />MONTH <br /><br />YEAR |  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite tutte le tabelle utente che non dispongono di una chiave primaria.  
  
```  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
L'esempio seguente mostra i dati temporali correlati possono essere esposti.  
   
**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].
  
```  
SELECT T1.object_id, T1.name as TemporalTableName, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,  
T2.name as HistoryTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,  
T1.temporal_type_desc  
FROM sys.tables T1  
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id  
ORDER BY T1.temporal_type desc  
```  

Nell'esempio seguente viene illustrato come è possibile esporre informazioni sulla memorizzazione di cronologia temporale.  

**Si applica a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].  
  
```  
SELECT DB.is_temporal_history_retention_enabled, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema, 
T1.name as TemporalTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema, T2.name as HistoryTableName,
T1.history_retention_period, T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases where name = DB_NAME()) DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2 
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [L'esecuzione di query di catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
