---
title: MSmerge_articlehistory (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd2fef95a478eebc6526fc888fa621c1ec198ab
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msmergearticlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_articlehistory** tabella tiene traccia delle modifiche apportate agli articoli durante una sessione di sincronizzazione dell'agente di Merge, con una riga per ogni articolo a cui sono state apportate modifiche. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|L'ID di una sessione del processo di agente di Merge nel [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) tabella di sistema.|  
|**phase_id**|**int**|Fase della sessione di sincronizzazione, i cui valori possono essere:<br /><br /> **1** = caricamento.<br /><br /> **2** = download.<br /><br /> **4** = pulizia.<br /><br /> **5** = chiusura.<br /><br /> **6** = modifiche dello schema.<br /><br /> **7** = BCP.|  
|**article_name**|**sysname**|Nome dell'articolo al quale sono state apportate le modifiche.|  
|**start_time**|**datetime**|Ora di inizio dell'elaborazione dell'articolo.|  
|**duration**|**int**|Durata dell'elaborazione di un articolo, in secondi.|  
|**inserimenti**|**int**|Numero di inserimenti applicati a un articolo specifico durante la sincronizzazione. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**aggiornamenti**|**int**|Numero di aggiornamenti applicati a un articolo specifico durante la sincronizzazione. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**Elimina**|**int**|Numero di eliminazioni applicate a un articolo specifico durante la sincronizzazione. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**è in conflitto**|**int**|Numero di conflitti che si sono verificati durante la sincronizzazione. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**conflicts_resolved**|**int**|Numero di conflitti che si sono verificati durante la sincronizzazione e che sono stati risolti. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**rows_retried**|**int**|Numero di righe per cui si è verificato un errore e che sono state ritentate durante la sincronizzazione. Questo valore verrà incrementato durante il processo di sincronizzazione e il valore finale rappresenta il numero totale.|  
|**percent_complete**|**decimal**|Percentuale del tempo di sincronizzazione totale impiegato dall'agente di merge per l'articolo durante la sessione. Questo valore è Null fino a quando la sessione non è stata completata.|  
|**estimated_changes**|**int**|Stima del numero di modifiche di riga che devono essere applicate all'articolo.|  
|**relative_cost**|**decimal**|Tempo impiegato per l'applicazione delle modifiche per questo articolo in rapporto al tempo totale per l'intera sessione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
