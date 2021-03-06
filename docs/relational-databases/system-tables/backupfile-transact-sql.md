---
title: backupfile (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84b26ca09b8cd537ed40f0af8844f3f0c7627c86
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni file di dati o di log di un database. Le colonne descrivono la configurazione dei file al momento dell'esecuzione del backup. Se il file è incluso nel backup è determinato dal **is_present** colonna. Questa tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Numero di identificazione univoco del file che include il set di backup. Riferimenti **backupset (backup_set_id)**.|  
|**first_family_number**|**tinyint**|Numero di gruppo del primo supporto che include il file di backup. Può essere NULL.|  
|**first_media_number**|**smallint**|Numero del primo supporto che include il file di backup. Può essere NULL.|  
|**filegroup_name**|**nvarchar(128)**|Nome del filegroup che include un file di database di backup. Può essere NULL.|  
|**page_size**|**int**|Dimensioni della pagina in byte.|  
|**file_number**|**Numeric(10,0)**|Numero di identificazione del file univoco all'interno di un database (corrisponde a **Sys. database_files**. **file_id**).|  
|**backed_up_page_count**|**Numeric(10,0)**|Numero di pagine di cui è stato eseguito il backup. Può essere NULL.|  
|**file_type**|**char(1)**|File di cui è stato eseguito il backup. I valori possibili sono:<br /><br /> D = file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> L = file di log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> F = catalogo full-text.<br /><br /> Può essere NULL.|  
|**source_file_block_size**|**Numeric(10,0)**|Dispositivo in cui si trova il file di dati o di log originale quando viene eseguito il backup. Può essere NULL.|  
|**file_size**|**Numeric(20,0)**|Lunghezza in byte del file di cui è stato eseguito il backup. Può essere NULL.|  
|**logical_name**|**nvarchar(128)**|Nome logico del file di cui è stato eseguito il backup. Può essere NULL.|  
|**physical_drive**|**nvarchar(260)**|Nome di dispositivo fisico o partizione. Può essere NULL.|  
|**physical_name**|**nvarchar(260)**|Parte rimanente del nome fisico del file (sistema operativo). Può essere NULL.|  
|**state**|**tinyint**|Stato del file. I valori possibili sono:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY PENDING<br /><br /> 4 = SUSPECT<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = ELIMINATO<br /><br /> Nota: Il valore 5 viene ignorato in modo che questi valori corrispondono ai valori per gli stati del database.|  
|**state_desc**|**nvarchar(64)**|Descrizione del file. I valori possibili sono:<br /><br /> ONLINE RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale il file è stato creato.|  
|**drop_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale il file è stato eliminato. Può essere NULL.<br /><br /> Se il file non è stato eliminato, questo valore è NULL.|  
|**file_guid**|**uniqueidentifier**|Identificatore univoco del file.|  
|**read_only_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale la modalità del filegroup contenente il file è passata da lettura/scrittura a sola lettura (la modifica più recente). Può essere NULL.|  
|**read_write_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale la modalità del filegroup contenente il file è passata da sola lettura a lettura/scrittura (la modifica più recente). Può essere NULL.|  
|**differential_base_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log (LSN) di base per i backup differenziali. Un backup differenziale include solo gli extent dati con una sequenza del log del numero maggiore o uguale a **differential_base_lsn**.<br /><br /> Per gli altri tipi di backup il valore è NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Per un backup differenziale, identificatore univoco del backup di dati più recente che costituisce la base differenziale del file. Se il valore è NULL, il file è stato incluso nel backup differenziale ma è stato aggiunto dopo la creazione della base.<br /><br /> Per gli altri tipi di backup il valore è NULL.|  
|**backup_size**|**Numeric(20,0)**|Dimensioni in byte del backup di questo file.|  
|**filegroup_guid**|**uniqueidentifier**|ID del filegroup. Per individuare informazioni sui filegroup nella tabella backupfilegroup, utilizzare **filegroup_guid** con **backup_set_id**.|  
|**is_readonly**|**bit**|1 = il file è di sola lettura.|  
|**is_present**|**bit**|1 = il file è incluso nel set di backup.|  
  
## <a name="remarks"></a>Osservazioni  
 RESTORE VERIFYONLY FROM *dispositivo_backup* WITH LOADHISTORY popola le colonne di **backupmediaset** tabella con i valori appropriati dall'intestazione del set di supporti.  
  
 Per ridurre il numero di righe in questa tabella e in altre tabelle di cronologia e di backup, eseguire il [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
