---
title: sp_add_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c83d0a0062f7f7affc19e91b929bb16831a8946d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="spaddlogshippingsecondaryprimary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta le informazioni primarie, aggiunge collegamenti di monitoraggio locale e remoto e crea processi di copia e di ripristino nel server secondario per il database primario specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@primary_server** = ] '*primary_server*'  
 Il nome dell'istanza primaria del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nella configurazione di log shipping. *primary_server* è **sysname** e non può essere NULL.  
  
 [  **@primary_database**  =] '*primary_database*'  
 Nome del database sul server primario. *primary_database* è **sysname**, non prevede alcun valore predefinito.  
  
 [ **@backup_source_directory** = ] '*backup_source_directory*'  
 Directory in cui vengono archiviati i file di backup del log delle transazioni dal server primario. *backup_source_directory* è **nvarchar (500)** e non può essere NULL.  
  
 [  **@backup_destination_directory**  =] '*backup_destination_directory*'  
 Directory nel server secondario in cui vengono copiati i file di backup. *backup_destination_directory* è **nvarchar (500)** e non può essere NULL.  
  
 [ **@copy_job_name** = ] '*copy_job_name*'  
 Nome da utilizzare per il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent creato per copiare i backup del log delle transazioni nel server secondario. *copy_job_name* è **sysname** e non può essere NULL.  
  
 [ **@restore_job_name** = ] '*restore_job_name*'  
 È il nome del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente nel server secondario che ripristina i backup del database secondario. *restore_job_name* è **sysname** e non può essere NULL.  
  
 [  **@file_retention_period**  =] '*file_retention_period*'  
 Il periodo di tempo, espresso in minuti, che viene mantenuto un file di backup nel server secondario nel percorso specificato per il @backup_destination_directory parametro prima di essere eliminati. *history_retention_period* è **int**, con un valore predefinito è NULL. Se non si specifica un valore, verrà utilizzato il valore 14420.  
  
 [ **@monitor_server** = ] '*monitor_server*'  
 Nome del server di monitoraggio. *Monitor_server* è **sysname**, senza impostazione predefinita e non può essere NULL.  
  
 [ **@monitor_server_security_mode** = ] '*monitor_server_security_mode*'  
 Modalità di sicurezza utilizzata per connettersi al server di monitoraggio.  
  
 1 = Autenticazione di Windows.  
  
 0 = Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *monitor_server_security_mode* è **bit** e non può essere NULL.  
  
 [ **@monitor_server_login** = ] '*monitor_server_login*'  
 Nome utente dell'account utilizzato per accedere al server di monitoraggio.  
  
 [ **@monitor_server_password** = ] '*monitor_server_password*'  
 Password dell'account utilizzato per accedere al server di monitoraggio.  
  
 [ **@copy_job_id** = ] '*copy_job_id*' OUTPUT  
 ID associato al processo di copia nel server secondario. *copy_job_id* è **uniqueidentifier** e non può essere NULL.  
  
 [ **@restore_job_id** = ] '*restore_job_id*' OUTPUT  
 ID associato al processo di ripristino nel server secondario. *restore_job_id* è **uniqueidentifier** e non può essere NULL.  
  
 [  **@secondary_id**  =] '*secondary_id*' OUTPUT  
 ID del server secondario nella configurazione per il log shipping. *secondary_id* è **uniqueidentifier** e non può essere NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuno  
  
## <a name="remarks"></a>Osservazioni  
 **sp_add_log_shipping_secondary_primary** deve essere eseguita la **master** database nel server secondario. Questa stored procedure esegue le operazioni seguenti:  
  
1.  Genera un ID secondario per il server e il database primari specificati.  
  
2.  Esegue le operazioni seguenti:  
  
    1.  Aggiunge una voce per l'ID secondario in **log_shipping_secondary** utilizzando gli argomenti specificati.  
  
    2.  Crea un processo di copia per l'ID secondario disabilitato.  
  
    3.  Imposta l'ID di processo di copia di **log_shipping_secondary** voce per l'ID di processo del processo di copia.  
  
    4.  Crea un processo di ripristino per l'ID secondario disabilitato.  
  
    5.  Impostare l'ID di processo di ripristino nel **log_shipping_secondary** voce per l'ID di processo del processo di ripristino.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire questa procedura.  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene illustrato l'utilizzo di **sp_add_log_shipping_secondary_primary** stored procedure per impostare le informazioni per il database primario [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nel server secondario.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul Log Shipping &#40; SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
