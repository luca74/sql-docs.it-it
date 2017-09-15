---
title: Classe di evento PreConnect:Completed | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5f6bba668ddd25925ede8fe8cf71e4f1775f3dd9
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="preconnectcompleted-event-class"></a>classe di evento PreConnect:Completed
  La classe di evento PreConnect:Completed indica la fine dell'esecuzione di un trigger LOGON o di una funzione di classificazione di Resource Governor.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Colonne di dati della classe di evento PreConnect:Completed  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|216|27|No|  
|SPID|**int**|ID del processo del server che genera l'evento.|12|Sì|  
|EventSubClass|**int**|1 per la funzione di classificazione definita dall'utente.|21|Sì|  
|StartTime|**datetime**|Ora di avvio della funzione di classificazione definita dall'utente.|14|Sì|  
|EndTime|**datetime**|Ora di avvio della funzione di classificazione definita dall'utente.|15|Sì|  
|Durata|**bigint**|Durata della funzione di classificazione in microsecondi.|13|Sì|  
|ObjectID|**int**|ID dell'oggetto di classificazione definito dall'utente.|22|Sì|  
|CPU|**int**|Utilizzo della CPU in millisecondi.|18|Sì|  
|Reads|**int**|Numero di letture logiche.|16|Sì|  
|Writes|**int**|Numero di scritture logiche.|17|Sì|  
|GroupID|**int**|ID del gruppo del carico di lavoro classificato.|66|Sì|  
|Errore|**int**|Ultimo numero di errore se non è possibile eseguire la funzione di classificazione definita dall'utente.|31|Sì|  
|State|**int**|Stato dell'ultimo errore.|30|Sì|  
|TargetUserName|**sysname**|Valore restituito (nome del gruppo del carico di lavoro) per la funzione di classificazione definita dall'utente se non è possibile trovare un gruppo attivo corrispondente. Negli altri casi la colonna è impostata su NULL.|39|Sì|  
|ObjectName|**nvarchar(256)**|Nome in due parti della funzione di classificazione definita dall'utente, ad esempio dbo.classifier.|34|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)   
 [Classe di evento PreConnect:Starting](../../relational-databases/event-classes/preconnect-starting-event-class.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  