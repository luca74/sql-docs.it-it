---
title: MSreplication_monitordata (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs: TSQL
helpviewer_keywords: MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bab9e68284c9c8acbbdd1211530edb5014950aa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationmonitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSreplication_monitordata** tabella contiene dati memorizzati nella cache utilizzati da Monitoraggio replica, con una riga per ogni sottoscrizione monitorata. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|Data e ora dell'ultimo aggiornamento dei dati di monitoraggio.|  
|**computeTime**|**int**|Tempo, espresso in secondi, necessario per calcolare i dati di monitoraggio.|  
|**publication_id**|**int**|ID della pubblicazione.|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_srvid**|**int**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**publication_type**|**int**|Tipo di pubblicazione. I possibili valori sono i seguenti.<br /><br /> **0** = pubblicazione transazionale<br /><br /> **1** = pubblicazione snapshot<br /><br /> **2** = pubblicazione di tipo merge|  
|**agent_type**|**int**|Tipo di agente di replica. I possibili valori sono i seguenti.<br /><br /> **1** = agente snapshot<br /><br /> **2** = agente di lettura log<br /><br /> **3** = agente di distribuzione<br /><br /> **4** = agente di merge<br /><br /> **9** = agente di lettura coda|  
|**agent_id**|**int**|ID dell'agente di replica.|  
|**agent_name**|**sysname**|Nome del processo dell'agente di replica.|  
|**job_id**|**uniqueidentifier**|GUID del processo dell'agente di replica.|  
|**status**|**int**|Stato dell'agente di replica. I possibili valori sono i seguenti.<br /><br /> **1** = avviato<br /><br /> **2** = ha avuto esito positivo<br /><br /> **3** = in corso<br /><br /> **4** = inattivo<br /><br /> **5** = nuovo tentativo in corso<br /><br /> **6** = non riuscito|  
|**isagentrunningnow**|**bit**|Un flag che indica se il processo dell'agente è attualmente in esecuzione, dove il valore **1** significa che il processo è in esecuzione.|  
|**avviso**|**int**|Avviso di soglia generato da una sottoscrizione, che può corrispondere al risultato dell'applicazione dell'operatore OR logico a uno o più dei valori seguenti.<br /><br /> **1** = expiration-una sottoscrizione di una pubblicazione transazionale ha superato il periodo di memorizzazione rispetto al valore soglia consentito, come percentuale del periodo di memorizzazione.<br /><br /> **2** = latency - il tempo necessario per replicare i dati da un server di pubblicazione transazionale al sottoscrittore supera la soglia, in secondi.<br /><br /> **4** = mergeexpiration - una sottoscrizione di una pubblicazione di tipo merge ha superato il periodo di memorizzazione rispetto al valore soglia consentito, come percentuale del periodo di memorizzazione. 8 = mergefastrunduration - è stata superata la soglia espressa in secondi relativa al tempo necessario per completare la sincronizzazione di una sottoscrizione di tipo merge tramite una connessione di rete veloce.<br /><br /> **16** = mergeslowrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, su una connessione di rete lenta o remota.<br /><br /> **32** = mergefastrunspeed – la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete veloce.<br /><br /> **64** = mergeslowrunspeed – la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete lenta o remota.|  
|**last_distsync**|**datetime**|Data e ora dell'ultima esecuzione dell'agente di distribuzione.|  
|**agentstoptime**|**datetime**|Data e ora di arresto dell'agente.|  
|**distdb**|**sysname**|Nome del database di distribuzione per la sottoscrizione.|  
|**conservazione**|**int**|Periodo di memorizzazione della pubblicazione.|  
|**time_stamp**|**datetime**|Solo per uso interno.|  
|**worst_latency**|**int**|Latenza più alta, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**best_latency**|**int**|Latenza più bassa, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**avg_latency**|**int**|Latenza media, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**cur_latency**|**int**|Latenza, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione durante l'esecuzione corrente.|  
|**worst_runspeedPerf**|**int**|Tempo di sincronizzazione più lungo per la pubblicazione di tipo merge.|  
|**best_runspeedPerf**|**int**|Tempo di sincronizzazione più breve per la pubblicazione di tipo merge.|  
|**average_runspeedPerf**|**int**|Media del tempo di sincronizzazione per la pubblicazione di tipo merge.|  
|**mergePerformance**|**int**|Prestazioni dell'ultima sincronizzazione confrontate con tutte le sincronizzazioni per la sottoscrizione, ottenute dividendo la velocità di recapito dell'ultima sincronizzazione per la media di tutte le velocità di recapito precedenti.|  
|**mergelatestsessionrunduration**|**int**|Durata dell'esecuzione più recente dell'agente di merge.|  
|**mergelatestsessionrunspeed**|**float(53)**|Frequenza di recapito dell'esecuzione più recente dell'agente di merge.|  
|**mergelatestsessionconnectiontype**|**int**|Connessione utilizzata per la sessione più recente dell'agente di merge. I possibili valori sono i seguenti.<br /><br /> **1** = rete locale (LAN)<br /><br /> **2** = connessione remota|  
|**retention_period_unit**|**tinyint**|Definisce l'unità utilizzata per la definizione dell'opzione retention. I possibili valori sono i seguenti.<br /><br /> **1** = Settimana<br /><br /> **2** = Mese<br /><br /> **3** = Anno|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio a livello di programmazione della replica](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  