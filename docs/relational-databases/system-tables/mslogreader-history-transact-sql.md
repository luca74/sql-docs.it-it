---
title: MSlogreader_history (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 191f696f65d744b66d2aa41b8841c24097bf6434
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mslogreaderhistory-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSlogreader_history** tabella contiene righe di cronologia per gli agenti di lettura Log associati al server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente di lettura log.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> 1 = In fase di avvio.<br /><br /> 2 = Esito positivo.<br /><br /> 3 = Operazione in corso.<br /><br /> 4 = Inattivo.<br /><br /> 5 = Nuovo tentativo.<br /><br /> 6 = Esito negativo.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**time**|**datetime**|Ora di registrazione del messaggio.|  
|**duration**|**int**|Durata espressa in secondi della sessione del messaggio.|  
|**commenti**|**nvarchar(255)**|Testo del messaggio.|  
|**xact_seqno**|**varbinary (16)**|Numero di sequenza dell'ultima transazione elaborata.|  
|**delivery_time**|**int**|Ora in cui è stata recapitata la prima transazione.|  
|**delivered_transactions**|**int**|Numero totale di transazioni recapitate durante la sessione.|  
|**delivered_commands**|**int**|Numero totale di comandi recapitati durante la sessione.|  
|**average_commands**|**int**|Numero medio di comandi recapitati durante la sessione.|  
|**delivery_rate**|**float**|Numero medio dei comandi recapitati al secondo.|  
|**delivery_latency**|**int**|Latenza tra l'immissione del commando nel database pubblicato e l'immissione del comando nel database di distribuzione. In millisecondi.|  
|**error_id**|**int**|L'ID dell'errore nella **MSrepl_error** tabella di sistema.|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
|**updateable_row**|**bit**|Impostare su **1** se la riga di cronologia può essere sovrascritto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
