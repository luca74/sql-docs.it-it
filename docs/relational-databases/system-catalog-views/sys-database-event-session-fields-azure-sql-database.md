---
title: Sys.database_event_session_fields (Database SQL di Azure) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16d550e1a453b921eb0768ab758557192e9f0e16
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseeventsessionfields-azure-sql-database"></a>Sys.database_event_session_fields (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni colonna personalizzabile che è impostata in modo esplicito su eventi e destinazioni.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|object_id|**int**|ID dell'oggetto a cui è associato il campo. Non ammette i valori Null.|  
|name|**sysname**|Nome del campo. Non ammette i valori Null.|  
|Valore|**sql_variant**|Valore del campo. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il server.  
  
## <a name="remarks"></a>Osservazioni  
 Questa vista ha le cardinalità della relazione seguenti.  
  
||||  
|-|-|-|  
|From|Per|Relazione|  
|Sys.database_event_session_actions.event_session_id|Sys.database_event_sessions.event_session_id|Molti-a-uno|  
|Sys.database_event_session_actions.event_id<br /><br /> Sys.database_event_session_actions.object_id<br /><br /> Sys.database_event_session_actions.event_session_id|Sys.database_event_session_events.event_session_id<br /><br /> Sys.database_event_session_events.event_id|Molti-a-uno|  
|Sys.database_event_session_actions.event_session_id<br /><br /> Sys.database_event_session_actions.object_id|Sys.database_event_session_targets.event_session_id<br /><br /> Sys.database_event_session_targets.target_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  