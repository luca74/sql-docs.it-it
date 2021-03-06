---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f9accc8ae7ffb64d82fa10c3b60a2f8fec44b8a
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/10/2018
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui processi di agente che generano snapshot dei dati filtrati. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication =** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutti i processi di snapshot dei dati filtrati che corrispondono alla stringa *dynamic_ snapshot_jobid*e *dynamic_snapshot_jobname*per tutte le pubblicazioni.  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 Nome del processo di snapshot dei dati filtrati. *dynamic_snapshot_jobname*viene **sysname**, con valore predefinito è **%**', che restituisce tutti i processi dinamici per una pubblicazione con l'oggetto specificato *dynamic_ snapshot_jobid*. Se quando è stato creato il processo non è stato specificato in modo esplicito un nome di processo, il nome del processo verrà indicato nel formato seguente:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 Identificatore di un processo di snapshot dei dati filtrati. *dynamic_snapshot_jobid*viene **uniqueidentifier**, con valore predefinito è NULL, che restituisce tutti i processi di snapshot che corrispondono alla stringa *dynamic_snapshot_jobname*.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica il processo di snapshot dei dati filtrati.|  
|**job_name**|**sysname**|Nome del processo di snapshot dei dati filtrati.|  
|**job_id**|**uniqueidentifier**|Identifica la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente nel server di distribuzione.|  
|**dynamic_filter_login**|**sysname**|Valore utilizzato per valutare il [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) funzione in un filtro di riga con parametri definito per la pubblicazione.|  
|**dynamic_filter_hostname**|**sysname**|Valore utilizzato per valutare il [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) funzione in un filtro di riga con parametri definito per la pubblicazione.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Percorso della cartella da cui i file di snapshot vengono letti se viene utilizzato un filtro di riga con parametri.|  
|**frequency_type**|**int**|Frequenza pianificata per l'esecuzione dell'agente. I possibile valori sono i seguenti.<br /><br /> **1** = una sola volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa<br /><br /> **64** = avvio automatico<br /><br /> **128** = periodica|  
|**frequency_interval**|**int**|Giorni in cui l'agente viene eseguito. I possibili valori sono i seguenti.<br /><br /> **1** = domenica<br /><br /> **2** = lunedì<br /><br /> **3** = martedì<br /><br /> **4** = Wednesday<br /><br /> **5** = Thursday<br /><br /> **6** = venerdì<br /><br /> **7** = sabato<br /><br /> **8** = Day<br /><br /> **9** = giorni feriali<br /><br /> **10** = giorni festivi|  
|**frequency_subday_type**|**int**|È il tipo che definisce la frequenza con cui viene eseguita quando l'agente *frequency_type* è **4** (giornaliero), i possibili valori sono i seguenti.<br /><br /> **1** = all'ora specificata<br /><br /> **2** = secondi<br /><br /> **4** = minuti<br /><br /> **8** = ore|  
|**frequency_subday_interval**|**int**|Numero di intervalli di *frequency_subday_type* che si verificano tra esecuzioni pianificate dell'agente.|  
|**frequency_relative_interval**|**int**|Settimana in cui viene eseguito l'agente in un determinato mese quando *frequency_type* è **32** (mensile relativo), i possibili valori sono i seguenti.<br /><br /> **1** = primo<br /><br /> **2** = secondi<br /><br /> **4** = terzo<br /><br /> **8** = quarto<br /><br /> **16** = ultimo|  
|**frequency_recurrence_factor**|**int**|Numero di settimane o mesi tra le esecuzioni pianificate dell'agente.|  
|**active_start_date**|**int**|Data della prima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_end_date**|**int**|Data dell'ultima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_start_time**|**int**|Ora della prima esecuzione pianificata dell'agente nel formato HHMMSS.|  
|**active_end_time**|**int**|Ora dell'ultima esecuzione pianificata dell'agente nel formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpdynamicsnapshot_job** viene utilizzata nella replica di tipo merge.  
  
 Se vengono utilizzati tutti i valori predefiniti dei parametri, verranno restituite informazioni su tutti i processi di snapshot dei dati partizionati per l'intero database di pubblicazione.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** predefinito del database e l'elenco di accesso per la pubblicazione può eseguire **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
