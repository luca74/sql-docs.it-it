---
title: Sys.dm broker_forwarded_messages (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c7292ca6344c7492da82c3d65ff4003f23f95f1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni messaggio di Service Broker che un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta per inoltrare.  
  

|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|ID della conversazione a cui appartiene il messaggio. Ammette valori Null.|  
|**is_initiator**|**bit**|Indica se il messaggio proviene dall'initiator della conversazione.  Ammette valori Null.<br /><br /> 0 = Non proveniente dall'initiator<br /><br /> 1 = Proveniente dall'initiator|  
|**to_service_name**|**nvarchar(512)**|Nome del servizio a cui viene inviato il messaggio. Ammette valori Null.|  
|**to_broker_instance**|**nvarchar(512)**|Identificatore del broker che ospita il servizio a cui viene inviato il messaggio. Ammette valori Null.|  
|**from_service_name**|**nvarchar(512)**|Nome del servizio da cui proviene il messaggio. Ammette valori Null.|  
|**from_broker_instance**|**nvarchar(512)**|Identificatore del broker che ospita il servizio da cui proviene il messaggio. Ammette valori Null.|  
|**adjacent_broker_address**|**nvarchar(512)**|Indirizzo di rete a cui viene inviato il messaggio. Ammette valori Null.|  
|**message_sequence_number**|**bigint**|Numero di sequenza del messaggio nella finestra del dialogo. Ammette valori Null.|  
|**message_fragment_number**|**int**|Se il messaggio di dialogo è frammentato, indica il numero di frammento contenuto nel messaggio di trasporto. Ammette valori Null.|  
|**hops_remaining**|**tinyint**|Numero di volte che il messaggio può essere ritrasmesso prima di raggiungere la destinazione finale. Ogni volta che il messaggio viene inoltrato, il numero viene ridotto di un'unità. Ammette valori Null.|  
|**valore time_to_live**|**int**|Tempo massimo durante il quale il messaggio può rimanere attivo. Se questo valore raggiunge 0, il messaggio viene eliminato. Ammette valori Null.|  
|**time_consumed**|**int**|Tempo durante il quale il messaggio è stato attivo. Ogni volta che il messaggio viene inoltrato, questo numero viene aumentato in base al tempo impiegato per l'inoltro del messaggio. Non ammette i valori Null.|  
|**message_id**|**uniqueidentifier**|ID del messaggio. Ammette valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative a Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  
